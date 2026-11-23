---
title: "Ejercicio 5: Iterar sobre el trabajo de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Ejercicio anterior: Gestión de agentes][previous-lesson] |
|:--|

## Revisar el trabajo

Durante este taller has trabajado con GitHub Copilot en varias tareas centradas en mejorar la experiencia de usuario y añadir funcionalidades. Has pedido a Copilot que documente el código, cree una funcionalidad de juegos relacionados y implemente accesibilidad con modos de alto contraste y claro. Ahora revisarás los cambios y, si es necesario, proporcionarás comentarios para mejorar el trabajo.

> [!NOTE]
> Los fundamentos del diseño de software y de DevOps no cambian por el uso de IA generativa. Debes revisar siempre el código generado y seguir tu proceso normal de DevOps.

## Seguridad y agente en la nube

Como el agente en la nube realiza su trabajo de forma asincrónica y sin supervisión directa, aplica restricciones de seguridad:

- Copilot solo tiene acceso de lectura al repositorio y acceso de escritura únicamente a la rama que utiliza para el código.
- El agente se ejecuta dentro de GitHub Actions en un entorno separado y efímero.
- Todos los flujos de trabajo de GitHub Actions requieren aprobación humana antes de ejecutarse.
- El acceso a recursos externos está limitado de forma predeterminada, incluidos los servidores MCP.

## Revisar la documentación generada

1. Vuelve a tu repositorio en github.com.
2. Selecciona **Pull Requests** y abre la PR titulada de forma similar a **Add missing documentation**.
3. Si aparece el indicador `[WIP]`, espera a que Copilot termine; esto puede tardar varios minutos.
4. Selecciona la pestaña **Files changed** y revisa los cambios.
5. Observa los comentarios TSDoc, las convenciones de TypeScript y los encabezados de archivo añadidos. Estas incorporaciones proceden de los archivos de instrucciones revisados al principio del ejercicio.

## Solicitar cambios a GitHub Copilot

Puedes pedir cambios a Copilot en una conversación o mediante comentarios en línea dentro de una solicitud de incorporación de cambios.

1. Añade un comentario que solicite una mejora y etiqueta a `@copilot`, como harías con cualquier miembro del equipo.
2. Puedes pedir, por ejemplo:
   - añadir encabezados de comentario al comienzo de cada archivo;
   - añadir comentarios TSDoc a archivos TypeScript y Astro;
   - crear un README que describa la estructura de la aplicación Astro.
3. Selecciona **View Session** para observar cómo Copilot crea una nueva sesión y realiza las actualizaciones.
4. Vuelve a la PR y revisa el nuevo confirmación en la pestaña **Files changed**.

## Revisar la funcionalidad de juegos relacionados

1. Vuelve a tu repositorio.
2. Abre la PR titulada de forma similar a **Show related games on the game details page**.
3. Selecciona **Files changed** y revisa el código generado.
4. Si faltan trabajos de aprobación de flujos de trabajo, selecciona **Approve and run workflows**.
5. Espera a que las comprobaciones del proyecto finalicen correctamente.
6. Si quieres probar manualmente la funcionalidad, puedes cambiar a la rama creada por Copilot desde tu Codespace:

   ```bash
   git fetch origin
   git checkout <nombre-de-la-rama>
   ```

## Revisar las funciones de accesibilidad

Finalmente, revisa la PR de las funciones de accesibilidad implementadas con el agente personalizado. Debe incluir el modo de alto contraste solicitado en el ejercicio 3 y el modo claro solicitado después.

Revisa especialmente:

- los controles para cambiar entre modos;
- el uso de almacenamiento local para persistir las preferencias;
- los cambios CSS de los modos claro y de alto contraste;
- los atributos de accesibilidad, como las etiquetas ARIA y la navegación con teclado;
- el código JavaScript o TypeScript que gestiona el cambio de modo.

Si las comprobaciones están a la espera, apruébalas y espera a que finalicen correctamente. Puedes cambiar a la rama en tu Codespace y probar manualmente ambos controles:

```bash
git fetch origin
git checkout <nombre-de-la-rama>
```

Después inicia la aplicación y prueba los modos claro y de alto contraste en el navegador, incluido su comportamiento tras recargar la página.

## Ejercicio opcional: seguir delegando

El agente en la nube funciona mejor cuando puede asumir elementos reales del backlog y permitirte centrarte en otras tareas:

- crear un formulario de interés de mecenas en la página de detalles del juego;
- implementar paginación en la lista de juegos;
- añadir validación de entradas y gestión de errores a los ayudantes de acceso a datos.

## Resumen

Has completado el recorrido del agente en la nube. Durante estos ejercicios:

- has inspeccionado los archivos de instrucciones personalizados del repositorio;
- has asignado incidencias al agente en la nube y observado su entorno, planificación y ejecución asincrónica;
- has creado y utilizado un agente personalizado para accesibilidad;
- has utilizado la página de agentes como centro de control;
- has revisado e iterado sobre las solicitudes de incorporación de cambios del agente.

## Revisión y próximos pasos

Los otros recorridos complementan lo aprendido aquí:

- 🖥️ **[Recorrido de VS Code][vscode]**: explora el modo agente de Copilot Chat y la integración MCP desde el IDE.
- 💻 **[Recorrido de CLI][cli]**: entrega dos cambios revisados desde el terminal con los modos Plan y Autopilot, habilidades de agente, un agente personalizado de QA, Playwright MCP y Agent Merge.

En tu propio repositorio, prueba estas ideas:

- asignar al agente en la nube una incidencia de refactorización o de cobertura de pruebas;
- crear un agente personalizado para otro ámbito;
- configurar `copilot-setup-steps.yml` para otra pila tecnológica.

## Recursos

- [GitHub Copilot][github-copilot]
- [Acerca de los agentes de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Procedimientos recomendados del entorno del agente en la nube][cloud-agent-best-practices]
- [Configurar el cortafuegos del agente en la nube][agent-firewall]

---

| [← Ejercicio anterior: Gestión de agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall
[vscode]: ../../vscode/
[cli]: ../../cli/
[previous-lesson]: ../4-managing-agents/
