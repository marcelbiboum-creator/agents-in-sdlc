---
title: "Lección 1 - Instalar GitHub Copilot CLI"
description: "Instala y autentica Copilot CLI en el Codespace, conoce el entorno y encuentra la incidencia de filtrado incluida."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

[GitHub Copilot CLI][about-copilot-cli] es un potente asistente de programación basado en agentes que se ejecuta en el terminal. Te permite explorar bases de código, generar código, ejecutar comandos e interactuar con herramientas externas desde la línea de comandos. También permite delegar tareas, solicitar cambios y mantener el flujo de trabajo. El primer paso, como cabe esperar, es instalar la herramienta.

En esta lección:

- instalarás GitHub Copilot CLI con npm;
- te autenticarás con tu cuenta de GitHub;
- confiarás en el repositorio del taller y probarás una conversación rápida;
- encontrarás la incidencia de filtrado mediante el servidor MCP integrado de GitHub.

## Escenario

Tu equipo empieza a utilizar agentes de IA para gestionar un backlog en crecimiento. Copilot CLI lleva esa capacidad al terminal, donde muchos desarrolladores ya trabajan. Esta lección te permitirá instalarlo, autenticarte y dejarlo listo para el resto del taller.

## Instalar Copilot CLI

Puedes instalar Copilot CLI mediante [npm][install-cli], WinGet y Homebrew. Como GitHub Codespaces incluye Node.js, utilizarás npm.

1. Vuelve a tu Codespace y abre una terminal.
2. Comprueba que Node.js está instalado y cumple el requisito de versión:

   ```bash
   node --version
   ```

   Deberías ver la versión 24 o posterior.

3. Instala Copilot CLI globalmente:

   ```bash
   npm install -g @github/copilot
   ```

4. Comprueba la instalación:

   ```bash
   copilot --version
   ```

   Debería aparecer el número de versión.

## Autenticarse con GitHub

En el primer inicio, Copilot CLI te solicitará autenticarte con tu cuenta de GitHub.

1. Inicia Copilot CLI:

   ```bash
   copilot
   ```

2. Si se solicita, sigue las instrucciones del código de dispositivo para autenticarte y autorizar Copilot CLI.
3. Copilot CLI muestra la siguiente indicación:

   ```plaintext
   Copilot can read files in this folder and, with your permission, edit them or run code and shell commands. It will remember your permissions for the rest of this session.

   Do you trust the files in this folder?
   ```

4. Comprueba que la ruta corresponde al repositorio Tailspin Toys y responde que sí seleccionando **Yes, and remember this folder for future sessions**.

> [!NOTE]
> En un Codespace, es posible que ya estés autenticado mediante tu sesión de GitHub. Si Copilot CLI se inicia sin solicitar autenticación, puedes continuar.

## Orientarte

Los comandos escritos en el aviso normal del terminal se ejecutan directamente en el Codespace. Cuando Copilot CLI se inicia, el lenguaje natural se envía al agente y los comandos de barra controlan la conversación.

1. Introduce `/model`, utiliza las teclas de dirección para seleccionar **Auto**, pulsa <kbd>Enter</kbd> y pulsa <kbd>Enter</kbd> de nuevo para confirmar.
2. Introduce `/help` para ver los comandos disponibles en tu versión instalada y pulsa <kbd>Esc</kbd> para cerrar la ayuda.
3. Pregunta a Copilot una cuestión sencilla para comprobar que todo funciona:

   ```plaintext
   What are the key files in this project?
   ```

4. Lee la respuesta y observa cómo Copilot explora el repositorio antes de contestar.
5. Introduce `/mcp list` y confirma que el servidor MCP integrado de GitHub está disponible.
6. Pide a Copilot que encuentre la incidencia de filtrado:

   ```plaintext
   Using GitHub MCP, find the issue in this repository titled "Allow users to filter games by category and publisher." Give me its URL and a short summary. Don't change anything.
   ```

7. Abre la URL y lee la incidencia. La utilizarás después de realizar un primer cambio rápido.

> [!TIP]
> Una sesión normal de Copilot CLI trabaja en la rama que tengas activa en el terminal; no crea automáticamente un árbol de trabajo. Crearás una rama de funcionalidad antes de cada cambio.

## Utilizar el atajo del taller

Copilot CLI normalmente pide permiso antes de utilizar herramientas fuera de sus permisos establecidos. Para este taller, lo volverás a iniciar con `--yolo`, un atajo aprobado por el usuario que elimina esos avisos dentro del Codespace para que puedas centrarte en los ejercicios.

> [!CAUTION]
> `--yolo` habilita permisos automáticos completos (`--allow-all-tools`, `--allow-all-paths` y `--allow-all-urls`). Utilízalo únicamente en un entorno aislado, como un Codespace o una máquina virtual, y nunca lo establezcas como opción predeterminada para el desarrollo diario. Consulta [Permitir o denegar el uso de herramientas][allow-all-warning] para obtener más información.

Para este taller, `--enable-all-github-mcp-tools` activa las herramientas de lectura y escritura de GitHub MCP que utilizarán las lecciones posteriores para trabajar con incidencias y solicitudes de incorporación de cambios. El Codespace limita el acceso a tu equipo local, pero los recursos autenticados de GitHub siguen siendo reales. Revisa los cambios antes de publicarlos o combinarlos.

1. Sal de Copilot CLI con `/exit`.
2. Vuelve a iniciarlo desde la raíz del repositorio:

   ```bash
   copilot --yolo --enable-all-github-mcp-tools
   ```

3. Haz otra pregunta rápida sobre el proyecto para confirmar que la conversación funciona y, después, sal con `/exit`.

Copilot guarda las conversaciones automáticamente. Más adelante, después de cambiar las instrucciones o añadir un agente, utilizarás `copilot --resume` para volver a la misma conversación de funcionalidad y a su rama.

## Resumen y próximos pasos

¡Enhorabuena! En esta lección:

- has instalado GitHub Copilot CLI con npm;
- te has autenticado con tu cuenta de GitHub;
- has confiado en el repositorio del taller y probado una conversación rápida;
- has encontrado la incidencia de filtrado mediante el servidor MCP integrado de GitHub.

A continuación, [iniciarás tu primer cambio centrado][next-lesson] y utilizarás Copilot CLI para mostrar una valoración por estrellas en las tarjetas de juegos.

## Recursos

- [Instalar GitHub Copilot CLI][install-cli]
- [Acerca de GitHub Copilot CLI][about-copilot-cli]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-add-star-rating/
[install-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/set-up-copilot-cli/install-copilot-cli
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[allow-all-warning]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli#allowing-and-denying-tool-use
