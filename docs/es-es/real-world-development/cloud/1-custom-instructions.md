---
title: "Ejercicio 1 - Instrucciones personalizadas (agente en la nube)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Ejercicio anterior: Requisitos previos][previous-lesson] · [Siguiente ejercicio: Agente en la nube de Copilot →][next-lesson]

El contexto es fundamental cuando trabajas con IA generativa. Si una tarea debe realizarse de una manera concreta o hay información de contexto que Copilot debe conocer, debes garantizar que esa información esté disponible. Los [archivos de instrucciones][instruction-files] permiten proporcionar esa orientación, de modo que Copilot entienda no solo *qué* quieres que haga, sino *cómo* quieres que lo haga.

En este ejercicio:

- explorarás cómo el contexto específico del proyecto, las pautas de programación y los estándares de documentación llegan a Copilot mediante instrucciones personalizadas del repositorio y archivos de instrucciones con alcance a rutas;
- añadirás un nuevo estándar aplicable a todo el repositorio en `.github/copilot-instructions.md`.

> [!NOTE]
> A diferencia de los recorridos de VS Code y CLI, aquí no ejecutarás un ejercicio de antes/después. El agente en la nube de Copilot trabaja de forma asincrónica en incidencias de GitHub, por lo que es más difícil demostrar el impacto en tiempo real. Observarás la influencia del archivo de instrucciones más adelante, al revisar las solicitudes de incorporación de cambios que genere el agente en la nube.

## Archivos de instrucciones

### Escenario

Como corresponde a cualquier taller de desarrollo serio, Tailspin Toys tiene pautas y requisitos para las prácticas de desarrollo:

- La capa de datos siempre necesita pruebas unitarias.
- La interfaz debe utilizar un tema oscuro y una apariencia moderna.
- La documentación debe incluirse en el código mediante comentarios TSDoc.
- Cada archivo debe comenzar con un bloque de comentarios que describa su propósito.

Mediante archivos de instrucciones garantizarás que Copilot tenga la información adecuada para realizar las tareas conforme a estas prácticas.

### Instrucciones personalizadas

Las instrucciones personalizadas permiten proporcionar contexto y preferencias a Copilot para que comprenda mejor tu estilo de programación y tus requisitos. Puedes especificar convenciones de código preferidas, bibliotecas e incluso los tipos de comentarios que quieres incluir. Puedes crear instrucciones para todo el repositorio o para tipos de archivos concretos.

Hay dos tipos de archivos de instrucciones:

- `.github/copilot-instructions.md`, un único archivo enviado a Copilot en **todas** las solicitudes del repositorio. Debe contener información del proyecto relevante para la mayoría de las conversaciones o solicitudes de CLI.
- Los archivos `.github/instructions/*.instructions.md`, que se pueden crear para tareas o tipos de archivo concretos. Permiten proporcionar pautas para lenguajes como TypeScript o Astro, o para tareas como crear una interfaz o un conjunto de pruebas unitarias.

> [!NOTE]
> Copilot Chat, Copilot CLI y el agente en la nube de Copilot utilizan tanto las instrucciones del repositorio como los archivos `*.instructions.md` con frontmatter `applyTo` al generar código. También existe compatibilidad con otros formatos, como `AGENTS.md` y `CLAUDE.md`.

## Explorar los archivos de instrucciones personalizadas del proyecto

Este repositorio incluye un archivo principal `.github/copilot-instructions.md` y varios archivos `*.instructions.md` para distintas tareas.

1. Abre `.github/copilot-instructions.md`.
2. Observa la descripción breve del proyecto y secciones como **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**. Bajo **Code standards**, revisa las pautas para flujos de trabajo de GitHub Actions.
3. Abre la carpeta `.github/instructions`. Encontrarás instrucciones para archivos Astro, la capa de datos de Drizzle, las pruebas y otros elementos.
4. Abre `.github/instructions/unit-tests.instructions.md`. Fíjate en `applyTo`: determina qué archivos coinciden con las instrucciones; por ejemplo, `**/*.test.ts`.
5. Abre `.github/instructions/drizzle.instructions.md` y revisa sus enlaces a otros archivos de instrucciones y archivos existentes del proyecto. Esto permite descomponer conjuntos grandes de instrucciones y remitir a Copilot a ejemplos concretos.

> [!NOTE]
> La sección **Code formatting requirements** de `copilot-instructions.md` documenta los estándares de programación del proyecto, pero todavía no exige documentación dentro del código. En los pasos siguientes añadirás reglas para comentarios TSDoc y encabezados de archivo.

## Añadir un nuevo estándar del repositorio

Crearás una regla aplicable a todo el proyecto que exija documentación en el código mediante comentarios TSDoc y un encabezado de comentario al inicio de cada archivo.

1. Desde el terminal del Codespace, crea y cambia a una rama nueva:

   ```bash
   git checkout -b custom-instructions-cloud
   ```

2. Abre `.github/copilot-instructions.md` y localiza la sección **Code formatting requirements**, cerca de la línea 27.
3. Añade las siguientes líneas justo debajo de los estándares existentes:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Guarda `copilot-instructions.md`.

> [!TIP]
> Los archivos de instrucciones del repositorio sirven para las pautas globales. Los archivos `*.instructions.md` sirven para lenguajes, tipos de archivo o tareas concretas. `.github/copilot-instructions.md` es el lugar adecuado para estándares globales como esta regla de documentación.

## Confirmar, enviar y combinar la actualización

El agente en la nube lee los archivos de instrucciones de la rama a la que apunta la incidencia. Cuando asignas una incidencia a Copilot en el siguiente ejercicio, Copilot partirá de `main`, así que los cambios deben llegar a `main`.

1. Prepara y confirma los cambios:

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. Envía la rama:

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. Abre una solicitud de incorporación de cambios desde `custom-instructions-cloud` hacia `main` en github.com y combínala.

> [!TIP]
> Si prefieres trabajar directamente en `main` durante el taller, puedes omitir la rama y confirmar directamente. Este paso en una rama refleja el modo en que actuarías en un proyecto real.

## Resumen y próximos pasos

Has explorado cómo Copilot obtiene contexto de los archivos de instrucciones y has añadido un nuevo estándar aplicable a todo el repositorio en `.github/copilot-instructions.md`. Verás ese estándar aplicado en las solicitudes de incorporación de cambios que genere el agente en la nube durante el resto de este recorrido.

A continuación, [asignarás tu primera incidencia al agente en la nube de Copilot][next-lesson].

## Recursos

- [Archivos de instrucciones para personalizar GitHub Copilot][instruction-files]
- [Procedimientos recomendados para crear instrucciones personalizadas][instructions-best-practices]
- [Cinco consejos para escribir mejores instrucciones personalizadas para Copilot][copilot-instructions-five-tips]
- [Awesome Copilot: una colección de archivos de instrucciones y otros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
[awesome-copilot]: https://github.com/github/awesome-copilot
