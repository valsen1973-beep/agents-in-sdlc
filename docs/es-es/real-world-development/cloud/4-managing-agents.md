---
title: "Ejercicio 4 - Supervisa y gestiona agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

En los dos ejercicios anteriores has pedido al agente en la nube de Copilot que se ocupe de tres tareas diferentes para mejorar la experiencia de usuario y añadir funcionalidad. Aunque el agente en la nube trabaja de forma autónoma y asíncrona, es importante supervisar estas tareas.

Dispones de varias herramientas para gestionar las tareas asignadas al agente en la nube, entre ellas la [página de agentes][agents-page] de GitHub.com. Desde este centro de control puedes ver las tareas de los agentes que tienen pull requests (PR) abiertas. También puedes explorar las operaciones realizadas e incluso guiar una sesión en curso.

En esta lección:

- explorarás la página de agentes para supervisar las tareas del agente en la nube.
- guiarás una sesión en curso para solicitar funcionalidad adicional.

## Situación

Después de asignar al agente el modo de alto contraste, el equipo decidió que sería buen momento para añadir también un tema claro. Ya se está actualizando el estilo del sitio y añadiendo controles de selección, por lo que tenía sentido incluir esta función. Guiarás el trabajo del agente para que añada el tema claro junto al modo de alto contraste.

## Revisa las tareas del agente en la nube de Copilot

Veamos el estado de las tareas que se han asignado al agente en la nube de Copilot.

1. Abre la [página de agentes de Copilot](https://github.com/copilot/agents).
2. Observa la lista de tareas en el panel principal y en el panel izquierdo. Deberías encontrar las tareas asignadas a Copilot, entre ellas:
   - actualizar la documentación del código base.
   - generar API para modificar juegos.
   - añadir un modo de alto contraste al sitio web.
3. Selecciona una de las tareas en curso y revisa las operaciones realizadas por Copilot. Pueden incluir:
   - obtener el código del repositorio.
   - preparar el entorno para Copilot.
   - configurar servidores MCP.
   - realizar los distintos pasos necesarios para completar la tarea.

> [!NOTE]
> Los pasos exactos variarán según el estado del trabajo de Copilot y el enfoque que haya seguido.

4. Observa también el panel de pull request (PR) que aparece a la derecha. Muestra la PR y los archivos modificados para facilitar la supervisión.

## Guía al agente en la nube

Ya has visto las tareas activas. Pidamos ahora a Copilot que incluya el control del tema claro mientras trabaja en el modo de alto contraste.

1. Selecciona la sesión relacionada con el modo de alto contraste. El título exacto dependerá del nombre que haya elegido Copilot y del estado actual del trabajo.

    ![Sesión de accesibilidad en el panel de agentes](../../../_images/ex6-accessibility-session.png)

2. Observa la sesión durante unos minutos hasta que indique que ha terminado de preparar el entorno y ha empezado a trabajar. Lo notarás cuando aparezcan mensajes parecidos a los siguientes.
3. En el cuadro de diálogo **Steer active session while Copilot is working**, escribe este prompt:

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![Captura de la tarea del agente en la nube en la página de agentes, con el cuadro de diálogo para guiar una sesión activa resaltado](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pulsa <kbd>Enter</kbd> para enviar el prompt.
5. Observa cómo Copilot lo confirma y lo añade a su flujo de trabajo.

## Deja que Copilot trabaje

Como antes, Copilot comenzará a trabajar en la tarea actualizada. Incorporará la nueva solicitud al flujo después de terminar el paso en el que estuviera trabajando cuando enviaste el mensaje.

El proceso tardará varios minutos, así que puedes aprovechar el tiempo para reflexionar sobre todo lo que has aprendido y explorado hasta ahora.

## Resumen y próximos pasos

En esta lección has explorado la página de agentes de Copilot, el centro de control para supervisar y guiar las tareas del agente en la nube de GitHub Copilot. Desde ahí puedes hacer un seguimiento de las tareas activas y completadas, revisar el trabajo en curso y redirigir las tareas activas para cambiar su alcance o añadir contexto.

Has aprendido a:

- explorar el centro de control y la página de agentes para supervisar las tareas del agente en la nube.
- redirigir una sesión en curso para solicitar funcionalidad adicional.

Mientras Copilot completa las mejoras de accesibilidad, puedes [iterar sobre las pull requests creadas por Copilot][next-lesson].

## Recursos

- [Página de agentes de Copilot][agents-page]
- [Acerca de los agentes personalizados][custom-agents]

---

| [← Lección anterior: Agentes personalizados][previous-lesson] | [Siguiente lección: Itera sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
