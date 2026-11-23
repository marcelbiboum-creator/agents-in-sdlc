---
title: "Ejercicio 3 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## ¿Qué son los agentes personalizados?

Los [agentes personalizados][custom-agents-concept] de GitHub Copilot permiten crear asistentes de IA especializados para tareas o ámbitos concretos del flujo de desarrollo. Al definir agentes mediante archivos Markdown en la carpeta `.github/agents` del repositorio, puedes proporcionar a Copilot instrucciones centradas, procedimientos recomendados, patrones de código y conocimientos específicos del dominio para que realice mejor determinados tipos de trabajo. Los equipos pueden convertir su experiencia en agentes reutilizables: un agente de accesibilidad que aplique las pautas [WCAG][wcag], un agente de seguridad que siga prácticas de programación segura o un agente de pruebas que mantenga patrones de pruebas coherentes.

Los agentes personalizados se definen con archivos Markdown en `.github/agents` o globalmente en `~/.copilot/agents`. Cada archivo tiene frontmatter YAML con al menos `name` y `description`, seguido de una indicación Markdown que define el comportamiento, la experiencia y las instrucciones del agente.

### Agentes personalizados frente a habilidades de agente

Los agentes personalizados y las [habilidades de agente][agent-skills-concept] tienen cierta superposición conceptual. Ambos se definen principalmente con archivos Markdown e indican a una IA cómo realizar operaciones. La diferencia más clara es que un **agente personalizado** es el trabajador y las **habilidades** son las herramientas.

Los agentes personalizados tienen su propia ventana de contexto y están preparados para orquestar habilidades e incluso otros agentes mientras realizan su trabajo.

> [!NOTE]
> No existe una única forma correcta de crear un agente personalizado. Como sucede con cualquier herramienta de IA, hay que probar e iterar para encontrar el enfoque adecuado a cada entorno y escenario.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## Escenario

Tailspin Toys quiere que su plataforma de financiación colectiva sea accesible para todas las personas, independientemente de sus capacidades o preferencias visuales. Los comentarios recientes indican que algunas personas encuentran difícil leer el tema oscuro actual por el contraste insuficiente entre el texto y el fondo. Para resolver este problema, el equipo de diseño ha solicitado un modo de alto contraste que las personas puedan activar y desactivar.

En este ejercicio:

- revisarás un agente personalizado de accesibilidad existente;
- asignarás una tarea a un agente personalizado.

## Revisar el agente personalizado de accesibilidad

Ya existe un agente personalizado de accesibilidad creado para este taller. Revísalo para comprender cómo orientará a Copilot.

1. Vuelve a tu Codespace y abre `.github/agents/accessibility.md`.
2. Observa el frontmatter YAML con los campos `name` y `description`.

> [!CAUTION]
> Los campos `name` y `description` del frontmatter son obligatorios para los agentes personalizados.

3. Revisa las siguientes secciones:
   - responsabilidades principales al generar código para un sitio accesible;
   - procedimientos recomendados de accesibilidad;
   - ejemplos de código HTML, CSS y JavaScript;
   - errores y malas prácticas habituales.

## Crear y asignar una incidencia

Utilizarás el centro de control de misión para asignar al agente en la nube la creación del modo de alto contraste.

1. Ve a tu repositorio.
2. Selecciona la pestaña **Issues** y después **New issue**.
3. Selecciona **Blank issue**.
4. Establece el título en `Add high contrast mode to website`.
5. Establece la descripción en:

   ```plaintext
   We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
   ```

6. Selecciona **Create**.
7. En el lateral derecho, selecciona **Assign to Copilot**.
8. Selecciona **Accessibility agent** en la lista de agentes personalizados y después **Assign**.

Copilot comenzará a trabajar en segundo plano.

## Resumen y próximos pasos

Este ejercicio ha presentado los [agentes personalizados][custom-agents] de GitHub Copilot: asistentes especializados diseñados para tareas y ámbitos concretos. Con los agentes personalizados puedes codificar los conocimientos y estándares de tu equipo en agentes reutilizables que orienten a Copilot.

Ahora puedes pasar a [supervisar y orientar la sesión del agente][next-lesson] desde el centro de control.

## Recursos

- [Acerca de los agentes personalizados][custom-agents]
- [Prepararse para utilizar agentes personalizados en tu organización][org-custom-agents]
- [Prepararse para utilizar agentes personalizados en tu empresa][enterprise-custom-agents]

---

| [← Ejercicio anterior: Agente en la nube de Copilot][previous-lesson] | [Siguiente ejercicio: Supervisar y gestionar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
