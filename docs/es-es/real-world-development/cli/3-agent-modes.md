---
title: "Lección 3 - Modos de agente: Plan y Autopilot"
description: "Utiliza Plan para acordar un enfoque, Autopilot para crear el filtrado a partir de una incidencia e Interactive para revisar el resultado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Empezamos añadiendo una funcionalidad pequeña al proyecto. Sin embargo, los cambios mayores requieren un proceso más sólido. Por suerte, GitHub Copilot CLI está diseñado para integrarse en el flujo existente de una organización y garantizar que construimos las cosas correctas de la manera adecuada. Esta es la primera de varias lecciones en las que seguirás un proceso típico de desarrollo dirigido por agentes: partirás de una incidencia para generar una nueva funcionalidad, comprobarás que el código sea válido, confirmarás que la funcionalidad se comporta como se espera y, finalmente, la combinarás correctamente en el proyecto.

> [!NOTE]
> Utilizarás la misma conversación y rama mientras continúas con el flujo de la funcionalidad. Normalmente tendrías ramas o PR diferentes para los distintos tipos de archivo con los que trabajarías, pero aquí utilizaremos un atajo para centrarnos en los conceptos principales.

Para empezar, en esta lección:

- iniciarás una conversación nueva de Copilot desde una incidencia de GitHub;
- definirás los requisitos en modo Plan;
- implementarás la nueva funcionalidad con el modo Autopilot;
- revisarás el código;
- validarás la funcionalidad manualmente en un navegador reenviado.

Durante esta funcionalidad, actualizarás las instrucciones del repositorio, personalizarás la habilidad existente `quality-checks`, añadirás validación MCP, crearás un agente de QA y abrirás la PR de la funcionalidad.

## Escenario

El catálogo de Tailspin Toys está creciendo y los visitantes necesitan limitar los juegos por categoría y editor. La incidencia del backlog describe la funcionalidad, pero los detalles, como la combinación de categorías, requieren acuerdo antes de programar. Utilizarás el modo Plan para resolver esas decisiones y, después, autorizarás una implementación acotada con Autopilot.

## Contexto

Introducir agentes de programación con IA en el flujo de desarrollo no cambia los principios fundamentales. ¡De hecho, los hace aún más importantes! La mayoría de los desarrolladores siguen un flujo similar a este:

1. Partir de una incidencia registrada que describa lo que hay que hacer.
2. Crear un plan con lo que debe desarrollarse.
3. Crear y revisar el código.
4. Ejecutar las pruebas para validar el código.
5. Validar manualmente la nueva funcionalidad.
6. Crear una solicitud de incorporación de cambios (PR).
7. Cuando el código haya sido revisado y el proceso de integración continua haya finalizado correctamente, combinarlo.

> [!NOTE]
> Los detalles exactos variarán según tu equipo y organización, pero la mayoría será una variante del flujo anterior.

Al mantener este enfoque estándar, garantizas que el código generado por IA cumpla los requisitos establecidos y pase por el mismo proceso de validación que el código escrito a mano.

## Modos de conversación

El **modo de conversación** controla cuánta autonomía tiene el agente. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para recorrer los modos:

- **Interactive**: tú y el agente trabajáis juntos. El agente propone cambios y espera tu indicación antes de continuar.
- **Plan**: el agente crea primero un plan y no puede editar archivos del proyecto.
- **Autopilot**: el agente trabaja de forma autónoma: escribe código, ejecuta pruebas e itera hasta completar la tarea.

Empieza en modo Plan, revisa el plan y utiliza Autopilot para implementarlo.

## Partir de la incidencia

Antes de comenzar el trabajo de filtrado, vuelve a tu Codespace y asegúrate de que el repositorio y el terminal estén preparados.

1. Vuelve a tu Codespace. Si está detenido, reinícialo antes de continuar.
2. Confirma que la PR de la valoración por estrellas está combinada.
3. Si el terminal no está abierto, pulsa <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
4. Actualiza `main` y crea una rama para el trabajo de filtrado:

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Inicia Copilot CLI:

   ```bash
   copilot --yolo
   ```

6. Pulsa <kbd>Tab</kbd> dos veces para abrir la pestaña **Issues**.
7. Pulsa <kbd>A</kbd> para mostrar todas las incidencias.
8. Utiliza las teclas de dirección para resaltar la incidencia titulada **Allow users to filter games by category and publisher**.
9. Pulsa <kbd>C</kbd> para añadir la incidencia a la indicación y volver a la pestaña **Session**.

