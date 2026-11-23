---
title: "Lección 8 - Crear y combinar la PR de la funcionalidad"
description: "Revisa juntos el filtrado, las instrucciones, la actualización de la habilidad, el perfil de QA y las pruebas, y después crea una PR y utiliza Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

La implementación del filtrado, las actualizaciones de las instrucciones, la actualización de la habilidad, el perfil de aseguramiento de la calidad (QA) y las pruebas están guardados en una rama. Es el momento de revisarlos juntos y abrir una solicitud de incorporación de cambios. Tú combinaste manualmente la solicitud de valoración por estrellas; esta vez permitirás que **Agent Merge** gestione el proceso.

> [!NOTE]
> Normalmente dividiríamos la funcionalidad, las actualizaciones de instrucciones, la actualización de la habilidad y el agente de QA en varias PR independientes. Para optimizar el taller, has mantenido el flujo completo de filtrado y calidad en una conversación y una rama, y todo ese trabajo se incluirá en esta PR.

En esta lección:

- aprenderás qué es Agent Merge y cómo automatiza el ciclo de vida de la combinación;
- inspeccionarás el cambio completo de la funcionalidad y las evidencias de verificación;
- crearás la PR del filtrado;
- habilitarás Agent Merge solo después de la revisión y confirmarás que la PR esté combinada.

## Escenario

Durante el flujo de filtrado has utilizado Copilot para planificar, implementar y verificar una funcionalidad. Tailspin Toys quiere automatizar el resto del trabajo de la PR, pero mantener bajo control del desarrollador la autorización de combinación.

## Presentamos Agent Merge

**Agent Merge** automatiza el trabajo restante necesario para integrar una solicitud de incorporación de cambios. Al habilitarlo, Copilot trabaja sobre lo que bloquea la PR: corrige las comprobaciones fallidas de integración continua (CI), responde a los comentarios de revisión y hace rebase cuando sea necesario, y después habilita la combinación automática de GitHub cuando el repositorio lo permita.

Hasta ahora has seleccionado **Merge pull request** tú mismo. Agent Merge puede asumir esa responsabilidad. Revisa el trabajo y decide si está preparado antes de habilitarlo.

## Utilizar Agent Merge para gestionar la PR

Con todo el código creado, vamos a revisarlo conjuntamente, crear la PR y permitir que Agent Merge gestione el resto del proceso.

1. Vuelve a tu Codespace.
2. Abre el cuadro de diálogo del agente introduciendo `/agent`.
3. Selecciona **Default** en la lista y pulsa <kbd>Enter</kbd>.
4. Crea una PR nueva con el comando `/pr create`.
5. Activa Agent Merge con `/pr agentmerge`.
6. Copilot supervisará el proceso de integración continua de la PR. Cuando todo haya finalizado correctamente, realizará la combinación.
7. Asegúrate de ver un mensaje de Copilot similar a «PR #14 was squash-merged successfully».

> [!IMPORTANT]
> Agent Merge no elude aprobaciones necesarias, protecciones de rama, colas de combinación, configuración del repositorio ni permisos ausentes. Si se bloquea, lee el motivo indicado y completa la combinación revisada manualmente cuando el repositorio lo permita.

## Resumen y próximos pasos

Has automatizado varios aspectos del proceso de desarrollo, incluida la generación de código, las pruebas y la validación del código, y ahora el proceso de solicitudes de incorporación de cambios. Has:

- aprendido qué es Agent Merge y cómo automatiza el ciclo de vida de la combinación;
- inspeccionado el cambio completo de la funcionalidad y las evidencias de verificación;
- creado la PR del filtrado;
- habilitado Agent Merge solo después de la revisión y confirmado que la PR estaba combinada.

A continuación, [explorarás otros comandos de barra útiles de Copilot CLI][next-lesson] para el contexto, los modelos, el uso compartido y la delegación opcional a la nube.

## Recursos

- [Gestionar solicitudes de incorporación de cambios con Copilot CLI][manage-prs]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
