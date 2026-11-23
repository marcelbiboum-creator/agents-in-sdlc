---
title: "Ejercicio 2 - Añadir nuevas funcionalidades con el modo agente de Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Incluso las actualizaciones más sencillas pueden afectar a varios archivos y requerir ejecutar pruebas. Como desarrollador, debes localizar los archivos necesarios, realizar los cambios, ejecutar las pruebas, depurar, detectar el archivo que faltaba y volver a actualizar. El modo agente de Copilot está diseñado para actuar de forma más autónoma en el IDE: explora la estructura del proyecto, realiza las actualizaciones necesarias, ejecuta tareas como las pruebas y corrige automáticamente los errores encontrados.

> [!NOTE]
> El modo agente y el agente en la nube ofrecen experiencias distintas. El modo agente realiza el trabajo en el IDE y permite ciclos rápidos de retroalimentación e interacción. El agente en la nube actúa de forma asincrónica como un miembro del equipo y se comunica mediante incidencias y solicitudes de incorporación de cambios.

En este ejercicio aprenderás cómo:

- el modo agente puede explorar el proyecto, identificar archivos relevantes y realizar cambios coordinados;
- Copilot puede implementar nuevas funcionalidades en la interfaz y la capa de datos;
- revisar los cambios y las pruebas generados antes de combinarlos.

## Escenario

A medida que crece el catálogo de juegos, quieres permitir filtrar por categoría y editor. Ya has añadido un ayudante para editores en el ejercicio anterior; ahora completarás el resto de la capa de datos, la interfaz y las pruebas con el modo agente.

## Ejecutar el sitio web de Tailspin Toys

El sitio es una plataforma de financiación colectiva de juegos de mesa con temática de desarrollo. Permite listar juegos y mostrar sus detalles. Es una única aplicación Astro que genera HTML estático durante la compilación. Las páginas consultan directamente una base de datos SQLite local desde su frontmatter mediante Drizzle ORM; no existe una API de backend separada ni un framework de interfaz cliente. Los ayudantes reutilizables de acceso a datos están en `src/lib/`, y la interactividad se añade mediante un pequeño bloque `<script>` de Astro con APIs estándar del DOM.

1. Vuelve a tu Codespace. Después del ejercicio anterior deberías estar en `main`.
2. Abre una terminal con <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Crea una rama nueva:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Inicia el sitio:

   ```bash
   npm run dev
   ```

5. Cuando el servidor indique que está preparado, abre `http://localhost:4321`. En un Codespace, la URL local se reenviará automáticamente a `https://<nombre-del-codespace>-4321.app.github.dev/`.

> [!NOTE]
> Si se abre un cuadro de diálogo para abrir el navegador, ciérralo seleccionando la **x**.

### Explorar el sitio

Las funciones principales son:

- **Página principal**: muestra una lista de juegos de mesa con títulos, imágenes y descripciones.
- **Página de detalles**: al seleccionar un juego, muestra su título, descripción, editor y categoría.

## Explorar el backlog con Copilot

> [!TIP]
> Abre Copilot Chat y selecciona **New Chat** para iniciar una conversación limpia.

1. Selecciona **Agent** en el desplegable de agentes. El agente puede planificar e implementar cambios en varios archivos, ejecutar comandos y utilizar herramientas.

   ![Ejemplo del selector de agentes en la vista de Chat](../../../_images/shared-chat-mode-selector.png)

2. Selecciona `Claude Sonnet 4.5` entre los modelos disponibles.

> [!CAUTION]
> Los autores no indican una preferencia por un modelo concreto. Este taller utilizó Claude Sonnet 4.5 para conseguir una experiencia relativamente coherente, pero los modelos de IA son probabilistas y las sugerencias pueden diferir.

3. Pide a Copilot que muestre el backlog:

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. Selecciona **Continue** para ejecutar el comando y mostrar las incidencias.
5. Revisa la lista generada. Observa cómo Copilot puede priorizar los elementos según su utilidad.

## Revisar los archivos de instrucciones

Antes de iniciar al agente, revisa las instrucciones que proporcionarán contexto.

1. En tu Codespace, abre `.github/instructions/ui.instructions.md`.
2. Observa las pautas sobre arquitectura, diseño de componentes, pruebas, accesibilidad y enlaces a instrucciones específicas para Astro, Tailwind CSS y Drizzle.

> [!TIP]
> Los archivos de instrucciones pueden enlazar a otros archivos de instrucciones y a archivos del proyecto mediante rutas relativas. Esto permite reutilizar contenido y dividir conjuntos complejos en partes manejables.

## Implementar el filtrado

Para completar el filtrado serán necesarios al menos tres tipos de cambios:

- añadir o perfeccionar la lógica de filtrado en la capa de datos (`src/lib/`);
- añadir o actualizar las pruebas del comportamiento del filtrado;
- actualizar la página de juegos con la interfaz de filtrado.

Todas las pruebas deben ejecutarse y pasar antes de combinar los cambios.

1. Continua en la conversación actual o inicia un chat nuevo.
2. Selecciona **Add Context**, **Instructions** y el archivo `ui`.
3. Confirma que **Agent** sigue seleccionado.
4. Confirma que `Claude Sonnet 4.5` sigue seleccionado.
5. Envía:

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Observa cómo Copilot explora el proyecto, localiza los ayudantes de datos, la interfaz y las pruebas, modifica los archivos y ejecuta las pruebas.

> [!NOTE]
> Pueden aparecer botones **Keep** y **Undo** en el editor mientras Copilot trabaja. Espera a que termine para decidir qué cambios conservar.

7. Cuando Copilot solicite ejecutar las pruebas, selecciona **Continue**.
8. Puede haber pausas o pruebas fallidas durante el proceso. Copilot puede corregir el código y volver a ejecutar las pruebas hasta completarlas sin errores.
9. Revisa el código generado.

> [!CAUTION]
> Es siempre importante revisar el código generado por Copilot o cualquier herramienta de IA.

10. Vuelve al navegador y prueba la nueva funcionalidad.
11. Cuando hayas confirmado que funciona y revisado el código, selecciona **Keep**.

## Ejercicio opcional: implementar paginación

Si el catálogo crece, puede ser necesario activar la paginación. Utiliza lo aprendido para pedir a Copilot que implemente la paginación:

- sigue las prácticas existentes y utiliza los archivos de instrucciones;
- decide si el usuario podrá seleccionar el tamaño de página o si será fijo;
- proporciona suficiente contexto en la indicación;
- iterar con Copilot cuando haga falta forma parte del flujo normal.

## Resumen y próximos pasos

Has utilizado el modo agente de Copilot para añadir funcionalidad a Tailspin Toys. Has aprendido que:

- el modo agente puede implementar cambios coordinados en la interfaz y la capa de datos;
- puede explorar el proyecto, identificar archivos relevantes y ejecutar pruebas;
- debes revisar todos los cambios y pruebas antes de combinarlos.

A continuación, [probarás la funcionalidad con el servidor MCP de Playwright][next-lesson] y abrirás una solicitud de incorporación de cambios.

## Recursos

- [Modos Ask, Edit y Agent de Copilot: qué hacen y cuándo utilizarlos][choose-mode]
- [Modo agente en VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
