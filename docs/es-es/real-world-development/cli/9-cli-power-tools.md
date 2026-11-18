---
title: "Lección 9 - Comandos de barra de GitHub Copilot CLI"
description: "Explora los comandos de barra para gestionar el contexto, seleccionar modelos, compartir sesiones y delegar trabajo opcionalmente en la nube."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como cualquier buena herramienta de CLI, GitHub Copilot CLI incluye muchos comandos de barra para interactuar con ella. Estos comandos ofrecen funciones avanzadas, información interna y opciones de configuración adicionales. Ya has usado comandos como `/diff`, `/mcp`, `/skills`, `/agent` y `/pr`. Veamos algunos más.

En esta lección:

- usarás `/context` y `/compact` para explorar cómo gestiona Copilot el contexto de la conversación.
- usarás `/model` para explorar los modelos disponibles.
- aprenderás cómo `/share` puede exportar o compartir una sesión.
- explorarás comandos opcionales para trabajar en paralelo, usar worktrees y delegar trabajo en el agente en la nube.

## Situación

Has terminado el flujo de trabajo principal de la CLI. Ahora veremos otras funciones: gestionar el contexto, cambiar de modelo, compartir sesiones y, de forma opcional, delegar trabajo en el [agente en la nube de Copilot][about-cloud-agent].

## Explora el contexto de Copilot CLI

En tareas grandes o complejas, puede que alcances el límite de contexto del modelo. Copilot CLI compacta automáticamente la conversación cuando hace falta, y puedes inspeccionarla o compactarla tú mismo con los comandos de barra.

1. Vuelve a tu Codespace e inicia Copilot CLI desde la raíz del repositorio si aún no está abierto.
2. Escribe:

   ```plaintext
   /context
   ```

3. Observa el modelo, el uso actual de tokens y cómo se distribuye el contexto entre las instrucciones del sistema, las herramientas, los mensajes y el espacio disponible.
4. Compacta la conversación:

   ```plaintext
   /compact
   ```

5. Vuelve a escribir `/context` y compara el resultado. Si la conversación ya es pequeña, quizá no veas un cambio notable.

> [!NOTE]
> Copilot CLI compacta automáticamente el contexto cuando se llena la ventana. Usa `/compact` para elegir cuándo hacerlo. Usa `/clear` o `/new` cuando cambies a una tarea no relacionada y quieras empezar una conversación nueva.

## Elige el modelo

Los distintos modelos tienen puntos fuertes distintos, y cada desarrollador puede tener sus preferencias. Copilot CLI permite mostrar los modelos disponibles y seleccionar uno.

1. Escribe:

   ```plaintext
   /model
   ```

2. Explora los modelos disponibles y la información sobre su uso.
3. Mantén el modelo actual, selecciona otro o pulsa <kbd>Esc</kbd> para cerrar la lista.

## Comparte una sesión

Trabajar en equipo y compartir lo aprendido ayuda a todo el mundo a mejorar el uso de las herramientas de IA. El comando `/share` permite exportar una sesión a un archivo Markdown o HTML, crear un enlace para compartirla o publicar un gist de GitHub.

1. Escribe `/help` y revisa las opciones de `/share` disponibles en tu versión.
2. Si quieres compartir la sesión, elige el destino adecuado; por ejemplo, `/share file` para exportar un archivo Markdown local.
3. Revisa el contenido exportado antes de enviarlo o publicarlo. Las exportaciones pueden incluir prompts, respuestas e información del proyecto.

Publicar un enlace o un gist es opcional. No publiques contenido del repositorio o de la conversación que tu equipo no quiera compartir.

## Opcional: amplía el trabajo o delégalo

El taller principal ha terminado. Copilot CLI también ofrece comandos para tareas mayores:

- `/fleet` puede dividir una tarea en subtareas independientes y ejecutarlas en paralelo mediante subagentes.
- `/worktree` puede crear un worktree de Git aislado para otra tarea.
- `/delegate` puede enviar una tarea al agente en la nube de Copilot, que trabaja de forma asíncrona y puede abrir una pull request.

Estos comandos son opcionales porque pueden crear worktrees adicionales o iniciar trabajo remoto. Antes de probarlos, inicia una tarea nueva y bien acotada, y revisa el resultado con tu flujo de trabajo habitual. Si quieres profundizar en el trabajo de agentes asíncronos, continúa con el [taller del agente en la nube][cloud-workshop].

## Resumen y próximos pasos

Los comandos de barra de Copilot CLI permiten configurar la herramienta, compartir sesiones y ver qué ocurre en segundo plano. En esta lección:

- usaste `/context` y `/compact` para explorar cómo gestiona Copilot el contexto de la conversación.
- usaste `/model` para explorar los modelos disponibles.
- aprendiste cómo `/share` puede exportar o compartir una sesión.
- exploraste comandos opcionales para trabajar en paralelo, usar worktrees y delegar trabajo en el agente en la nube.

Copilot CLI ofrece muchos más comandos de barra y funciones por descubrir. Para cerrar el recorrido, [repasaremos lo aprendido][next-lesson] y veremos los próximos pasos.

## Recursos

- [Referencia de comandos de Copilot CLI][cli-reference]
- [Gestión del contexto en Copilot CLI][context-management]
- [Acerca del agente en la nube de Copilot][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
