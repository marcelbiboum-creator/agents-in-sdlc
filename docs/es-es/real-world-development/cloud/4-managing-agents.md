---
title: "Ejercicio 4 - Supervisar y gestionar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

En los ejercicios anteriores pediste al agente en la nube de Copilot que asumiera tres tareas diferentes centradas en mejorar la experiencia de usuario y añadir funcionalidades. Aunque el agente está diseñado para operar de forma asincrónica y autónoma, supervisar esas tareas sigue siendo importante.

Puedes gestionar las tareas asignadas al agente desde la [página de agentes][agents-page] de GitHub.com. Desde este centro de control puedes ver todas las tareas de agentes con solicitudes de incorporación de cambios abiertas, explorar las operaciones realizadas e incluso orientar una sesión en curso.

En esta lección:

- explorarás la página de agentes para supervisar las tareas del agente en la nube;
- orientarás una sesión activa para solicitar funcionalidad adicional.

## Escenario

Después de asignar al agente la creación de un modo de alto contraste, el equipo considera que también sería apropiado añadir un modo claro. Como ya se están actualizando los estilos y creando los controles de cambio, parece lógico incluir esta funcionalidad. Quieres orientar el trabajo del agente para que añada el modo claro además del modo de alto contraste.

## Revisar las tareas del agente en la nube

1. Ve a la [página de agentes de Copilot][agents-page].
2. Observa la lista de tareas en el panel principal y en el lateral. Deberías ver las tareas asignadas, por ejemplo:
   - actualizar la documentación del código;
   - generar APIs para modificar juegos;
   - añadir un modo de alto contraste al sitio.
3. Selecciona una tarea en ejecución y revisa las operaciones realizadas por Copilot. Pueden incluir:
   - obtener el código del repositorio;
   - crear el entorno de trabajo;
   - configurar servidores MCP;
   - ejecutar los pasos necesarios para completar la tarea.

> [!NOTE]
> Los pasos exactos pueden variar según el estado del trabajo y el enfoque que haya utilizado Copilot.

4. También observa el panel de solicitudes de incorporación de cambios situado a la derecha, donde puedes revisar la PR y los archivos modificados.

## Orientar al agente en la nube

Ahora pedirás a Copilot que incluya el modo claro mientras trabaja en el modo de alto contraste.

1. Selecciona la sesión relacionada con la incorporación del modo de alto contraste.
2. Espera hasta que indique que ha completado la configuración y comenzado el trabajo.
3. En el cuadro **Steer active session while Copilot is working**, añade:

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

4. Pulsa <kbd>Enter</kbd> para enviar la indicación.
5. Observa cómo Copilot reconoce la indicación y la incorpora a su flujo de trabajo.

## Permitir que Copilot termine el trabajo

Copilot incorporará la nueva solicitud a su flujo después de completar el paso concreto que estaba realizando al recibir el mensaje. Esto puede tardar varios minutos.

## Resumen y próximos pasos

Has explorado la página de agentes de Copilot, tu centro de control para supervisar y orientar las tareas del agente en la nube. Desde ella puedes seguir todas las tareas activas y completadas, revisar el trabajo y redirigir tareas en curso.

Ahora puedes pasar a [iterar sobre las solicitudes de incorporación de cambios creadas por Copilot][next-lesson].

## Recursos

- [Página de agentes de Copilot][agents-page]
- [Acerca de los agentes personalizados][custom-agents]

---

| [← Ejercicio anterior: Agentes personalizados][previous-lesson] | [Siguiente ejercicio: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
