---
title: "Lección 9 - Comandos de barra en GitHub Copilot CLI"
description: "Explora comandos de barra para gestionar el contexto, seleccionar modelos, compartir sesiones y delegar opcionalmente a la nube."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como cualquier buena herramienta de CLI, GitHub Copilot CLI incluye muchos comandos de barra para interactuar con ella. Estos comandos muestran funciones avanzadas, información interna y opciones de configuración adicionales. Ya has utilizado comandos como `/diff`, `/mcp`, `/skills`, `/agent` y `/pr`. Vamos a explorar algunos más.

En esta lección:

- utilizarás `/context` y `/compact` para explorar cómo Copilot gestiona el contexto de una conversación;
- utilizarás `/model` para explorar los modelos disponibles;
- aprenderás cómo `/share` puede exportar o compartir una sesión;
- explorarás comandos opcionales para el trabajo paralelo, los árboles de trabajo y la delegación al agente en la nube.

## Escenario

Ya has completado el flujo principal de CLI. Ahora veremos algunas funciones adicionales: gestión del contexto, cambio de modelos, uso compartido de sesiones y delegación opcional a [Copilot cloud agent][about-cloud-agent].

## Explorar el contexto de Copilot CLI

Cuando trabajas en tareas mayores o más complejas, puede que alcances el límite máximo de la ventana de contexto del modelo. Copilot CLI compacta automáticamente la conversación cuando es necesario, y tú puedes inspeccionarla o compactarla con comandos de barra.

1. Vuelve a tu Codespace e inicia Copilot CLI desde la raíz del repositorio si aún no está abierto.
2. Introduce:

   ```plaintext
   /context
   ```

3. Observa el modelo, el uso actual de tokens y cómo se distribuye el contexto entre las instrucciones del sistema, las herramientas, los mensajes y el espacio libre.
4. Compacta la conversación:

   ```plaintext
   /compact
   ```

5. Introduce `/context` de nuevo y compara el resultado. Puede que no haya un cambio drástico si la conversación ya es pequeña.

> [!NOTE]
> Copilot CLI compacta automáticamente el contexto cuando se llena la ventana. Utiliza `/compact` cuando quieras elegir el momento. Utiliza `/clear` o `/new` cuando cambies a una tarea no relacionada y quieras una conversación nueva.

## Elegir el modelo

Los distintos modelos tienen fortalezas diferentes y los desarrolladores tienen preferencias distintas. Copilot CLI te permite listar y seleccionar el modelo que quieres utilizar.

1. Introduce:

   ```plaintext
   /model
   ```

2. Explora los modelos disponibles y la información de uso.
3. Conserva el modelo actual, selecciona otro o pulsa <kbd>Esc</kbd> para cerrar la lista.

## Compartir una sesión

Trabajar en equipo y compartir conocimientos ayuda a todos a mejorar su uso de las herramientas de IA. El comando `/share` puede exportar una sesión a un archivo Markdown o HTML, crear un enlace compartible o publicar un gist de GitHub.

1. Introduce `/help` y revisa las opciones de `/share` disponibles en tu versión instalada.
2. Si quieres compartir esta sesión, elige el destino que se ajuste a tus necesidades, por ejemplo `/share file` para una exportación Markdown local.
3. Revisa el contenido exportado antes de enviarlo a alguien o publicarlo. Las exportaciones de sesión pueden incluir indicaciones, respuestas y detalles del proyecto.

Publicar un enlace o gist es opcional. No publiques contenido del repositorio ni de conversaciones que tu equipo no haya decidido compartir.

## Opcional: escalar o delegar

El taller principal ya está completo. Copilot CLI también ofrece comandos para tareas mayores:

- `/fleet` puede dividir subtareas independientes entre subagentes y ejecutarlas en paralelo.
- `/worktree` puede crear un árbol de trabajo de Git aislado para una tarea independiente.
- `/delegate` puede enviar una tarea a Copilot cloud agent, que trabaja de forma asincrónica y puede abrir una solicitud de incorporación de cambios.

Estos comandos son opcionales, porque pueden crear árboles de trabajo adicionales o trabajo remoto. Antes de probarlos, inicia una tarea nueva y bien delimitada, y revisa el resultado mediante tu flujo de trabajo habitual. Si quieres profundizar en el trabajo asincrónico con agentes, continúa con el [taller del agente en la nube][cloud-workshop].

## Resumen y próximos pasos

Utilizar comandos de barra en Copilot CLI te permite configurarlo, compartir sesiones y ver qué ocurre internamente. En esta lección:

- has utilizado `/context` y `/compact` para explorar cómo Copilot gestiona el contexto de una conversación;
- has utilizado `/model` para explorar los modelos disponibles;
- has aprendido cómo `/share` puede exportar o compartir una sesión;
- has explorado comandos opcionales para el trabajo paralelo, los árboles de trabajo y la delegación al agente en la nube.

Hay más comandos de barra disponibles y mucho más que explorar con Copilot CLI. Vamos a cerrar el recorrido [revisando lo aprendido][next-lesson] y viendo algunos próximos pasos para seguir aprendiendo.

## Recursos

- [Referencia de comandos de Copilot CLI][cli-reference]
- [Gestión del contexto en Copilot CLI][context-management]
- [Acerca de Copilot cloud agent][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
