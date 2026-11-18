---
title: "Ejercicio 5: Itera sobre el trabajo de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Supervisa los agentes][previous-lesson] |
|:--|

## Revisa el trabajo

A lo largo de este taller has trabajado con GitHub Copilot en varias tareas para mejorar la experiencia de usuario y añadir funciones. Le has pedido a Copilot que documente el código, cree una función de juegos relacionados para que el equipo de diseño pueda explorarla e implemente mejoras de accesibilidad, incluidos controles para el modo de alto contraste y el tema claro. Revisemos los cambios y, si hace falta, enviemos comentarios a Copilot para que los mejore.

### Situación

Como hemos repetido varias veces, los fundamentos del diseño de software y DevOps no cambian al añadir IA generativa. Siempre hay que revisar el código generado y seguir el proceso habitual de DevOps. Con eso en mente, revisemos las sugerencias de GitHub Copilot para añadir documentación, juegos relacionados y mejoras de accesibilidad antes de activar la revisión para el resto del equipo.

## Seguridad y agente en la nube de GitHub Copilot

Como el agente en la nube de Copilot trabaja de forma asíncrona y sin supervisión, se han establecido restricciones de seguridad para que el proceso siga siendo seguro. Entre ellas:

- Copilot solo tiene acceso de lectura al repositorio y acceso de escritura **únicamente** a la rama que utiliza para su código.
- El agente en la nube se ejecuta en GitHub Actions y crea un entorno efímero independiente para trabajar.
- Una persona debe aprobar cualquier flujo de trabajo de GitHub Actions antes de ejecutarlo.
- [El acceso a recursos externos está limitado de forma predeterminada](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall), incluidos los servidores MCP.

## Revisa la documentación generada

Empecemos por la primera pull request (PR) creada por el agente en la nube de GitHub Copilot: la que añade documentación al código. Usarás la interfaz estándar de las PR de GitHub.com.

> [!NOTE]
> Al abrir la PR, quizá veas una advertencia de que el cortafuegos bloquea GitHub Copilot. Es **normal**: Copilot tiene acceso limitado a recursos externos de forma predeterminada, incluidas las llamadas a servidores MCP externos. Si quieres, puedes [personalizar o deshabilitar el cortafuegos del agente en la nube de Copilot][agent-firewall].

1. Vuelve al repositorio en github.com.
2. Selecciona **Pull Requests** para abrir la lista de PR.
3. Abre la pull request titulada algo parecido a **Add missing documentation**.

> [!NOTE]
> Si Copilot sigue trabajando, el título de la pull request incluirá la etiqueta **[WIP]**. En ese caso, espera a que termine. Puede tardar unos minutos; puedes descansar o repasar lo que has aprendido.

4. Cuando la PR esté lista, selecciona la pestaña **Files changed** y revisa los cambios.

    ![Pestaña Files changed](../../../_images/shared-pr-files-changed.png)

5. Explora el código actualizado, que incluirá nuevos comentarios TSDoc y otra documentación. Los cambios exactos pueden variar.

    Al revisar los cambios, busca comentarios TSDoc, convenciones de TypeScript y cabeceras de archivo. Proceden de los archivos de instrucciones que revisaste al principio del ejercicio 2.

6. Cuando hayas revisado las actualizaciones y estés conforme, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
7. Deberías ver un indicador que muestra que hay flujos de trabajo pendientes de aprobación.
8. Si hay flujos pendientes, selecciona **Approve and run workflows**.

   ![Aprobar y ejecutar flujos de trabajo](../../../_images/shared-approve-workflows.png)

9. En la sección de comprobaciones de la PR, deberían aparecer los flujos de trabajo en cola. Si todo va bien, las comprobaciones del proyecto para la aplicación Astro deberían superarse. Puede tardar unos minutos.

## Pide cambios a GitHub Copilot

