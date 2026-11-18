---
title: "Ejercicio 3 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## ¿Qué son los agentes personalizados?

Los [agentes personalizados][custom-agents-concept] de GitHub Copilot permiten crear asistentes de IA especializados para tareas o dominios concretos de tu flujo de desarrollo. Al definir agentes en archivos Markdown en la carpeta `.github/agents` del repositorio, proporcionas a Copilot instrucciones, prácticas recomendadas, patrones de programación y conocimientos específicos que le ayudan a realizar ciertos tipos de trabajo con mayor eficacia. Los equipos pueden convertir sus conocimientos en agentes reutilizables: uno de accesibilidad que aplique las directrices de [WCAG][wcag], uno de seguridad que siga prácticas de programación segura o uno de pruebas que mantenga patrones coherentes.

Los agentes personalizados se definen en archivos Markdown de la carpeta `.github/agents` del proyecto o, de forma global, en `~/.copilot/agents`. Cada archivo tiene un frontmatter YAML con, al menos, los campos `name` y `description`, seguido de un prompt Markdown que define el comportamiento, los conocimientos y las instrucciones del agente.

### Diferencias entre los agentes personalizados y las habilidades de agente

Los agentes personalizados y las [habilidades de agente][agent-skills-concept] tienen algunos aspectos en común: ambos se definen principalmente mediante archivos Markdown e indican a una IA cómo realizar ciertas operaciones. La forma más sencilla de distinguirlos es que un **agente personalizado** es quien realiza el trabajo, mientras que las **habilidades** son herramientas.

Los agentes personalizados disponen de su propia ventana de contexto y están diseñados para coordinar habilidades (e incluso otros agentes) durante el trabajo. En este taller, el agente personalizado de accesibilidad revisará el sitio y lo actualizará conforme a las directrices de accesibilidad. Durante ese trabajo podría usar habilidades, por ejemplo, una para el flujo de pull requests o para ejecutar y gestionar pruebas.

> [!NOTE]
> No hay una única forma correcta de crear agentes personalizados. Como con cualquier tecnología de IA, prueba distintas opciones e itera para encontrar la que mejor se adapte a tus entornos y situaciones.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

En esta lección explorarás cómo se definen los agentes personalizados y cómo se les asigna una tarea.

## Situación

Tailspin Toys se compromete a que todas las personas puedan usar su plataforma de financiación colectiva, independientemente de sus capacidades o preferencias visuales. Los comentarios recientes han señalado que a algunos usuarios les cuesta leer el tema oscuro actual debido al bajo contraste entre el texto y el fondo. Para resolver este problema de accesibilidad, el equipo de diseño ha solicitado un modo de alto contraste que los usuarios puedan activar y desactivar.

Como la accesibilidad es fundamental, quieres implementar esta mejora cuanto antes. Para ello, usarás un agente personalizado.

## Revisa el agente personalizado de accesibilidad

Ya se ha creado un agente personalizado de accesibilidad. Revisemos su contenido para entender cómo guía a Copilot.

Vuelve a tu codespace y abre el archivo del agente personalizado de accesibilidad:

1. Abre `.github/agents/accessibility.md`.
2. Observa los campos `name` y `description` del frontmatter YAML.

> [!CAUTION]
> El frontmatter con `name` y `description` es obligatorio para los agentes personalizados.

3. Lee las secciones siguientes, que describen:
   - las responsabilidades principales al generar código para un sitio web accesible.
   - las prácticas recomendadas de accesibilidad.
   - ejemplos de código HTML, CSS y JavaScript.
   - errores y problemas habituales.

## Crea y asigna una incidencia

El panel de agentes es el centro de control de todos los agentes de tu entorno. Desde allí puedes asignar tareas al agente en la nube de Copilot, supervisarlas e incluso redirigir y proporcionar más contexto. Empecemos por asignar a Copilot una tarea para crear el modo de alto contraste.

1. Abre tu repositorio.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el cuadro de diálogo de nueva incidencia.
4. Selecciona **Blank issue**.
5. Escribe `Add high contrast mode to website` en el campo **Title**.
6. En el campo **Description**, escribe:

    ```plaintext
    We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
    ```

7. Selecciona **Create** para crear la incidencia.
8. En el lado derecho, selecciona **Assign to Copilot** para abrir el cuadro de diálogo de asignación.
9. Selecciona **Accessibility agent** en la lista de agentes personalizados.

    ![Captura de la asignación del agente en la nube, con los campos del agente personalizado y de accesibilidad resaltados](../../../_images/ex5-select-custom-agent.png)

10. Selecciona **Assign**.
11. Copilot empezará a trabajar en segundo plano.

## Resumen y próximos pasos

En esta lección has explorado los [agentes personalizados][custom-agents] de GitHub Copilot, asistentes especializados en tareas y dominios concretos. Los agentes personalizados permiten convertir los conocimientos y estándares del equipo en agentes reutilizables que guían a Copilot para realizar ciertos tipos de trabajo con mayor eficacia.

Has aprendido:

- cómo se definen los agentes personalizados.
- cómo asignar una tarea a un agente personalizado.

Mientras Copilot trabaja en el modo de alto contraste, puedes [supervisar y guiar la sesión del agente][next-lesson] desde el panel de agentes.

## Recursos

- [Acerca de los agentes personalizados][custom-agents]
- [Preparar la organización para usar agentes personalizados][org-custom-agents]
- [Preparar la empresa para usar agentes personalizados][enterprise-custom-agents]

---

| [← Lección anterior: Agente en la nube de GitHub Copilot][previous-lesson] | [Siguiente lección: Supervisa y gestiona agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