Observa que la indicación ahora empieza por `#7` (o un número parecido). El carácter `#` permite incorporar una incidencia o solicitud de incorporación de cambios (PR) de GitHub al contexto.

## Planificar la funcionalidad de filtrado

La planificación te permite acordar el enfoque que se seguirá para implementar una funcionalidad o realizar tareas antes de entregarlas a Copilot. Siempre es una buena idea dedicar algo de tiempo a planificar cuando el trabajo es complejo. Cambiaremos a modo Plan y pediremos a Copilot que cree el plan.

1. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para cambiar a modo Plan. Confirma que el indicador de modo situado debajo de la indicación muestra **Plan**.
2. Después de la referencia a la incidencia añadida en el paso anterior, introduce esta indicación:

   ```plaintext
   Create a plan for implementing this feature.
   ```

Copilot empezará a crear el plan. Primero explorará el proyecto y, después, determinará el mejor enfoque.

3. Durante el proceso, Copilot puede hacer preguntas sobre cómo deben funcionar las capacidades de filtrado. Respóndelas según tus preferencias. ¡Aquí no hay respuestas incorrectas!
4. Cuando el plan esté completo, pulsa <kbd>Control</kbd>+<kbd>E</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) para expandirlo.
5. Desplázate hacia arriba y hacia abajo para revisar el plan.
6. Pide a Copilot que revise cualquier parte del plan que no coincida con tus decisiones.

## Aprobar Autopilot

Con el plan escrito y revisado, es el momento de implementarlo. Vamos a dejar que Copilot haga su trabajo mediante Autopilot.

Autopilot permitirá a Copilot iterar sobre el problema hasta que considere que está resuelto.

1. Selecciona **Accept plan and build on autopilot (recommended)** o la opción con una etiqueta similar en tu versión instalada.
2. Confirma que el indicador de modo situado debajo de la indicación muestra **Autopilot**.
3. Observa cómo Copilot itera sobre el plan establecido, genera código y ejecuta pruebas.

> [!NOTE]
> La aprobación puede iniciar la implementación de inmediato, así que revisa el plan primero. Si Copilot informa de dependencias ausentes o de un conflicto de puerto, resuelve el problema de configuración antes de dar las comprobaciones por completadas.

## Revisar y verificar la implementación

Cuando el código esté generado, debe revisarse antes de combinarse, igual que cualquier otro código. Vamos a revisar el código y ejecutar el sitio para asegurarnos de que todo funciona correctamente.

1. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para entrar en modo Interactive. Confirma que el indicador ya no muestra **Plan** ni **Autopilot**.
2. Introduce `/diff` e inspecciona la implementación del filtrado y las pruebas.
3. Compara el resultado con la incidencia y las decisiones tomadas durante la planificación.
4. Cuando hayas revisado el código, pulsa <kbd>Esc</kbd> para salir de la vista de diferencias.
5. Revisa la salida de las comprobaciones del proyecto y pide a Copilot que resuelva cualquier fallo.

## Explorar la nueva funcionalidad

El código parece correcto, pero ¿funciona? Vamos a iniciar la aplicación como antes y abrir el sitio mediante el puerto reenviado de Codespaces.

1. Pide a Copilot que inicie la aplicación:

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. Cuando Codespaces indique que el puerto `4321` está disponible, selecciona **Open in Browser**.
3. Prueba el filtrado por categoría, el filtrado por editor y las combinaciones acordadas en el plan.
4. Confirma que el comportamiento de restablecimiento y de resultados vacíos coincide con la incidencia y tus decisiones.
5. Vuelve a tu Codespace y pide a Copilot que detenga el servidor de desarrollo iniciado.

## Resumen y próximos pasos

Has utilizado distintos modos de conversación para crear y revisar una funcionalidad. En esta lección:

- has iniciado una conversación nueva de Copilot desde una incidencia de GitHub;
- has definido los requisitos en modo Plan;
- has implementado la nueva funcionalidad con el modo Autopilot;
- has revisado el código;
- has validado manualmente la funcionalidad en un navegador reenviado.

A continuación, profundizaremos un poco más en cómo se genera el código y nos aseguraremos de que siga las prácticas documentadas mediante el [uso de instrucciones personalizadas][next-lesson].

## Recursos

- [Autopilot en GitHub Copilot CLI][autopilot]
- [Referencia de comandos de Copilot CLI][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
