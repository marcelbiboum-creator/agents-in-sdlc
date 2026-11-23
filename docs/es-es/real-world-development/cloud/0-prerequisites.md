---
title: "Ejercicio 0: Requisitos previos"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Antes de comenzar los ejercicios del agente en la nube de Copilot, debes preparar el entorno. Crearás tu propia copia del repositorio Tailspin Toys y activarás un [Codespace][codespaces] desde el que editarás archivos de instrucciones y revisarás el trabajo realizado por el agente en la nube.

## Configurar el repositorio del laboratorio

Para crear una copia del repositorio que contendrá el código que utilizarás, crearás una instancia a partir de la [plantilla][template-repository]. La nueva instancia contendrá todos los archivos necesarios y la utilizarás durante los ejercicios.

1. En una ventana nueva del navegador, abre la [plantilla de Tailspin Toys][tailspin-template].
2. Crea tu propia copia del repositorio seleccionando **Use this template** en la página del repositorio del laboratorio y, después, **Create a new repository**.

    ![Botón Use this template](../../../_images/ex0-use-template.png)

3. Si realizas el taller como parte de un evento dirigido por GitHub o Microsoft, sigue las instrucciones de tus mentores. En caso contrario, crea el nuevo repositorio en una organización en la que tengas acceso a GitHub Copilot.

    ![Configuración del repositorio creado a partir de la plantilla](../../../_images/ex0-repository-settings.png)

4. Anota la ruta del repositorio que creaste (**nombre-de-organización-o-usuario/nombre-del-repositorio**), porque la necesitarás más adelante.

## Crear un Codespace

Ahora utilizarás un Codespace para completar los ejercicios.

[GitHub Codespaces][codespaces] es un entorno de desarrollo basado en la nube que permite escribir, ejecutar y depurar código directamente desde el navegador. Proporciona un IDE completo con compatibilidad para varios lenguajes de programación, extensiones y herramientas.

1. Ve al repositorio recién creado.
2. Selecciona el botón verde **Code**.

    ![Selecciona el botón Code](../../../_images/ex0-code-button.png)

3. Selecciona la pestaña **Codespaces** y, después, el botón **+** para crear un Codespace nuevo.

    ![Crea un Codespace nuevo](../../../_images/ex0-create-codespace.png)

La creación del Codespace tardará varios minutos, aunque sigue siendo mucho más rápido que instalar manualmente todos los servicios. Aprovecha ese tiempo para explorar otras funciones de GitHub Copilot.

> [!CAUTION]
> Volverás al Codespace en un ejercicio futuro. Por ahora, déjalo abierto en una pestaña del navegador.

> [!NOTE]
> Este taller está diseñado para ejecutarse dentro de un Codespace o de un [dev container][dev-containers] local. Ambos garantizan que el entorno tenga todos los requisitos previos instalados para ofrecer una experiencia fluida. Si prefieres ejecutarlo localmente, abre el repositorio clonado en VS Code y selecciona **Reopen in Container** cuando se te indique; VS Code creará el mismo dev container que utiliza el Codespace.

## Resumen

¡Enhorabuena! Has creado una copia del repositorio del laboratorio y iniciado el proceso de creación de tu Codespace, que utilizarás mientras trabajas junto al agente en la nube de Copilot.

## Próximo paso

Vamos a añadir instrucciones personalizadas que seguirá el agente en la nube. Continúa con el [Ejercicio 1 - Instrucciones personalizadas][next-lesson].

## Recursos

- [Información general sobre GitHub Codespaces][codespaces]
- [Crear un repositorio a partir de una plantilla][template-repository]
- [Primeros pasos con Codespaces][codespaces-quickstart]

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers
[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-custom-instructions/
