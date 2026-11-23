---
title: "Ejercicio 4 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## ¿Qué son los agentes personalizados?

Los [agentes personalizados][custom-agents-concept] de GitHub Copilot permiten crear asistentes de IA especializados para tareas o ámbitos concretos del flujo de desarrollo. Al definir agentes mediante archivos Markdown en `.github/agents`, puedes proporcionar a Copilot instrucciones centradas, procedimientos recomendados, patrones de código y conocimientos específicos del dominio. Los equipos pueden convertir su experiencia en agentes reutilizables: un agente de accesibilidad que aplique las pautas [WCAG][wcag], un agente de seguridad que siga prácticas seguras o un agente de pruebas que mantenga patrones coherentes.

Cada agente personalizado se define con un archivo Markdown que contiene frontmatter YAML con `name` y `description`, seguido de instrucciones que definen su comportamiento y conocimientos.

Los agentes personalizados y las [habilidades de agente][agent-skills-concept] tienen cierta superposición. Un agente personalizado representa al trabajador y las habilidades representan herramientas que puede utilizar.

> [!NOTE]
> No existe una única forma correcta de crear un agente personalizado. Hay que probar e iterar para encontrar el enfoque adecuado a cada entorno.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## Escenario

Tailspin Toys quiere que su plataforma sea accesible para todas las personas. Los comentarios indican que algunas personas encuentran difícil leer el tema oscuro por su bajo contraste. El equipo de diseño ha solicitado un modo de alto contraste que pueda activarse y desactivarse.

En este ejercicio:

- revisarás un agente personalizado de accesibilidad existente;
- utilizarás el agente en Copilot Chat para implementar el modo de alto contraste.

## Revisar el agente personalizado de accesibilidad

Ya existe un agente personalizado de accesibilidad para este taller.

1. Vuelve a tu Codespace y crea una rama nueva desde `main`:

   ```bash
   git checkout main
   git pull
   git checkout -b accessibility-vscode
   ```

2. Abre `.github/agents/accessibility.md`.
3. Observa el frontmatter YAML con `name` y `description`.

> [!CAUTION]
> Los campos `name` y `description` son obligatorios en el frontmatter de un agente personalizado.

4. Revisa las secciones siguientes:
   - responsabilidades principales;
   - procedimientos recomendados de accesibilidad;
   - ejemplos de HTML, CSS y JavaScript;
   - errores habituales.

## Utilizar el agente personalizado en Copilot Chat

VS Code muestra los agentes personalizados definidos en `.github/agents` en el desplegable de agentes de Copilot Chat.

1. Selecciona **Agent** en el desplegable si aún no está seleccionado.
2. Abre el desplegable situado en la parte inferior de la vista de Chat.
3. Selecciona **Accessibility agent**.
4. Envía:

   ```plaintext
   Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
   ```

5. Copilot Chat explorará el código, propondrá cambios y los aplicará.
6. Observa el indicador **Files changed** y revisa los archivos modificados.

> [!NOTE]
> Este proceso puede tardar varios minutos. Copilot puede modificar componentes Astro, CSS y pruebas relacionadas.

Revisarás y orientarás este trabajo en el siguiente ejercicio.

## Resumen y próximos pasos

Has explorado los [agentes personalizados][custom-agents] de GitHub Copilot y utilizado el modo agente de Copilot Chat para implementar una funcionalidad con el agente de accesibilidad.

A continuación, [supervisarás y orientarás el trabajo del agente][next-lesson], revisarás los cambios y añadirás un control de modo claro.

## Recursos

- [Acerca de los agentes personalizados][custom-agents]
- [Crear agentes personalizados en el IDE][creating-custom-agents-ide]
- [Agentes personalizados en VS Code][custom-agents-vscode]
- [Configuración de agentes personalizados][custom-agents-config]

---

| [← Ejercicio anterior: Probar con Playwright MCP][previous-lesson] | [Siguiente ejercicio: Supervisar y gestionar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
