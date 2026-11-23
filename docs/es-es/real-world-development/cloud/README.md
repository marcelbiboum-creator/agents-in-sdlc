---
slug: es-es/real-world-development/cloud
title: "Agente en la nube de GitHub Copilot"
description: "Añade instrucciones personalizadas y asigna incidencias al agente en la nube de Copilot mientras aprendes a supervisar, orientar e iterar sobre su trabajo."
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

**[Agente en la nube de GitHub Copilot][cloud-agent]** permite que GitHub Copilot trabaje de forma asincrónica en la nube. Asignas trabajo en GitHub y el agente en la nube lo recoge en segundo plano: explora el repositorio, realiza cambios y abre una solicitud de incorporación de cambios, mientras tú puedes dedicarte a otras tareas.

A lo largo de estos ejercicios añadirás instrucciones personalizadas que seguirá el agente en la nube, después asignarás una incidencia de GitHub y permitirás que implemente el trabajo. Revisarás el trabajo y utilizarás agentes personalizados para dar forma a su enfoque, supervisarás y orientarás las sesiones desde el panel de agentes y terminarás revisando sus solicitudes de incorporación de cambios e iterando sobre los resultados.

## Ejercicios

| Ejercicio | Tema | Descripción |
| ---------- | ----- | ----------- |
| [0. Requisitos previos][ex0] | Configuración | Crea tu repositorio y tu Codespace |
| [1. Instrucciones personalizadas][ex1] | Contexto | Añade instrucciones personalizadas que seguirá el agente en la nube |
| [2. Agente en la nube][ex2] | Agente asincrónico | Asigna incidencias al agente en la nube de Copilot |
| [3. Agentes personalizados][ex3] | Agentes especializados | Revisa y utiliza agentes personalizados |
| [4. Gestión de agentes][ex4] | Supervisión | Supervisa y orienta las sesiones de agentes |
| [5. Iteración][ex5] | Revisión | Revisa las PR, itera sobre el trabajo de Copilot y elige los próximos pasos |

## Requisitos previos

Antes de asistir a este taller, asegúrate de tener:

- [ ] Una cuenta de GitHub con un plan activo de **Copilot Student, Pro, Pro+, Business o Enterprise**
- [ ] El agente en la nube de Copilot habilitado para tu cuenta o organización

> [!TIP]
> ¿No tienes un plan de pago? Los estudiantes verificados pueden obtener GitHub Copilot gratis a través de [GitHub Education][student-plan]. El plan **Copilot Student** incluye las funciones de agente, MCP, revisión de código y Copilot CLI que utiliza este taller.

> [!NOTE]
> El agente en la nube está disponible en **Copilot Student, Pro, Pro+, Business y Enterprise**, todas las modalidades excepto Copilot Free. En Copilot Business o Enterprise, un administrador debe habilitarlo para tu organización.

> [!NOTE]
> Este recorrido no incluye MCP. Para explorar servidores MCP con Copilot, consulta el [recorrido de CLI][cli] o el [recorrido de VS Code][vscode].

## Primeros pasos

**[Empieza con el ejercicio 0: Requisitos previos →][ex0]**

[cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[student-plan]: https://github.com/education/students
[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-cloud-agent/
[ex3]: 3-custom-agents/
[ex4]: 4-managing-agents/
[ex5]: 5-iterating/
[cli]: ../cli/
[vscode]: ../vscode/
