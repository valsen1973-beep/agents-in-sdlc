---
title: "Ejercicio 1 - Instrucciones personalizadas (agente en la nube)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Requisitos previos][previous-lesson] · [Siguiente lección: Agente en la nube de Copilot →][next-lesson]

El contexto es fundamental cuando se trabaja con IA generativa. Si una tarea debe realizarse de una forma concreta o Copilot necesita información adicional, conviene asegurarse de que pueda acceder a ese contexto. Los [archivos de instrucciones][instruction-files] proporcionan directrices para que Copilot entienda no solo *qué* debe hacer, sino también *cómo*.

En este ejercicio:

- explorarás cómo llegan a Copilot el contexto específico del proyecto, las directrices de programación y los estándares de documentación mediante las instrucciones personalizadas del repositorio y los archivos de instrucciones específicos de rutas.
- añadirás un nuevo estándar general del repositorio a `.github/copilot-instructions.md`.

> [!NOTE]
> A diferencia de los itinerarios de VS Code y CLI, aquí no compararás el resultado de un prompt antes y después. El agente en la nube de Copilot trabaja de forma asíncrona en incidencias de GitHub, por lo que su influencia es más difícil de mostrar en tiempo real. Verás el efecto de las instrucciones más adelante, al revisar las pull requests del agente.

## Archivos de instrucciones

### Situación

Como cualquier empresa de desarrollo, Tailspin Toys tiene directrices y requisitos para las prácticas de desarrollo. Entre ellos:

- La capa de datos siempre debe tener pruebas unitarias.
- La interfaz de usuario debe usar un tema oscuro y un diseño moderno.
- El código debe incluir documentación en forma de comentarios TSDoc.
- Cada archivo debe empezar con un bloque de comentarios que describa su contenido.

Con los archivos de instrucciones, proporcionarás a Copilot la información necesaria para que realice las tareas conforme a estas prácticas.

### Instrucciones personalizadas

Las instrucciones personalizadas proporcionan a Copilot contexto y preferencias para que comprenda mejor tu estilo y tus requisitos de programación. Esta función te ayuda a obtener sugerencias y fragmentos de código más pertinentes. Puedes especificar las convenciones de programación, las bibliotecas y los comentarios que prefieres. Puedes crear instrucciones para todo el repositorio o para tipos concretos de archivos y tareas.

Hay dos tipos de archivos de instrucciones:

- `.github/copilot-instructions.md` es un único archivo que se envía a Copilot **en todas** las solicitudes del repositorio. Debe contener información de nivel de proyecto pertinente para la mayoría de las solicitudes, como la pila tecnológica, una descripción general de lo que se está creando, las prácticas recomendadas y otras directrices globales.
- Los archivos `.github/instructions/*.instructions.md` pueden crearse para tareas o tipos de archivos concretos. Permiten proporcionar directrices para lenguajes como TypeScript o Astro, o para tareas como crear un componente de interfaz de usuario o un nuevo conjunto de pruebas unitarias.

> [!NOTE]
> En el IDE, los archivos de instrucciones solo se usan para generar código con Copilot Chat, no para completar código ni para las sugerencias de siguiente edición.
>
> Copilot Chat, Copilot CLI y el agente en la nube de Copilot usan las instrucciones del repositorio y los archivos `*.instructions.md` (con frontmatter `applyTo`) al generar código.
>
> GitHub Copilot también [admite archivos de instrucciones en otros formatos][custom-instructions-support], como AGENTS.md y CLAUDE.md.

### Prácticas recomendadas para gestionar archivos de instrucciones

No es posible explicar aquí en detalle cómo crear archivos de instrucciones. Sin embargo, los ejemplos del proyecto muestran un enfoque representativo. En general:

- Mantén las instrucciones de `copilot-instructions.md` centradas en directrices del proyecto, como describir lo que se está creando, la estructura del proyecto y los estándares generales de programación.
- Usa los archivos `*.instructions.md` para directrices específicas de tipos de archivos (pruebas unitarias, componentes Astro, capa de datos) o tareas concretas.
- Escribe en lenguaje natural. Explica las directrices con claridad e incluye ejemplos del código que se debe usar y del que se debe evitar.

No hay una única forma de crear archivos de instrucciones, del mismo modo que no hay una única forma de usar IA. La experimentación te permitirá encontrar el enfoque adecuado para tu proyecto.

> [!TIP]
> Todos los proyectos que usan GitHub Copilot deberían tener un conjunto sólido de archivos de instrucciones. Al explorar este proyecto, quizá encuentres archivos para distintos tipos de tareas, como [actualizar la interfaz de usuario][ui-instructions] y [trabajar con Astro][astro-instructions].
>
> Copilot también puede ayudarte a generar archivos de instrucciones. Cada entorno ofrece esta opción de una forma distinta (por ejemplo, **Configure Chat → Generate Agent Instructions** en VS Code o `/init` en Copilot CLI). La lección correspondiente al entorno explicará cómo usarla cuando proceda.
>
> ¿Buscas plantillas o un punto de partida? Explora [awesome-copilot][awesome-copilot], un repositorio con archivos de instrucciones, agentes personalizados y otros recursos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explora los archivos de instrucciones personalizadas de este proyecto

