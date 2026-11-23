---
title: "Ejercicio 3 - Probar la funcionalidad con el servidor MCP de Playwright"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Ejercicio anterior: Modo agente][previous-lesson] · [Siguiente ejercicio: Agentes personalizados →][next-lesson]

Acabas de crear la funcionalidad de filtrado con el modo agente. Antes de abrir una solicitud de incorporación de cambios debes confirmar que funciona en el navegador. En lugar de probarla manualmente, conectarás el **servidor MCP de Playwright** y permitirás que Copilot controle un navegador real.

En este ejercicio:

- aprenderás qué es Model Context Protocol (MCP) y cómo amplía Copilot;
- añadirás el servidor MCP de Playwright al espacio de trabajo;
- pedirás a Copilot que utilice el servidor para probar el filtrado;
- publicarás la rama y abrirás una PR.

## ¿Qué es Model Context Protocol (MCP)?

El modo agente gana capacidad cuando puede llegar más allá del editor. MCP proporciona a Copilot una forma estándar de comunicarse con herramientas y servicios externos.

![Diagrama del modo agente y su interacción con el contexto, el modelo y las herramientas, incluidas las herramientas aportadas por servidores MCP y extensiones de VS Code](../../../_images/ex1-mcp-diagram.png)

[Model Context Protocol (MCP)][mcp-blog-post] proporciona a los agentes de IA una forma de comunicarse con herramientas y servicios externos en tiempo real. Les permite acceder a información actualizada y realizar acciones en tu nombre.

Los servidores MCP actúan como puente entre el agente y las herramientas externas. Algunos populares son:

- **[Servidor MCP de GitHub][github-mcp-server]**: permite gestionar repositorios, incidencias y solicitudes de incorporación de cambios.
- **[Servidor MCP de Playwright][playwright-mcp-server]**: permite automatizar navegadores con Playwright.

GitHub mantiene un [registro MCP][mcp-registry] para facilitar el descubrimiento de servidores.

> [!CAUTION]
> Trata los servidores MCP como cualquier otra dependencia. Antes de utilizarlos, revisa su código fuente, verifica el editor y considera las implicaciones de seguridad.

## Revisar la configuración MCP

El archivo `.vscode/mcp.json` configura los servidores disponibles en el espacio de trabajo de VS Code.

1. Abre `.vscode/mcp.json` en tu Codespace.
2. Deberías ver ya configurado el servidor `github`:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       }
     }
   }
   ```

Esta entrada permite a Copilot leer el backlog en ejercicios anteriores mediante el [servidor remoto MCP de GitHub][remote-github-mcp-server].

## Añadir el servidor MCP de Playwright

1. En `.vscode/mcp.json`, añade una entrada `playwright` junto a `github`:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       },
       "playwright": {
         "command": "npx",
         "args": ["@playwright/mcp@latest", "--headless"]
       }
     }
   }
   ```

2. Guarda el archivo.

El servidor `playwright` es local: VS Code lo inicia ejecutando `npx @playwright/mcp@latest`. La opción `--headless` evita mostrar una ventana, lo que es necesario dentro de un Codespace.

> [!NOTE]
> Tailspin Toys ya utiliza Playwright para las pruebas de extremo a extremo, por lo que el navegador requerido probablemente ya esté instalado. Si falta, Copilot puede ejecutar `npx playwright install chromium`.

## Iniciar y confiar en el servidor

VS Code inicia los servidores MCP bajo demanda.

1. En `.vscode/mcp.json`, selecciona **Start** sobre la entrada `playwright`.
2. Si VS Code solicita confirmar que confías en el servidor, revisa la configuración y confírmala.

## Probar el filtrado

Con el servidor conectado y la aplicación en ejecución, pide a Copilot que pruebe la funcionalidad:

```text
Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

1. Go to the games page and note how many games are listed.
2. Apply a category filter and confirm the list updates to only show games in that category.
3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
4. Combine a category and a publisher filter and confirm the results respect both.

Report what you observe at each step, and call out anything that does not behave as expected.
```

Copilot lanzará el navegador, recorrerá los pasos y resumirá sus observaciones. Compara el resultado con los criterios de aceptación de la incidencia. Si algo no coincide, pide a Copilot que corrija el código antes de abrir la PR.

> [!NOTE]
> La aplicación debe estar disponible en `http://localhost:4321`. Si detuviste el servidor de desarrollo, inicia de nuevo antes de enviar la indicación.

## Publicar la rama y crear la solicitud de incorporación de cambios

1. En el panel **Source Control**, revisa los cambios realizados por Copilot.
2. Prepara los cambios seleccionando el icono **+**.
3. Genera un mensaje de confirmación con el botón **Sparkle**.
4. Selecciona **Publish** para enviar la rama `filtering-vscode`.

### Crear la PR

1. Abre Copilot Chat y selecciona **New Chat**.
2. Asegúrate de que **Agent** esté seleccionado.
3. Pide a Copilot:

   ```plaintext
   Find the issue in the repo related to filtering by category and publisher. Create a new pull request for the current branch, and associate it with the correct issue.
   ```

4. Selecciona **Continue** cuando se solicite.
5. Autentícate con GitHub si es la primera vez que se utiliza una herramienta GitHub.
6. Abre la PR creada por Copilot y revisa su contenido. No la combines todavía.

## Resumen y próximos pasos

Has utilizado el servidor MCP de Playwright para probar la funcionalidad en un navegador antes de entregarla. A continuación, [crearás un agente personalizado][next-lesson] para tareas centradas como las revisiones de accesibilidad.

## Recursos

- [¿Qué es MCP y por qué se habla de ello?][mcp-blog-post]
- [Servidor MCP de Microsoft Playwright][playwright-mcp-server]
- [Servidor MCP de GitHub][github-mcp-server]
- [Registro MCP de GitHub][mcp-registry]
- [Servidores MCP en VS Code][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
