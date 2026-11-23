---
title: "Ejercicio 0: Requisitos previos"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Antes de empezar los ejercicios de VS Code, debes preparar el entorno. Crearás tu propia copia del repositorio Tailspin Toys, activarás un [Codespace][codespaces] y confirmarás que GitHub Copilot Chat esté activo en el editor.

## Configurar el repositorio del laboratorio

Para crear una copia del repositorio donde añadirás código, crearás una instancia a partir de la [plantilla][template-repository]. Contendrá todos los archivos necesarios para el laboratorio.

1. En una ventana nueva del navegador, abre la [plantilla de Tailspin Toys][tailspin-template].
2. Crea tu copia seleccionando **Use this template** en la página del repositorio y después **Create a new repository**.

    ![Botón Use this template](../../../_images/ex0-use-template.png)

3. Si realizas el taller como parte de un evento dirigido por GitHub o Microsoft, sigue las instrucciones de los mentores. En caso contrario, crea el repositorio en una organización en la que tengas acceso a GitHub Copilot.

    ![Configuración del repositorio creado a partir de la plantilla](../../../_images/ex0-repository-settings.png)

4. Anota la ruta del repositorio creado (**nombre-de-organización-o-usuario/nombre-del-repositorio**), porque la utilizarás más adelante.

> [!NOTE]
> **Tu backlog ya está preparado**
>
> Cuando creas el repositorio a partir de la plantilla, se genera automáticamente un backlog de incidencias de GitHub. Trabajarás a partir de esas incidencias durante el taller; no necesitas crear ninguna.

## Crear un Codespace

Utilizarás un Codespace para completar los ejercicios.

[GitHub Codespaces][codespaces] es un entorno de desarrollo basado en la nube que permite escribir, ejecutar y depurar código desde el navegador. Incluye un IDE completo con compatibilidad con varios lenguajes, extensiones y herramientas.

1. Ve al repositorio recién creado.
2. Selecciona el botón verde **Code**.

    ![Selecciona el botón Code](../../../_images/ex0-code-button.png)

3. Selecciona la pestaña **Codespaces** y el botón **+** para crear un Codespace nuevo.

    ![Crea un Codespace nuevo](../../../_images/ex0-create-codespace.png)

La creación puede tardar varios minutos, aunque sigue siendo mucho más rápida que instalar manualmente todos los servicios. Puedes aprovechar este tiempo para explorar otras funciones de GitHub Copilot.

> [!CAUTION]
> Volverás al Codespace en otro ejercicio. Por ahora, déjalo abierto en una pestaña del navegador.

> [!NOTE]
> Este taller está preparado para ejecutarse en un Codespace o en un [dev container][dev-containers] local. Ambos garantizan que los requisitos previos estén instalados para ofrecer una experiencia fluida. Si prefieres trabajar localmente, abre el repositorio clonado en VS Code y selecciona **Reopen in Container** cuando se te indique.

## Utilizar GitHub Copilot Chat y el modo agente

Para utilizar el modo agente de GitHub Copilot Chat necesitas tener instalada la extensión GitHub Copilot Chat. Debería estarlo si utilizas un Codespace de GitHub.

> [!TIP]
> Si no tienes instalada la extensión GitHub Copilot Chat, puedes [instalarla desde Visual Studio Code Marketplace][copilot-chat-extension]. También puedes abrir la vista **Extensions**, buscar **GitHub Copilot Chat** y seleccionar **Install**.

Después de instalarla, puede que tengas que autenticarte con tu cuenta de GitHub.

1. Vuelve a tu Codespace.
2. Si no ves Copilot Chat a la derecha del editor, selecciona el icono **Copilot Chat** en la parte superior.
3. Escribe un mensaje como «Hello world» en la ventana de Copilot Chat y pulsa <kbd>Enter</kbd>.
4. Si no estás autenticado, sigue las instrucciones para iniciar sesión en tu cuenta de GitHub.

    ![Ejemplo de solicitud de autenticación de Copilot Chat](../../../_images/ex1-copilot-authentication.png)

5. Después de autenticarte, debería aparecer la ventana de Copilot Chat.

## Resumen

¡Enhorabuena! Has creado una copia del repositorio del laboratorio y comenzado la creación de tu Codespace, que utilizarás para escribir código.

## Próximo paso

Vamos a poner a trabajar a Copilot. Continúa con el [Ejercicio 1 - Instrucciones personalizadas][next-lesson], donde enseñarás a Copilot las convenciones del proyecto.

## Recursos

- [Información general sobre GitHub Codespaces][codespaces]
- [Crear un repositorio a partir de una plantilla][template-repository]
- [Primeros pasos con Codespaces][codespaces-quickstart]

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers
[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[copilot-chat-extension]: https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat
[next-lesson]: ../1-custom-instructions/