El repositorio incluye un archivo principal `copilot-instructions.md` y varios archivos `*.instructions.md` para distintas tareas. Ábrelos en la interfaz web de GitHub o en un codespace, si ya tienes uno abierto.

1. Abre `.github/copilot-instructions.md`.
2. Explora el archivo y fíjate en la breve descripción del proyecto y en secciones como **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**. La sección **Code standards** contiene directrices para **GitHub Actions Workflows**. Se aplican a cualquier interacción con Copilot.
3. Abre la carpeta `.github/instructions` y explórala. Encontrarás instrucciones para archivos Astro, la capa de datos Drizzle, pruebas y otros elementos.
4. Abre `.github/instructions/unit-tests.instructions.md`. El campo `applyTo` de la parte superior define un patrón relativo a la raíz del repositorio que determina qué archivos coinciden. En este caso, se aplican a los archivos TypeScript de pruebas, por ejemplo, los que coincidan con `**/*.test.ts`.
5. Fíjate en las instrucciones para crear pruebas unitarias en este proyecto.
6. Por último, abre `.github/instructions/drizzle.instructions.md` y desplázate hasta el final. Observa los enlaces a otros archivos de instrucciones (como `unit-tests.instructions.md`) y a archivos existentes del proyecto. Así puedes dividir conjuntos de instrucciones grandes en archivos más pequeños y reutilizables, y señalar a Copilot ejemplos que debe seguir. (Las rutas son relativas al archivo de instrucciones, no a la raíz del repositorio).

> [!NOTE]
> La sección **Code formatting requirements** de `copilot-instructions.md` documenta los estándares de programación del proyecto, pero aún no exige documentación en el código. En los siguientes pasos añadirás reglas para comentarios TSDoc y comentarios de cabecera de archivo.

## Añade un nuevo estándar al repositorio

Este es el único cambio que harás en este ejercicio: añadir una regla general para que la documentación se incluya en el código mediante comentarios TSDoc y una cabecera de archivo. El agente en la nube la usará más adelante, cuando le asignes incidencias.

Antes de editar el archivo, crea una rama. Aunque el agente en la nube leerá las instrucciones de la rama a la que se dirija la incidencia, confirmar los cambios en una rama te permitirá mantenerlos organizados:

1. Desde el terminal del codespace, crea una rama y cámbiate a ella:

   ```bash
   git checkout -b custom-instructions-cloud
   ```

Como se explicó antes, `.github/copilot-instructions.md` proporciona a Copilot información general del proyecto. Añadamos los estándares de programación para mejorar las sugerencias de código.

1. Vuelve a abrir `.github/copilot-instructions.md`.
2. Busca la sección **Code formatting requirements**, que debería estar cerca de la línea 27. Observa que describe los estándares de programación, pero no exige documentación en el código; por eso la función auxiliar generada no incluía comentarios.
3. Añade el siguiente texto Markdown justo debajo de los estándares existentes para indicar que Copilot debe añadir una cabecera de comentarios a cada archivo y comentarios TSDoc:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Guarda `copilot-instructions.md`.

> [!TIP]
> Como has visto en la lección anterior, los archivos de instrucciones pueden crearse en el nivel del repositorio (`.github/copilot-instructions.md`) para proporcionar directrices globales, o como archivos `*.instructions.md` para lenguajes, tipos de archivos o tareas concretos. El archivo del repositorio es el lugar adecuado para estándares generales, como la regla sobre los comentarios de documentación que acabas de añadir.

## Confirma, envía y combina la actualización de instrucciones

El agente en la nube lee los archivos de instrucciones de la rama a la que se dirige la incidencia. Cuando le asignes una incidencia en el siguiente ejercicio, Copilot creará una rama a partir de `main`. Por eso, los cambios de instrucciones deben llegar a `main` para que el agente pueda usarlos.

1. Prepara y confirma los cambios:

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. Envía la rama:

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. En github.com, abre una pull request de `custom-instructions-cloud` a `main` y combínala. Así, el agente en la nube podrá leer las instrucciones cuando le asignes trabajo en el siguiente ejercicio.

> [!TIP]
> Si prefieres trabajar directamente en `main` durante este taller, puedes omitir los pasos de la rama y confirmar los cambios directamente en `main`. La rama permite practicar un flujo de trabajo habitual en un proyecto real.

## Resumen y próximos pasos

Has explorado cómo obtiene Copilot el contexto de los archivos de instrucciones y has añadido un estándar general a `.github/copilot-instructions.md`. Podrás comprobar el efecto de ese estándar en las pull requests que genere el agente en la nube durante el resto del itinerario.

A continuación, [asignarás tu primera incidencia al agente en la nube de Copilot][next-lesson].

## Recursos

- [Archivos de instrucciones para personalizar GitHub Copilot][instruction-files]
- [Prácticas recomendadas para crear instrucciones personalizadas][instructions-best-practices]
- [Cinco consejos para redactar mejores instrucciones personalizadas para Copilot][copilot-instructions-five-tips]
- [Awesome Copilot: colección de archivos de instrucciones y otros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
