---
title: "Ejercicio 2 - Agente en la nube de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Instrucciones personalizadas][previous-lesson] |
|:--|

Es probable que casi todas las organizaciones tengan problemas de deuda técnica. Pueden ser problemas de seguridad sin resolver, código heredado que necesita actualizarse o solicitudes de funcionalidad que llevan mucho tiempo en el backlog por falta de tiempo. El agente en la nube de GitHub Copilot puede actualizar código y añadir funcionalidad de forma autónoma. Cuando termina, genera una pull request en borrador para que la revise un desarrollador. Así es posible delegar tareas tediosas, acelerar el desarrollo y dedicar más tiempo a los problemas generales.

Con el agente en la nube de Copilot explorarás cómo:

- personalizar el entorno de generación de código.
- asegurarte de que las operaciones se realicen de forma segura.
- crear incidencias con un alcance claro.
- asignar incidencias a Copilot.

## Situaciones

Tailspin Toys tiene deuda técnica pendiente. Los contratistas que crearon la primera versión del sitio dejaron la documentación en mal estado: comprobarás que falta por completo. El primer paso es añadir comentarios TSDoc a todas las funciones exportadas de la aplicación.

Además, el equipo de diseño quiere mejorar la exploración de juegos. Quiere mostrar juegos relacionados —otros títulos de la misma categoría— en la página de detalles de cada juego, para que los usuarios puedan seguir explorando. No necesita una implementación perfecta, sino algo que permita hacer pruebas de aceptación de la experiencia. Es un impedimento, pero hay incidencias más prioritarias.

Estos son dos ejemplos de tareas que pueden quedar relegadas y que conviene asignar al agente en la nube de Copilot. El agente puede trabajar en ellas de forma asíncrona mientras el desarrollador se ocupa de otras tareas y, después, puede revisar su trabajo y confirmar que todo está bien.

## Presentación del agente en la nube de GitHub Copilot

El [agente en la nube de GitHub Copilot](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) puede realizar tareas en segundo plano de forma parecida a un desarrollador. Puedes hacerlo de varias formas, por ejemplo, [asignando una incidencia de GitHub a Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions). Cuando se le asigna una incidencia, Copilot crea una pull request en borrador para registrar el progreso, configura un entorno y empieza a trabajar. Puedes consultar la sesión de Copilot mientras sigue en curso o una vez terminada. Cuando la solución propuesta esté lista para revisión, te mencionará en la pull request.

## La importancia de acotar bien las instrucciones

GitHub Copilot no hace magia: no puedes dejar de pensar en la tarea. Hasta las operaciones que parecen sencillas pueden ser complejas al analizarlas en detalle. Por eso, ten en cuenta las [prácticas recomendadas para acotar tareas para el agente en la nube][cloud-agent-best-practices]. Trátalo como un compañero de programación con IA: trabaja por etapas, aprende, experimenta y adapta el enfoque. Los fundamentos del desarrollo de software no cambian al añadir IA generativa.

## Instrucciones personalizadas de este repositorio

En ejercicios anteriores has aprendido cómo guían las instrucciones personalizadas a Copilot. Si ya has completado un ejercicio práctico sobre instrucciones personalizadas, habrás visto cómo funciona `.github/copilot-instructions.md`. Si no, este es un buen momento para revisar rápidamente los archivos de instrucciones que incluye el repositorio. Antes de asignar trabajo al agente en la nube, léelos sin hacer cambios para que luego puedas observar su efecto.

Abre estos archivos en la interfaz web de GitHub o en un codespace:

- `.github/copilot-instructions.md`: revisa la sección **Code standards**, especialmente las convenciones de TypeScript y los comentarios TSDoc.
- `.github/instructions/unit-tests.instructions.md`: fíjate en el frontmatter `applyTo`, que aplica estas instrucciones a los archivos `**/*.test.ts`.

Cuando asignes al agente en la nube la incidencia `Code lacks documentation` en la sección siguiente, comprueba si la pull request incluye comentarios TSDoc, convenciones de TypeScript y cabeceras de archivo procedentes de estas instrucciones. Volveremos a señalarlo al revisar las PR en una lección posterior.

## Configura el entorno de desarrollo del agente en la nube de Copilot

Para crear código suele ser necesario configurar el entorno y ejecutar scripts de preparación. Lo mismo se aplica al asignar tareas a Copilot, que trabaja de forma parecida a un ingeniero de software.

El agente en la nube usa [GitHub Actions][github-actions] como entorno de trabajo. Puedes personalizarlo con un [flujo de trabajo de configuración especial][setup-workflow] en `.github/workflows/copilot-setup-steps.yml`, que se ejecuta antes de que el agente empiece. Así puedes darle acceso a las herramientas y dependencias necesarias. Este flujo ya está configurado para el taller y prepara Node.js, las dependencias del proyecto, los navegadores para las pruebas de extremo a extremo y la base de datos SQLite migrada y precargada para la aplicación Astro:

```yaml
name: "Copilot Setup Steps"

# Permite probar los pasos de configuración desde la pestaña "Actions" del repositorio
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Establece los permisos mínimos necesarios para *tus pasos*. Copilot tendrá su propio token para sus operaciones.
    permissions:
      # Si quieres clonar el repositorio como parte de los pasos de configuración, por ejemplo, para instalar dependencias, necesitarás el permiso `contents: read`. Si no clonas el repositorio durante la configuración, Copilot lo hará automáticamente cuando terminen los pasos.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Configuración del frontend y de la aplicación: Node.js (la aplicación usa Astro y Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migra y precarga la base de datos SQLite local para que las compilaciones y las pruebas tengan datos.
      - name: Set up the database
        run: npm run db:setup
```