La colaboración con Copilot en una pull request no tiene por qué ser un proceso unidireccional. Puedes mencionarlo en comentarios de la PR o en comentarios en línea del código, igual que harías con otra persona del equipo. Copilot verá el comentario e iniciará otra sesión para resolverlo. Como los resultados no son deterministas, no podemos especificar exactamente qué pedir. Algunas ideas:

- Añadir a cada archivo de código una cabecera de comentarios que describa brevemente su contenido.
- Añadir comentarios TSDoc a los archivos TypeScript y Astro.
- Crear un archivo README que describa la estructura de la aplicación Astro.

1. Añade un comentario con una solicitud de cambio a la documentación generada y menciona a **@copilot**, como harías con cualquier usuario. Puedes usar una de las ideas anteriores o proponer otra mejora de documentación.
2. Selecciona **View Session** para observar el trabajo de Copilot. Verás que inicia una sesión nueva para realizar los cambios.
3. Selecciona **Back to pull request** para volver a la PR.

    ![Volver a la pull request](../../../_images/ex7-back-to-pr.png)

4. Cuando Copilot termine, aparecerá un commit nuevo en la pull request.
5. Selecciona la pestaña **Files changed** para revisar los cambios.

Puedes seguir iterando hasta que estés satisfecho. Cuando hayas terminado, puedes marcar la PR como lista para revisión y combinarla en la rama principal.

![Marcar la PR como lista para revisión](../../../_images/ex7-ready-for-review.png)

## Revisa la funcionalidad de juegos relacionados

Volvamos a la PR que Copilot ha creado para resolver la incidencia de los juegos relacionados en la página de detalles.

1. Vuelve al repositorio en GitHub.com.
2. Selecciona la pestaña **Pull Requests**.
3. Selecciona la PR titulada algo parecido a **Show related games on the game details page**.
4. Selecciona la pestaña **Files changed** para revisar el código generado.
5. Cuando hayas revisado los cambios y estés satisfecho, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
6. Deberías ver un indicador que muestra que hay flujos de trabajo pendientes de aprobación.
7. Si hay flujos pendientes, selecciona **Approve and run workflows**.

   ![Aprobar y ejecutar flujos de trabajo](../../../_images/shared-approve-workflows.png)

8. En la sección de comprobaciones de la PR, deberían aparecer los flujos de trabajo en cola. Si todo va bien, las comprobaciones del proyecto para la aplicación Astro deberían superarse. Puede tardar unos minutos.
9. **Opcional:** puedes cambiar a esta rama en tu Codespace y probar manualmente la funcionalidad de juegos relacionados. Abre el terminal del Codespace y ejecuta estos comandos (sustituye `<branch-name>` por el nombre de la rama creada por Copilot, por ejemplo, **copilot/fix-8**):

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

Copilot ha creado la función de juegos relacionados. Como antes, puedes trabajar de forma iterativa con el agente en la nube y solicitar actualizaciones, por ejemplo, cambiar la cantidad de juegos relacionados que se muestra o añadir las cabeceras y los comentarios TSDoc que faltan (recuerda que asignaste esta tarea **antes** de actualizar las instrucciones personalizadas). Para ello, añade otro comentario en la pestaña **Conversation**; Copilot lo verá e iniciará una sesión nueva.

## Revisa las funciones de accesibilidad

Por último, revisemos las mejoras de accesibilidad implementadas mediante el agente personalizado. Esta PR debería incluir el modo de alto contraste que asignaste en el ejercicio 3 y el tema claro que solicitaste desde el panel de agentes en el ejercicio 4.

1. Vuelve al repositorio en GitHub.com.
2. Selecciona la pestaña **Pull Requests**.
3. Selecciona la PR titulada algo parecido a **Add high contrast mode to website**.

> [!NOTE]
> Si Copilot sigue trabajando, el título de la pull request incluirá la etiqueta **[WIP]**. En ese caso, espera a que termine. Puede tardar unos minutos.

