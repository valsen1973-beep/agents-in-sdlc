---
title: "Ejercicio 2 - Añade funcionalidad con el modo de agente de Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Incluso las actualizaciones más sencillas de una aplicación suelen requerir cambios en varios archivos y tareas como ejecutar pruebas. El flujo de trabajo de un desarrollador normalmente consiste en localizar los archivos necesarios, hacer los cambios, ejecutar las pruebas, depurar, averiguar qué archivo se ha pasado por alto y volver a modificarlo. Y así sucesivamente.

El modo de agente de Copilot puede ayudarte con todo esto.

El modo de agente está diseñado para trabajar de forma más autónoma en el IDE. Se comporta de manera parecida a un desarrollador: primero explora la estructura del proyecto, realiza los cambios necesarios, ejecuta tareas como las pruebas y corrige automáticamente los errores que encuentra. Veamos cómo usarlo para añadir funcionalidad al sitio.

> [!NOTE]
> Aunque los nombres se parecen, el modo de agente y el agente en la nube ofrecen experiencias distintas. El modo de agente trabaja en el IDE y permite ciclos de comentarios rápidos e interacción. El agente en la nube trabaja de forma asíncrona como un compañero del equipo e interactúa contigo mediante incidencias y pull requests.

En este ejercicio aprenderás a:

- hacer que el modo de agente de Copilot explore el proyecto, identifique los archivos pertinentes y coordine los cambios.
- implementar nuevas funciones en la interfaz de usuario y la capa de datos.
- revisar los cambios y las pruebas que genera el modo de agente antes de combinarlos en el código base.

## Situación

Como la lista de juegos sigue creciendo, quieres que los usuarios puedan filtrarla por categoría y editor. En el ejercicio anterior ya añadiste una función auxiliar para los editores. Ahora completarás con el modo de agente de Copilot el resto del trabajo en la capa de datos, la interfaz de usuario y las pruebas.

## Ejecuta el sitio web de Tailspin Toys

Antes de hacer cambios, explora el sitio web de Tailspin Toys para conocer su funcionalidad actual.

El sitio es una plataforma de financiación colectiva de juegos de mesa con temática de desarrollo. Permite mostrar los juegos y sus detalles. Es una aplicación Astro que genera páginas HTML estáticas durante la compilación. Las páginas consultan directamente una base de datos SQLite local mediante Drizzle ORM en su frontmatter; no hay una API de backend independiente ni un framework de interfaz de usuario en el cliente. Las funciones reutilizables de acceso a datos se encuentran en `src/lib/`, y la interactividad se añade mediante un pequeño `<script>` de Astro con ámbito y API DOM estándar.

### Inicia el sitio web

Para facilitar la ejecución del sitio, se ha proporcionado la tarea `npm run dev`, que inicia un único servidor de desarrollo de Astro. Puedes ejecutarla en GitHub Codespace siguiendo estos pasos:

1. Vuelve a tu codespace. Después del ejercicio anterior deberías estar en `main`.
2. Abre un terminal en el Codespace con <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Crea y selecciona una rama nueva para este trabajo de filtrado:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Ejecuta este comando para iniciar el sitio:

   ```bash
   npm run dev
   ```

   Cuando el servidor de desarrollo de Astro esté listo, aparecerá un mensaje con la URL, parecido a este:

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> Si aparece un cuadro de diálogo que te pregunta si quieres abrir un navegador en `http://localhost:4321`, ciérralo seleccionando **x**.

5. Mantén pulsada la tecla <kbd>Command</kbd> (Mac) o <kbd>Ctrl</kbd> (Windows/Linux) y selecciona la dirección del servidor Astro `http://localhost:4321` en el terminal.

> [!NOTE]
> En Codespaces, al seleccionar el enlace localhost en el terminal, se te redirige automáticamente a `https://<your-codespace-name>-4321.app.github.dev/`. Se trata de un túnel privado a tu codespace, que ahora hospeda el servidor web.

### Explora el sitio web

Cuando el sitio esté en funcionamiento, podrás explorar sus funciones principales:

- **Página principal**: muestra juegos de mesa con sus títulos, imágenes y descripciones.
- **Página de detalles del juego**: al seleccionar un juego, se abre una página con más información, como el título, la descripción, el editor y la categoría.

## Explora el backlog con Copilot

> [!TIP]
> **Abre Copilot Chat**
>
> Antes de empezar los siguientes ejercicios, vuelve al codespace, abre el panel Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. El modo y el modelo varían según el ejercicio; cada paso lo indicará cuando sea relevante.

La implementación inicial del sitio funciona, pero queremos añadir más funcionalidades. Empecemos por revisar el backlog. Al crear el proyecto a partir de la plantilla se generaron incidencias automáticamente. Pide a GitHub Copilot que te muestre esos elementos.

1. Selecciona **Agent** en el selector de agentes de la vista Chat. El agente **Agent** planifica e implementa cambios de forma autónoma en varios archivos, ejecuta comandos de terminal e invoca herramientas.

   ![Captura del selector de agentes en la vista Chat.](../../../_images/shared-chat-mode-selector.png)

2. Selecciona **Claude Sonnet 4.5** en la lista de modelos disponibles.

> [!CAUTION]
> Los autores de este taller no muestran preferencia por un modelo concreto. Durante su desarrollo usamos Claude Sonnet 4.5, por lo que lo indicamos para que las sugerencias sean relativamente uniformes y la experiencia sea más sencilla. Sin embargo, los modelos de lenguaje grandes son probabilísticos y las sugerencias pueden diferir de las descritas en el taller. Es normal.