El archivo se parece a cualquier otro flujo de trabajo de GitHub, pero tiene algunos aspectos importantes:

- Contiene un único trabajo llamado `copilot-setup-steps`. Se ejecuta en GitHub Actions antes de que Copilot empiece a trabajar en la pull request.
- El activador `workflow_dispatch` permite ejecutar manualmente el flujo de trabajo desde la pestaña **Actions** del repositorio. Es útil para comprobar que funciona sin esperar a que Copilot lo ejecute.

## Añade documentación

Todo el mundo entiende la importancia de la documentación, pero muchos proyectos tienen información desactualizada o carecen de ella. Esta deuda técnica suele quedar desatendida, lo que reduce la productividad y dificulta mantener el código o incorporar a nuevos desarrolladores. Copilot destaca a la hora de crear documentación, así que esta es una buena incidencia para el agente en la nube. Trabajará en segundo plano y generará la documentación necesaria. En una lección posterior revisarás su trabajo.

1. Abre tu repositorio en github.com en una pestaña nueva del navegador.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el cuadro de diálogo de nueva incidencia.
4. Selecciona **Blank issue**.
5. Escribe `Code lacks documentation` en el campo **Title**.
6. En **Description**, escribe:

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. Selecciona **Create** para crear la incidencia.
8. En el lado derecho, selecciona **Assign to Copilot** para abrir el cuadro de diálogo de asignación.

  ![Asignación de Copilot a una incidencia](../../../_images/shared-assign-copilot.png)

9. Selecciona **Assign**.
10. Selecciona la pestaña **Pull Requests**.
11. Abre la pull request (PR) que se ha generado. Su título será parecido a `[WIP]: Code lacks documentation`. Si aún no aparece, espera un momento y actualiza la ventana del navegador.
12. Al cabo de unos minutos, Copilot debería haber creado una lista de tareas.

> [!NOTE]
> La lista de tareas puede tardar varios minutos en aparecer en la PR. Copilot está preparando el entorno (ejecuta el flujo de trabajo anterior), analiza el proyecto y determina la mejor forma de abordar el problema.

13. Revisa la lista y las tareas que va a completar.
14. Desplázate por la cronología de la pull request y busca un mensaje que indique que Copilot ha empezado a trabajar en la incidencia.
15. Selecciona el botón **View session**.

  ![Vista de la sesión de Copilot](../../../_images/ex4-view-session.png)

> [!CAUTION]
> Es posible que tengas que actualizar la ventana para ver el indicador actualizado.

16. Desplázate por la sesión en directo y observa cómo Copilot resuelve el problema: explora el código y comprende el estado del proyecto, se detiene a pensar y decidir el plan y crea código.

El proceso puede tardar varios minutos. Uno de los objetivos principales del agente en la nube de Copilot es trabajar de forma asíncrona para que puedas ocuparte de otras tareas. Aprovecharemos esa función asignándole otra tarea y, mientras tanto, nos centraremos en crear una funcionalidad para la aplicación.

## Añade una sección de juegos relacionados a la página de detalles

Una de las ventajas del agente en la nube de GitHub Copilot es que permite repartir el trabajo para que tú y el agente podáis ocuparos de tareas distintas. Puede que añadir una sección de juegos relacionados no lleve mucho tiempo, pero podrías dedicar ese tiempo a otro trabajo. Asignemos la tarea al agente en la nube de Copilot.

1. Vuelve a tu repositorio en github.com.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el cuadro de diálogo de nueva incidencia.
4. Selecciona **Blank issue**.
5. En el campo **Title**, escribe `Show related games on the game details page`.
6. En **Description**, escribe:

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
    ```

7. Selecciona **Create** para crear la incidencia.
8. En el lado derecho, selecciona **Assign to Copilot** para abrir el cuadro de diálogo de asignación.

  ![Asignación de Copilot a una incidencia](../../../_images/shared-assign-copilot.png)

9. Selecciona **Assign**.

Al poco tiempo, aparecerá 👀 en el primer comentario de la incidencia para indicar que Copilot está trabajando en ella.

![Copilot usa el emoji de ojos para indicar que está trabajando en la incidencia](../../../_images/ex4-issue-eyes-emoji.png)

Copilot ya está trabajando en la segunda solicitud. El agente en la nube trabaja de forma parecida a un ingeniero de software, así que no hace falta supervisarlo continuamente; puedes revisar el resultado cuando termine. Ahora veremos cómo crear y usar agentes personalizados.

## Resumen y próximos pasos

En esta lección has explorado el [agente en la nube de GitHub Copilot][copilot-agents]. Puedes asignar incidencias a Copilot para que trabaje de forma asíncrona. Copilot puede resolver deuda técnica, crear funcionalidades o ayudar a migrar código a otro framework.

Has aprendido a:

- personalizar el entorno de generación de código.
- asegurarte de que las operaciones se realicen de forma segura.
- crear incidencias con un alcance claro.
- asignar incidencias a Copilot.

Mientras el agente en la nube trabaja en segundo plano, puedes aprender a crear y usar agentes personalizados. El [agente en la nube de Copilot también admite servidores MCP][cloud-agent-mcp] y puede usar las instrucciones personalizadas que hemos visto en módulos anteriores.

## Recursos

- [Acerca del agente en la nube de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Prácticas recomendadas para el flujo de configuración del agente en la nube][cloud-agent-best-practices]

| [Siguiente lección: Agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
