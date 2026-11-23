---
title: "Ejercicio 5 - Supervisar y gestionar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Ejercicio anterior: Agentes personalizados][previous-lesson] |
|:--|

Cuando utilizas Copilot en modo agente, explora el código, propone cambios, los aplica y ejecuta comandos de forma autónoma. En VS Code puedes observar cada llamada a herramientas y cada edición en tiempo real. Puedes revisar diferencias en línea y aceptar o rechazar cambios, así como orientar la conversación con indicaciones adicionales.

En este ejercicio:

- supervisarás el trabajo del agente de accesibilidad;
- revisarás y aceptarás las ediciones propuestas;
- orientarás la sesión para añadir un control de modo claro.

## Escenario

El agente personalizado de accesibilidad utilizado en el [Ejercicio 4][previous-lesson] está implementando el modo de alto contraste. Mientras trabaja, el equipo de diseño solicita también un modo claro para las personas que encuentran demasiado oscuro el tema predeterminado. En lugar de iniciar otra conversación, ampliarás la sesión existente.

## Supervisar el progreso de Copilot

La vista de Copilot Chat muestra los pasos, lecturas de archivos, comandos y ediciones propuestas.

1. Vuelve a la vista de Copilot Chat del ejercicio anterior.
2. Mientras el agente trabaja, observa las llamadas a herramientas y las lecturas o modificaciones.
3. Cuando aparezca una diferencia:
   - selecciona **Keep** para aceptar el cambio;
   - selecciona **Undo** para revertirlo y permitir un nuevo intento.
4. Utiliza el indicador **Files changed** para revisar el conjunto completo de archivos modificados.

> [!NOTE]
> Si una llamada a herramientas solicita permisos, por ejemplo para ejecutar un comando, el agente mostrará una petición de **Allow**. Aprueba únicamente los comandos que consideres adecuados.

5. Espera a que el agente termine de implementar el modo de alto contraste y revisa su resumen final.

## Orientar al agente para añadir el modo claro

Continúa la misma conversación para añadir el modo claro. El agente conservará el contexto previo, incluidos los componentes modificados, el enfoque de estilos y el patrón de almacenamiento local.

1. Envía la siguiente indicación de seguimiento:

   ```plaintext
   Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
   ```

2. El agente continuará desde su estado actual y propondrá cambios para el modo claro.
3. Revisa cada modificación con **Keep** o **Undo**.
4. Si el agente toma una dirección que no quieres, selecciona **Stop** junto al campo de chat y envía una indicación aclaratoria.

> [!TIP]
> Orientar una sesión activa suele ser más rápido que comenzar otra desde cero. Puedes solicitar ajustes, corregir el enfoque o ampliar el alcance mediante indicaciones de seguimiento.

## Revisar el conjunto de cambios

Antes de confirmar el trabajo:

1. Abre la vista **Source Control** de VS Code.
2. Revisa todos los archivos modificados.
3. Abre algunos archivos y examina las diferencias.
4. Confirma que se mantienen los patrones de accesibilidad: atributos ARIA, navegación por teclado, HTML semántico y persistencia mediante almacenamiento local.
5. Cuando estés satisfecho, prepara y confirma los cambios desde el panel de control de código fuente.

## Resumen y próximos pasos

Has utilizado el modo agente de Copilot Chat para supervisar y orientar una sesión activa: revisar cada modificación, aceptar o rechazar cambios y enviar indicaciones de seguimiento sin perder el contexto.

En la [próxima lección][next-lesson] publicarás el trabajo de accesibilidad como solicitud de incorporación de cambios y revisarás los cambios producidos por el agente personalizado.

## Recursos

- [Copilot Chat en VS Code][copilot-chat-vscode]
- [Uso del modo agente][agent-mode]

---

| [← Ejercicio anterior: Agentes personalizados][previous-lesson] | [Siguiente ejercicio: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
