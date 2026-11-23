---
title: "Ejercicio 2 - Agente en la nube de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Ejercicio anterior: Instrucciones personalizadas][previous-lesson] |
|:--|

Probablemente pocas organizaciones, o ninguna, puedan decir que no tienen deuda técnica. Puede tratarse de problemas de seguridad sin resolver, código heredado que necesita actualizaciones o solicitudes de funcionalidades que llevan tiempo en el backlog porque no había tiempo para implementarlas. El agente en la nube de GitHub Copilot está diseñado para realizar tareas como actualizar código y añadir funcionalidades de forma autónoma. Cuando termina, genera una PR en borrador lista para que una persona la revise.

Explorarás los siguientes aspectos:

- personalizar el entorno para generar código;
- garantizar que las operaciones se realizan de forma segura;
- la importancia de definir bien el alcance de las incidencias;
- asignar incidencias a Copilot.

## Escenarios

Tailspin Toys tiene deuda técnica que quiere resolver. Los contratistas que crearon la primera versión dejaron la documentación en un estado poco adecuado: simplemente no existía. Como primer paso, quieren añadir comentarios TSDoc a todas las funciones exportadas de la aplicación.

El equipo de diseño también quiere mejorar el descubrimiento de juegos. Quiere que la página de detalles de cada juego muestre otros juegos relacionados de la misma categoría, para que las personas puedan seguir navegando. No necesitan una implementación pulida todavía; solo quieren algo utilizable para probar la experiencia. Es un bloqueador actual, pero hay otras incidencias con prioridad más alta.

Estos son ejemplos de tareas que pueden quedar aplazadas y son ideales para asignarlas al agente en la nube de Copilot. El agente podrá trabajar de forma asincrónica, permitiendo al desarrollador centrarse en otras tareas y volver después para revisar el trabajo de Copilot.

## Presentamos el agente en la nube de GitHub Copilot

El [agente en la nube de GitHub Copilot][copilot-agents] puede realizar tareas en segundo plano, de forma similar a un desarrollador. Puede hacerlo de varias maneras, incluida la [asignación de una incidencia de GitHub a Copilot][assign-issue]. Al asignarla, Copilot crea una solicitud de incorporación de cambios en borrador para seguir el progreso, configura un entorno y comienza a trabajar. Puedes consultar su sesión mientras está en curso o después de finalizar. Cuando esté lista para la revisión, te indicará en la solicitud de incorporación de cambios.

## La importancia de instrucciones bien delimitadas

No hay magia en GitHub Copilot: no puedes evitar el pensamiento necesario. Incluso las operaciones aparentemente sencillas adquieren complejidad al profundizar, así que [delimita cuidadosamente las tareas para el agente en la nube][cloud-agent-best-practices]. Trátalo como a un compañero de programación con IA: trabaja por fases, aprende, experimenta y adapta el enfoque. Los fundamentos del desarrollo de software no cambian por la incorporación de IA generativa.

## Instrucciones personalizadas en este repositorio

Los ejercicios anteriores presentan las instrucciones personalizadas y explican cómo orientan a Copilot. Si ya has trabajado con las instrucciones personalizadas, ya conoces `.github/copilot-instructions.md`; si no, este es un buen momento para revisarlo. Antes de asignar trabajo al agente en la nube, consulta los archivos de instrucciones incluidos en el repositorio para observar su efecto más adelante.

Abre los siguientes archivos en la interfaz web de GitHub o en un Codespace:

- `.github/copilot-instructions.md`: revisa la sección **Code standards**, especialmente las expectativas para TypeScript y los comentarios TSDoc.
- `.github/instructions/unit-tests.instructions.md`: observa el frontmatter `applyTo`, que limita estas instrucciones a los archivos `**/*.test.ts`.

Cuando asignes la incidencia `Code lacks documentation` al agente en la nube, observa los comentarios TSDoc, las convenciones de TypeScript y los encabezados de comentario de la solicitud de incorporación de cambios resultante.

## Configurar el entorno de desarrollo del agente en la nube

Crear código requiere un entorno concreto y scripts de configuración que garanticen que todo esté listo. Lo mismo ocurre con las tareas asignadas a Copilot.

El agente en la nube utiliza [GitHub Actions][github-actions] para su entorno. Puedes personalizarlo mediante un [flujo de trabajo de configuración especial][setup-workflow], definido en `.github/workflows/copilot-setup-steps.yml`, que se ejecuta antes de que el agente empiece.

Este entorno ya está preconfigurado para el laboratorio y garantiza acceso a Node.js, las dependencias del proyecto, los navegadores de Playwright y la base de datos SQLite migrada y poblada:

```yaml
name: "Copilot Setup Steps"

# Permite probar los pasos de configuración desde la pestaña Actions del repositorio
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Establece los permisos mínimos necesarios
    permissions:
      # Si quieres clonar el repositorio como parte de la configuración, necesitarás permisos contents: read
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Configuración de frontend y aplicación: el proyecto completo utiliza Astro y Drizzle/libSQL
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migra y completa la base de datos SQLite local
      - name: Set up the database
        run: npm run db:setup
```

El flujo contiene un único trabajo, `copilot-setup-steps`, que GitHub Actions ejecuta antes de que Copilot comience a trabajar en la solicitud de incorporación de cambios. El desencadenador `workflow_dispatch` permite probar manualmente el flujo desde la pestaña **Actions**.

## Añadir documentación

1. Abre tu repositorio en github.com en una pestaña nueva.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** y después **Blank issue**.
4. Establece el título en `Code lacks documentation`.
5. Establece la descripción en:

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

6. Selecciona **Create**.
7. En el lateral derecho, selecciona **Assign to Copilot** y después **Assign**.
8. Abre la pestaña **Pull Requests** y revisa la solicitud titulada de forma similar a `[WIP]: Code lacks documentation`. Si todavía no aparece, espera unos minutos y actualiza la página.
9. Observa la lista de tareas que crea Copilot.
10. Cuando Copilot haya iniciado el trabajo, selecciona **View session** y sigue su análisis y ejecución.

> [!NOTE]
> La creación de la sesión y del entorno puede tardar varios minutos.

## Añadir una sección de juegos relacionados

Una ventaja del agente en la nube es que permite dividir el trabajo: tú puedes seguir con otra tarea mientras el agente trabaja en esta.

1. Vuelve al repositorio en github.com.
2. Abre **Issues**, selecciona **New issue** y usa **Blank issue**.
3. Establece el título en `Show related games on the game details page`.
4. Establece la descripción en:

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

5. Crea la incidencia y asígnala a Copilot.

Copilot comenzará su segunda tarea en segundo plano. No necesitas supervisarla continuamente: volverás para revisar su trabajo una vez finalizado.

## Resumen y próximos pasos

Este ejercicio ha presentado el [agente en la nube de GitHub Copilot][copilot-agents]. Puedes asignarle incidencias para que realice tareas de forma asincrónica, ya sean deuda técnica, nuevas funcionalidades o migraciones.

Has explorado:

- la personalización del entorno de generación de código;
- las restricciones de seguridad;
- la importancia de incidencias bien delimitadas;
- la asignación de incidencias a Copilot.

Con el agente trabajando en segundo plano, puedes pasar a crear y utilizar [agentes personalizados][next-lesson].

## Recursos

- [Acerca del agente en la nube de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Procedimientos recomendados del entorno de configuración del agente en la nube][cloud-agent-best-practices]

| [Ejercicio siguiente: Agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
