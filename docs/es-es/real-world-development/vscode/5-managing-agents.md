---
title: "Ejercicio 5 - Supervisa y gestiona agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Agentes personalizados][previous-lesson] |
|:--|

Cuando usas GitHub Copilot en modo de agente, trabaja de forma autónoma: explora el código base, propone cambios, edita archivos y ejecuta comandos. Como trabaja en tu equipo en tiempo real, Copilot Chat en VS Code muestra cada llamada a herramientas y cada edición de archivo a medida que sucede. Puedes revisar las diferencias en el chat, aceptar o rechazar cambios concretos y guiar la conversación con prompts de seguimiento para ajustar o ampliar el trabajo sin salir del editor.

En este ejercicio:

- supervisarás en tiempo real el trabajo del agente de accesibilidad.
- revisarás y aceptarás los cambios de archivo propuestos.
- guiarás al agente durante la sesión para que añada un control de tema claro junto con el modo de alto contraste.

## Situación

El agente personalizado de accesibilidad del [ejercicio 4][previous-lesson] está implementando el modo de alto contraste. Mientras trabaja, el equipo de diseño ha solicitado otra función: un control para activar el tema claro, dirigido a usuarios a quienes les resulte demasiado oscuro el tema predeterminado. En lugar de empezar una conversación nueva, guiarás la sesión existente para ampliar el trabajo.

## Supervisa el progreso de Copilot

La vista Copilot Chat muestra cada paso del agente: los archivos que explora, los comandos que ejecuta y las ediciones que propone. Cada edición aparece en el chat con sus diferencias y los controles **Keep** y **Undo**.

1. Vuelve a la vista Copilot Chat del ejercicio 4.
2. Mientras trabaja el agente, desplázate por el chat para ver cada llamada a herramienta. Verás lecturas y ediciones de archivos y los comandos de terminal que solicita ejecutar.
3. Cuando el agente proponga una edición, aparecerá una comparación en línea:
   - selecciona **Keep** para aceptar el cambio.
   - selecciona **Undo** para revertirlo y pedir al agente que vuelva a intentarlo.
4. También puedes abrir el indicador **Files changed** de la parte superior del chat para ver todos los archivos modificados durante esta sesión.

> [!NOTE]
> Si una llamada a herramienta solicita permiso (por ejemplo, para ejecutar un comando de terminal), el agente se detendrá y mostrará una solicitud **Allow**. Aprueba solo los comandos que te parezcan adecuados.

5. Espera a que el agente termine de implementar el modo de alto contraste. Debería mostrar un mensaje final que resuma los cambios.

## Guía al agente para añadir el tema claro

Cuando el modo de alto contraste esté listo, amplía la misma conversación para añadir un control del tema claro. Como continuarás en la misma sesión, el agente conservará el contexto del trabajo anterior, incluidos los componentes modificados, el enfoque de estilo y el patrón de almacenamiento local.

1. En el campo de texto de Copilot Chat, envía este prompt de seguimiento:

    ```plaintext
    Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
    ```

2. El agente continuará desde donde dejó el trabajo, explorará los cambios y propondrá cómo añadir el tema claro.
3. Revisa cada cambio nuevo a medida que se aplique, como hiciste con el modo de alto contraste. Usa **Keep** o **Undo** para cada diferencia.
4. Si el agente sigue un enfoque que no quieres —por ejemplo, si intenta reorganizar la interfaz de los controles de una forma que no te convence—, puedes detenerlo con el botón **Stop** junto al campo de texto y enviar un mensaje de seguimiento para aclarar lo que necesitas.

> [!TIP]
> Guiar una sesión en curso es más rápido que empezar de nuevo. Envía prompts de seguimiento para pedir ajustes («simplifica el CSS: usa variables CSS en lugar de duplicar selectores»), corregir el rumbo («no añadas un tercer control; integra el tema claro en el panel de configuración existente») o ampliar el alcance («añade también métodos abreviados de teclado para ambos controles»).

## Revisa los cambios

Antes de confirmar el trabajo, revisa rápidamente todos los archivos modificados por el agente.

1. Abre la vista **Source Control** de VS Code.
2. Revisa la lista completa de archivos modificados. Deberías ver cambios en los componentes Astro, los estilos y las pruebas relacionadas.
3. Abre algunos archivos modificados y examina las diferencias. Confirma que se aplican los principios de accesibilidad del agente personalizado: atributos ARIA, navegación con teclado, HTML semántico y persistencia en el almacenamiento local.
4. Cuando estés satisfecho, prepara y confirma los cambios desde el panel Source Control. Los publicarás en [la siguiente lección][next-lesson].

## Resumen y próximos pasos

Has usado el modo de agente de Copilot Chat para supervisar y guiar una sesión en curso: has revisado los cambios de archivo a medida que se aplicaban, aceptado o rechazado ediciones y enviado prompts de seguimiento para ampliar el trabajo sin perder el contexto.

En esta lección has aprendido a:

- supervisar el trabajo de un agente en tiempo real.
- aceptar y rechazar ediciones individuales.
- guiar una sesión en curso con prompts de seguimiento.

En la [siguiente lección][next-lesson] publicarás el trabajo de accesibilidad como pull request y revisarás los cambios generados durante el taller por el agente personalizado local.

## Recursos

- [Copilot Chat en VS Code][copilot-chat-vscode]
- [Usar el modo de agente][agent-mode]

---

| [← Lección anterior: Agentes personalizados][previous-lesson] | [Siguiente lección: Itera sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