> [!NOTE]
> Como los modelos de lenguaje grandes son probabilísticos, Copilot podría usar un comando MCP diferente, pero debería poder completar la tarea.

3. Pide a Copilot que muestre las incidencias del backlog con este prompt:

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. Selecciona **Continue** para ejecutar el comando que enumera las incidencias.
5. Revisa la lista generada.

Observa que Copilot ha priorizado los elementos según lo que considera más útil para los usuarios.

## Revisa los archivos de instrucciones

Antes de pedir al agente que genere el código, revisa el archivo de instrucciones que proporcionará contexto a Copilot. Usarás el archivo de [interfaz de usuario (UI)](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md), que explica cómo añadir funciones al sitio web.

1. En tu codespace, abre `.github/instructions/ui.instructions.md`.
2. Fíjate en las directrices generales para añadir funcionalidad:
   - una descripción general de la arquitectura.
   - principios de diseño de componentes, capacidad de prueba y accesibilidad.
   - enlaces a archivos de instrucciones específicos para distintos tipos de archivos, como Astro, Tailwind CSS y Drizzle.

> [!TIP]
> Los archivos de instrucciones pueden hacer referencia a otros archivos de instrucciones y a archivos del proyecto. Las rutas son relativas a la ubicación del archivo de instrucciones. Así se pueden reutilizar directrices, dividir conjuntos grandes en archivos más manejables y señalar ejemplos y plantillas a Copilot.

## Implementa la funcionalidad de filtrado

Para completar el filtrado, tendrás que hacer al menos tres cambios distintos en la aplicación:

- añadir o ajustar la lógica de filtrado restante en la capa de datos (`src/lib/`).
- añadir o actualizar las pruebas del comportamiento del filtrado.
- actualizar la página con la lista de juegos para incluir la interfaz de filtrado.

También hay que ejecutar las pruebas y confirmar que se superan antes de combinar los cambios. El modo de agente de Copilot puede encargarse de estas tareas.

1. Puedes continuar la conversación actual con Copilot o seleccionar **New Chat**.
2. Selecciona **Add Context**, **Instructions** y **ui** como archivo de instrucciones.

   ![Captura de cómo seleccionar el archivo de instrucciones de la interfaz de usuario](../../../_images/ex3-select-instructions-file.png)

3. Confirma que **Agent** sigue seleccionado en el selector de agentes de la vista Chat.

   ![Captura del selector de agentes en la vista Chat.](../../../_images/shared-chat-mode-selector.png)

4. Confirma que el modelo seleccionado sigue siendo **Claude Sonnet 4.5**.
5. Pide a Copilot que implemente la funcionalidad de acuerdo con la incidencia correspondiente del backlog:

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Observa cómo Copilot explora el proyecto y localiza los archivos pertinentes. Debería encontrar tanto las funciones auxiliares de la capa de datos como la interfaz y las pruebas. Después, modificará los archivos y ejecutará las pruebas.

   ![Captura de Copilot explorando archivos del proyecto](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot realizará varias tareas, como explorar el proyecto, modificar archivos y ejecutar pruebas. El proceso puede tardar unos minutos según la complejidad de la tarea y del código base. Mientras trabaja, quizá veas los controles **Keep** y **Undo** en el editor. Cuando termine, tendrás estas opciones para cada cambio; no hace falta seleccionarlas mientras el trabajo siga en curso.

7. Cuando Copilot lo solicite, selecciona **Continue** para ejecutar las pruebas.

   ![Captura de un cuadro de diálogo de Copilot Chat que pide permiso para ejecutar pruebas](../../../_images/ex3-agent-mode-run-tests.png)

8. Puede que haya pausas e incluso que algunas pruebas fallen durante el proceso. No pasa nada: Copilot alterna entre generar código y ejecutar pruebas hasta completar la tarea y dejar de detectar errores.

   ![Captura de una sesión completa de Copilot Agent Mode](../../../_images/ex3-agent-mode-proposed-changes.png)

9. Explora el código generado para detectar posibles problemas.

> [!CAUTION]
> Recuerda que siempre es importante revisar el código generado por Copilot o por cualquier otra herramienta de IA.

10. Vuelve al navegador donde se está ejecutando el sitio y explora la nueva funcionalidad.
11. Cuando hayas confirmado que todo funciona y revisado el código, selecciona **Keep** en la ventana de Copilot Chat.

## Resumen y próximos pasos

¡Enhorabuena! En este ejercicio has aprendido a usar el modo de agente de GitHub Copilot para añadir funciones al sitio web de Tailspin Toys. Hemos visto que:

- el modo de agente puede implementar nuevas funciones en la interfaz y la capa de datos.
- el modo de agente puede explorar el proyecto, identificar archivos y coordinar cambios.
- es importante revisar los cambios y las pruebas antes de combinarlos en el código base.

A continuación, [probarás la funcionalidad con el servidor Playwright MCP][next-lesson] y abrirás una pull request.

### Ejercicio de exploración adicional: implementar paginación

Cuando crezca la lista de juegos, será necesario habilitar la paginación. Usa lo que has aprendido para pedir a Copilot que añada esta función. Ten en cuenta lo siguiente:

- sigue las prácticas recomendadas y usa los archivos de instrucciones existentes.
- decide cómo quieres implementar la paginación: por ejemplo, si el usuario podrá elegir el tamaño de página o si será fijo.
- al redactar el prompt, proporciona a Copilot las directrices necesarias para crear la implementación que quieres.
- quizá tengas que iterar con GitHub Copilot y pedir cambios o proporcionar más contexto. Es lo habitual al trabajar con Copilot.

## Recursos

- [Modos ask, edit y agent de Copilot: diferencias y usos][choose-mode]
- [Modo de agente en VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