4. Selecciona la pestaña **Files changed** para revisar el código generado.
5. Revisa la implementación y presta atención a estos elementos:
   - los componentes de interfaz de usuario para cambiar de modo.
   - el uso del almacenamiento local para conservar las preferencias del usuario.
   - los cambios de CSS o de estilo para los modos de alto contraste y claro.
   - los atributos de accesibilidad, como las etiquetas ARIA y la navegación con teclado.
   - el código JavaScript/TypeScript que gestiona el cambio de modo.

6. Cuando hayas revisado los cambios y estés satisfecho, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
7. Deberías ver un indicador que muestra que hay flujos de trabajo pendientes de aprobación.
8. Si hay flujos pendientes, selecciona **Approve and run workflows**.

   ![Aprobar y ejecutar flujos de trabajo](../../../_images/shared-approve-workflows.png)

9. En la sección de comprobaciones de la PR, deberían aparecer los flujos de trabajo en cola. Si todo va bien, las comprobaciones del proyecto para la aplicación Astro deberían superarse. Puede tardar unos minutos.
10. **Opcional:** puedes cambiar a esta rama en tu Codespace para probar manualmente las funciones de accesibilidad. Abre el terminal del Codespace y ejecuta estos comandos (sustituye `<branch-name>` por el nombre de la rama creada por Copilot):

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    Después, inicia la aplicación y prueba los controles de alto contraste y del tema claro en el navegador. Confirma que funcionan y que las preferencias se conservan al volver a cargar la página.

Observa cómo el agente personalizado de accesibilidad ha guiado a Copilot para aplicar buenas prácticas de accesibilidad. Si detectas algún problema o mejora, puedes mencionar a **@copilot** en un comentario para solicitar cambios, como hiciste con las PR anteriores.

## Ejercicio opcional: sigue delegando

El agente en la nube es más útil cuando puedes asignarle elementos reales del backlog y ocuparte de otra cosa mientras trabaja. Para practicarlo, crea algunas incidencias más en el repositorio y asígnaselas a Copilot. Algunas ideas:

- Crear un formulario para que los patrocinadores indiquen su interés en la página de detalles del juego.
- Implementar paginación en la página con la lista de juegos.
- Añadir validación de entradas y gestión de errores a las funciones de acceso a datos.

## Resumen

Has completado el itinerario del agente en la nube. En estas lecciones:

- **Inspeccionaste los archivos de instrucciones personalizados del repositorio** para observar su efecto en el trabajo del agente.
- **Asignaste incidencias al agente en la nube de Copilot** y observaste cómo preparaba el entorno, planificaba y trabajaba de forma asíncrona.
- **Creaste y usaste un agente personalizado** para mejorar la accesibilidad con controles para los modos de alto contraste y claro.
- **Usaste la página de agentes de Copilot como centro de control** para supervisar y guiar la sesión de accesibilidad.
- **Revisaste e iteraste sobre las pull requests del agente en la nube**, mencionando a `@copilot` para solicitar cambios y aprobando flujos de trabajo.

## Revisión y próximos pasos

Has completado el itinerario del agente en la nube. Si quieres seguir explorando, los otros itinerarios complementan lo que has practicado:

- 🖥️ **[Itinerario de VS Code](../../vscode/)**: explora el modo de agente de Copilot Chat y la integración MCP directamente en el IDE.
- 💻 **[Itinerario de CLI](../../cli/)**: entrega desde el terminal dos cambios revisados con los modos Plan y Autopilot, habilidades de agente, un agente de QA personalizado, Playwright MCP, Agent Merge y el puente opcional `/delegate` al agente en la nube.

En tu propio repositorio, prueba estas ideas:

- Asigna al agente en la nube una incidencia de refactorización o cobertura de pruebas.
- Crea un agente personalizado para otro ámbito.
- Configura `copilot-setup-steps.yml` para otra pila tecnológica.

## Recursos

- [GitHub Copilot][github-copilot]
- [Acerca de los agentes de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Prácticas recomendadas para el flujo de configuración del agente en la nube][cloud-agent-best-practices]
- [Configurar el cortafuegos del agente en la nube de Copilot][agent-firewall]

---

| [← Lección anterior: Supervisar agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
