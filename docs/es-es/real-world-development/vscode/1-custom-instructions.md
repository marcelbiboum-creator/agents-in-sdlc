---
title: "Ejercicio 1 - Instrucciones personalizadas (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Ejercicio anterior: Requisitos previos][previous-lesson] · [Siguiente ejercicio: Modo agente →][next-lesson]

El contexto es fundamental al trabajar con IA generativa. Si una tarea debe realizarse de cierta manera o hay información de contexto que Copilot debe conocer, esa orientación debe ser accesible. Una de las formas principales es utilizar [archivos de instrucciones][instruction-files].

En este ejercicio:

- explorarás cómo llegan a Copilot el contexto del proyecto, las pautas de programación y los estándares de documentación;
- generarás el primer fragmento de datos para el filtrado con las instrucciones actuales;
- añadirás un nuevo estándar aplicable a todo el repositorio;
- volverás a ejecutar la misma indicación y observarás cómo cambia el código;
- confirmarás las instrucciones y el filtrado en `main`.

> [!CAUTION]
> El código generado puede diferir de los estándares definidos. Copilot no es determinista. La finalidad es observar la tendencia después de actualizar las instrucciones, no obtener una salida idéntica carácter a carácter.

## Archivos de instrucciones

Como corresponde a un taller de desarrollo, Tailspin Toys tiene una serie de pautas:

- La capa de datos siempre necesita pruebas unitarias.
- La interfaz debe tener un tema oscuro y una apariencia moderna.
- La documentación debe añadirse al código mediante comentarios TSDoc.
- Cada archivo debe comenzar con un bloque de comentarios que describa su propósito.

Los archivos de instrucciones permiten que Copilot comprenda tanto *qué* quieres crear como *cómo* debe hacerse.

Hay dos tipos:

- `.github/copilot-instructions.md`, enviado a Copilot en todas las solicitudes del repositorio.
- `.github/instructions/*.instructions.md`, creado para tareas o tipos de archivo concretos.

> [!NOTE]
> Los archivos de instrucciones se utilizan para la generación de código en Copilot Chat, no para las sugerencias de autocompletado. Copilot Chat, Copilot CLI y el agente en la nube utilizan instrucciones del repositorio y archivos `*.instructions.md` con frontmatter `applyTo`.

## Explorar los archivos de instrucciones del proyecto

1. Abre `.github/copilot-instructions.md`.
2. Observa su descripción del proyecto y las secciones **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**.
3. Abre `.github/instructions` y revisa las instrucciones para Astro, Drizzle, las pruebas y otros elementos.
4. Abre `.github/instructions/unit-tests.instructions.md` y observa el campo `applyTo`, por ejemplo `**/*.test.ts`.
5. Abre `.github/instructions/drizzle.instructions.md` y revisa sus enlaces a otros archivos y a ejemplos existentes.

## Crear una rama

1. Vuelve al Codespace del ejercicio anterior.
2. Abre una terminal con <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Crea y cambia a una rama nueva:

   ```bash
   git checkout -b custom-instructions
   ```

## Utilizar Copilot Chat antes de actualizar las instrucciones

> [!TIP]
> Abre Copilot Chat, inicia un chat nuevo y selecciona el modo que corresponde a cada paso.

1. Cierra las pestañas que no necesites para que Copilot use únicamente el contexto adecuado.
2. Abre `src/lib/publishers.ts`.
3. Selecciona **Agent** en el selector de agentes.
4. Envía:

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot explorará el proyecto y aplicará cambios en el ayudante y sus pruebas.
6. Observa que el ayudante propuesto es una función tipada que recibe un cliente `db` como primer argumento y devuelve un array tipado de editores. Esto procede de las convenciones de Drizzle.
7. Observa que el código propuesto no incluye comentarios TSDoc ni un encabezado de archivo.

> [!CAUTION]
> Como Copilot es probabilista, podría añadir comentarios incluso sin recibir esa instrucción. En ese caso, lo importante sigue siendo comprobar que el estándar sea coherente después de actualizar las instrucciones.

## Añadir un nuevo estándar del repositorio

1. Abre `.github/copilot-instructions.md`.
2. Localiza **Code formatting requirements**, cerca de la línea 27.
3. Añade:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Guarda el archivo.

> [!TIP]
> Las instrucciones del repositorio son adecuadas para estándares globales como esta regla. Los archivos `*.instructions.md` son apropiados para lenguajes, tipos de archivo o tareas concretas.

## Volver a ejecutar la indicación

1. Inicia un chat nuevo en Copilot Chat.
2. Vuelve a abrir `src/lib/publishers.ts`.
3. Envía exactamente la misma indicación:

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. Observa que el archivo propuesto comienza con un bloque de comentarios similar a:

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. Observa que la función incluye ahora un comentario TSDoc similar a:

   ```typescript
   /**
    * Returns a list of all publishers with their id and name.
    *
    * @param db - The Drizzle database client.
    * @returns A promise that resolves to an array of publisher objects.
    */
   ```

## Confirmar las instrucciones y enviar la rama

1. Abre una terminal y confirma el estado:

   ```bash
   git status
   ```

2. Prepara y confirma las instrucciones y todos los archivos modificados para el ayudante:

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

3. Si las pruebas generan archivos de apoyo adicionales, añade también esos archivos.
4. Envía la rama:

   ```bash
   git push -u origin custom-instructions
   ```

## Crear y combinar una solicitud de incorporación de cambios

Puedes pedir a Copilot que encuentre la incidencia relacionada, cree una PR desde la rama actual y la combine.

1. Abre Copilot Chat y pulsa <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux).
2. Selecciona **Agent** y pide:

   ```text
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

3. Revisa y permite las acciones de GitHub cuando VS Code lo solicite.
4. Cuando se haya creado la PR, pide a Copilot que la combine y vuelva a `main` localmente:

   ```text
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

## Resumen y próximos pasos

Has explorado cómo Copilot obtiene contexto de los archivos de instrucciones y utilizado Copilot Chat en VS Code para:

- enviar una indicación de generación de código y observar el resultado con las instrucciones existentes;
- añadir un nuevo estándar aplicable a todo el repositorio;
- volver a ejecutar la misma indicación y observar el cambio;
- confirmar las instrucciones y la base del ayudante.

A continuación, pondrás esas instrucciones en práctica en el [modo agente][next-lesson] mientras Copilot añade una funcionalidad en el código.

## Recursos

- [Archivos de instrucciones para personalizar GitHub Copilot][instruction-files]
- [Procedimientos recomendados para crear instrucciones personalizadas][instructions-best-practices]
- [Cinco consejos para escribir mejores instrucciones personalizadas][copilot-instructions-five-tips]
- [Instrucciones personalizadas para GitHub Copilot][personal-instructions]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
