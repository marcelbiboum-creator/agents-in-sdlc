---
title: "Lección 10 - Repaso y próximos pasos"
description: "Recapitula el flujo de trabajo de Copilot CLI, las dos solicitudes de incorporación de cambios, las personalizaciones reutilizables y otros recursos."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Has utilizado GitHub Copilot CLI a lo largo de un flujo de trabajo continuo con Tailspin Toys. Has:

- preparado un Codespace, instalado Copilot CLI, explorado el proyecto y encontrado la incidencia de filtrado incluida;
- añadido valoraciones por estrellas, revisado el resultado en un navegador reenviado y combinado manualmente tu primera solicitud de incorporación de cambios (PR);
- partido de la incidencia de filtrado, definido el enfoque en modo Plan, creado la funcionalidad en modo Autopilot y revisado el resultado en modo Interactive;
- orientado al agente con instrucciones personalizadas, después personalizado la habilidad existente `quality-checks` y utilizado para ejecutar pruebas unitarias, lint y comprobaciones de tipos;
- añadido el servidor Model Context Protocol (MCP) de Playwright y utilizado para explorar el filtrado en un navegador real;
- creado y seleccionado un agente personalizado de aseguramiento de la calidad (QA) para evaluar requisitos, cobertura, resultados de habilidades y evidencia del navegador;
- revisado el cambio completo de filtrado y autorizado Agent Merge para la PR del filtrado;
- explorado comandos de barra para el contexto, los modelos, el uso compartido y la delegación opcional a la nube.

## Qué has publicado

El taller tiene dos hitos de PR, cada uno en su propia rama creada a partir de `main` actualizado:

1. **Valoraciones por estrellas:** muestra el `starRating` existente y un estado explícito «sin valorar» en las tarjetas de juegos.
2. **Flujo de trabajo de filtrado y calidad:** implementa el filtrado, actualiza las instrucciones y aplícalas a la funcionalidad, personaliza el informe de `quality-checks`, crea un perfil de QA e incluye las pruebas asociadas.

Desde la planificación del filtrado hasta la apertura de su PR, has utilizado la misma conversación y rama. Hemos combinado ese trabajo en una sola PR para optimizar el taller.

## Distintos tipos de verificación

Has comprobado el código de varias maneras: pruebas automatizadas, tu propia inspección en el navegador y la exploración del navegador realizada por Copilot mediante MCP. La habilidad `quality-checks` ejecutó pruebas unitarias, lint y comprobaciones de tipos e informó de los resultados con el nuevo formato. QA reunió esos resultados con una revisión de los requisitos y la cobertura de pruebas antes de la PR.

Las pruebas añadidas deben cubrir brechas reales; una ejecución de QA que no necesite nuevas pruebas puede ser correcta. Revisa el código y las evidencias antes de autorizar la combinación y actualiza las evidencias afectadas después de los cambios.

## Mejores prácticas

El contexto y las herramientas que proporcionas a Copilot determinan su trabajo. En este taller, has actualizado instrucciones, personalizado una habilidad, creado un perfil de QA y configurado un servidor MCP. Reutiliza estas personalizaciones entre conversaciones y ajústalas a medida que cambien las necesidades de tu equipo. Las instrucciones establecen estándares, las habilidades describen tareas repetibles, los agentes personalizados definen funciones especialistas y los servidores MCP conectan herramientas externas. Revisa los cambios reales y los resultados de las herramientas, no solo el resumen del agente.

Haz coincidir el **modo y el modelo** con la tarea. Usa **Plan** para reflexionar sobre el enfoque antes de crear, **Interactive** para mantener el control en cambios centrados y **Autopilot** para tareas bien delimitadas. Elige un modelo más rápido para ediciones rutinarias y uno más capaz para trabajos complejos.

El contexto sigue siendo tan importante como la infraestructura. Describir claramente *qué* quieres construir, *por qué* y *cómo* cambia significativamente el resultado.

## Más por explorar

Ya has cubierto el flujo de trabajo principal. Estas son otras funciones de CLI que merece la pena revisar:

- `/review`, para pedir al agente de revisión de código que analice los cambios;
- `/rubber-duck`, para hablar de un problema y obtener otra perspectiva;
- `/fleet`, para organizar subtareas independientes en paralelo;
- `/worktree`, para aislar una tarea independiente;
- `/delegate`, para enviar una tarea a Copilot cloud agent.

## Próximos pasos

La mejor manera de mejorar con cualquier herramienta es seguir utilizándola. Úsala para código de producción, para proyectos personales y para esa pequeña aplicación que llevas años teniendo en mente y nunca has creado. Comparte tus aprendizajes con tu equipo y aprende de los suyos. Y, como siempre, explora la documentación.

Si quieres ampliar Tailspin Toys desde el terminal, continúa con la serie opcional [Foundry Backer Concierge][foundry]. Para comparar otros entornos, explora el [taller de VS Code][vscode], el [taller de la aplicación GitHub Copilot][app] o el [taller de Copilot cloud agent][cloud].

## Recursos

- [Acerca de GitHub Copilot CLI][about-cli]
- [Referencia de comandos de Copilot CLI][cli-reference]
- [Personalizar Copilot CLI][customize-cli]
- [Gestionar solicitudes de incorporación de cambios con Copilot CLI][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
