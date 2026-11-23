---
title: "Lección 4 - Orientar a Copilot con instrucciones personalizadas"
description: "Explora las instrucciones del repositorio, añade un estándar de documentación y aplícalo al código del filtrado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

El contexto es clave cuando trabajas con IA generativa. Si una tarea debe realizarse de una manera concreta, quieres que esa orientación esté disponible para Copilot. Los [archivos de instrucciones][instruction-files] describen no solo *qué* código quieres, sino *cómo* debe estructurarse. Ahora que has creado el filtrado, explorarás las instrucciones que utilizó Copilot, añadirás un estándar de documentación y lo aplicarás a tu código.

En esta lección:

- explorarás cómo las instrucciones del repositorio y los archivos de instrucciones con alcance a rutas llegan al agente;
- actualizarás el archivo de instrucciones para garantizar que se sigan los estándares de programación;
- verás el impacto de los archivos de instrucciones en el código.

## Escenario

Como en cualquier buen taller de desarrollo, Tailspin Toys tiene pautas y requisitos para las prácticas de desarrollo. Estos incluyen:

- Los comentarios deben explicar la intención y las decisiones no evidentes, en lugar de repetir el código.
- Las funciones exportadas en `db/` y `src/lib/` deben documentar su propósito, sus parámetros y sus valores de retorno con TSDoc/JSDoc, incluido un argumento `db` inyectable cuando exista.
- Los componentes reutilizables de Astro deben documentar sus contratos de `Props`, y los comentarios deben mantenerse actualizados cuando cambie el código relacionado.
- Deben conservarse las pautas existentes de formato y lint.

Mediante los archivos de instrucciones, garantizarás que Copilot tenga la información adecuada para realizar las tareas conforme a las prácticas destacadas.

## Archivos de instrucciones

Las instrucciones personalizadas permiten proporcionar contexto y preferencias a Copilot, de manera que pueda comprender mejor tu estilo de programación y tus requisitos. Esta función puede ayudarte a orientar a Copilot para obtener sugerencias y fragmentos de código más relevantes. Puedes especificar tus convenciones de programación preferidas, las bibliotecas e incluso los tipos de comentarios que quieras incluir en el código. Puedes crear instrucciones para todo el repositorio o para tipos de archivos concretos.

Hay dos tipos de archivos de instrucciones:

- `.github/copilot-instructions.md`, un único archivo de instrucciones que se envía a Copilot en **todas** las solicitudes del repositorio. Debe contener información de nivel de proyecto relevante para la mayoría de las solicitudes.
- Los archivos `.github/instructions/*.instructions.md`, que proporcionan pautas para lenguajes, tipos de archivo o tareas concretas.

> [!NOTE]
> Otros formatos de instrucciones y su compatibilidad varían según el entorno. Consulta la [referencia de compatibilidad de instrucciones personalizadas][custom-instructions-support] antes de basarte en un formato concreto.

## Explorar los archivos de instrucciones personalizadas de este proyecto

Para empezar, el proyecto base ya incluye varios archivos de instrucciones. Vamos a explorar lo que ya existe antes de realizar un cambio y observar su impacto.

1. Vuelve a tu Codespace.
2. En el editor de Codespaces, no en el terminal, abre `.github/copilot-instructions.md`.
3. Explora el archivo y observa la descripción breve del proyecto y sus pautas de programación. Estas instrucciones se aplican a todas las interacciones con Copilot en este repositorio.
4. Abre la carpeta `.github/instructions` y explora los archivos. Observa que existen instrucciones para archivos Astro, la capa de datos de Drizzle, las pruebas y mucho más.
5. Abre `.github/instructions/unit-tests.instructions.md`. Fíjate en el campo `applyTo` de la parte superior; establece un patrón global que determina a qué archivos se aplican las instrucciones.
6. Abre `.github/instructions/drizzle.instructions.md` y observa sus enlaces a otros archivos de instrucciones y a archivos existentes del proyecto. Esto permite dividir conjuntos de instrucciones grandes en archivos reutilizables más pequeños y señalar a Copilot los ejemplos que debe seguir.

## Actualizar los archivos de instrucciones para adaptarlos a las pautas del equipo

Los archivos existentes son un buen comienzo, pero todavía queda una brecha. Modifiquemos el archivo principal `copilot-instructions.md` para garantizar que el TypeScript recién generado incluya comentarios TSDoc.

1. En `.github/copilot-instructions.md`, busca la sección titulada **Code formatting guidance**, que debería encontrarse alrededor de la línea 35.
2. Añade lo siguiente como último elemento:

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

El archivo se guardará automáticamente.

## Utilizar la orientación actualizada

Copilot CLI carga las instrucciones del repositorio al iniciar una conversación. Después de guardar las instrucciones actualizadas, sal de la conversación de filtrado y reanúdala para que Copilot comience con la nueva orientación sin perder el contexto de la funcionalidad.

1. Si la conversación de filtrado sigue abierta, introduce `/exit` para cerrarla. Copilot CLI guarda las conversaciones automáticamente.
2. Desde la raíz del repositorio y en la rama `game-filters-cli`, reanuda la conversación guardada:

   ```bash
   copilot --resume
   ```

   Si se te solicita, selecciona la conversación de filtrado y confirma que tienes activa la rama `game-filters-cli`.
3. Pide a Copilot que aplique la orientación actualizada:

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. Introduce `/diff` y lee los archivos TypeScript modificados. Observa los nuevos comentarios TSDoc y confirma que explican el código con precisión.

## Resumen y próximos pasos

Has explorado cómo Copilot CLI obtiene contexto de los archivos de instrucciones y has aplicado un nuevo estándar a tu funcionalidad. Concretamente:

- has explorado cómo las instrucciones del repositorio y los archivos de instrucciones con alcance a rutas llegan al agente;
- has actualizado el archivo de instrucciones para garantizar que se sigan los estándares de programación;
- has observado el impacto de los archivos de instrucciones en el código.

A continuación, [personalizarás y ejecutarás la habilidad reutilizable quality-checks][next-lesson] para garantizar que el lint y las pruebas se ejecuten de forma coherente.

## Recursos

- [Añadir instrucciones personalizadas para Copilot CLI][instruction-files]
- [Compatibilidad de instrucciones personalizadas][custom-instructions-support]
- [Procedimientos recomendados para crear instrucciones personalizadas][instructions-best-practices]
- [Awesome Copilot: una colección de archivos de instrucciones y otros recursos][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
