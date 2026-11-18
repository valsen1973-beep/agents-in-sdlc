---
title: "Lección 10 - Resumen y próximos pasos"
description: "Repasa el flujo de trabajo con Copilot CLI, las dos pull requests, las personalizaciones reutilizables y otros recursos."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Has utilizado GitHub Copilot CLI a lo largo de un flujo de trabajo completo para Tailspin Toys. En concreto:

- preparaste un Codespace, instalaste Copilot CLI, exploraste el proyecto y encontraste la incidencia de filtrado del backlog.
- añadiste valoraciones con estrellas, revisaste el resultado en un navegador reenviado y combinaste manualmente tu primera pull request (PR).
- partiste de la incidencia de filtrado, definiste el enfoque con el modo Plan, lo implementaste con Autopilot y lo revisaste en el modo Interactive.
- guiaste al agente mediante instrucciones personalizadas, personalizaste la habilidad `quality-checks` y la usaste para ejecutar pruebas unitarias, lint y comprobaciones de tipos.
- añadiste el servidor Playwright Model Context Protocol (MCP) y lo usaste para explorar el filtrado en un navegador real.
- creaste y seleccionaste un agente personalizado de control de calidad (QA) para evaluar los requisitos, la cobertura, los resultados de la habilidad y las pruebas en el navegador.
- revisaste el cambio completo de filtrado y autorizaste Agent Merge para combinar su PR.
- exploraste comandos de barra para gestionar el contexto y los modelos, compartir contenido y delegar trabajo opcionalmente en la nube.

## Lo que has publicado

El taller incluye dos hitos de PR, cada uno en su propia rama basada en la versión actualizada de `main`:

1. **Valoraciones con estrellas:** muestra el `starRating` existente y un estado explícito para los juegos sin valorar en las tarjetas.
2. **Filtrado y flujo de trabajo de calidad:** implementa el filtrado, actualiza las instrucciones y las aplica a la funcionalidad, personaliza el informe de `quality-checks`, crea un perfil de QA e incluye las pruebas relacionadas.

Has utilizado la misma conversación y rama desde la planificación del filtrado hasta la creación de su PR. Hemos agrupado ese trabajo en una PR para simplificar el taller.

## Distintos tipos de verificación

Has comprobado el código de varias formas: con pruebas automatizadas, con tu propia inspección en el navegador y con la exploración del navegador mediante MCP de Copilot. La habilidad `quality-checks` ha ejecutado pruebas unitarias, lint y comprobaciones de tipos, y ha incluido los resultados en el nuevo formato. El agente de QA ha reunido esos resultados con una revisión de los requisitos y la cobertura antes de la PR.

Las pruebas nuevas deben cubrir carencias reales; si una ejecución de QA no requiere nuevas pruebas, puede ser correcto. Revisa el código y las pruebas antes de autorizar la combinación, y actualiza las pruebas afectadas después de hacer cambios.

## Prácticas recomendadas

El contexto y las herramientas que proporcionas influyen en el trabajo de Copilot. En este taller has actualizado instrucciones, personalizado una habilidad, creado un perfil de QA y configurado un servidor MCP. Reutiliza estas personalizaciones en distintas conversaciones y ajústalas a las necesidades del equipo. Las instrucciones establecen estándares, las habilidades describen tareas repetibles, los agentes personalizados definen roles especializados y los servidores MCP conectan herramientas externas. Revisa los cambios reales y los resultados de las herramientas, no solo el resumen del agente.

Adapta el **modo y el modelo** a la tarea. Usa **Plan** para pensar en un enfoque antes de implementarlo, **Interactive** para seguir de cerca los cambios concretos y **Autopilot** para las tareas bien acotadas. Elige un modelo más rápido para cambios rutinarios y otro más capaz para trabajos complejos.

El contexto sigue siendo tan importante como la infraestructura. Describir con claridad *qué* quieres crear, *por qué* y *cómo* influye de forma importante en el resultado.

## Más posibilidades

Ya has completado el flujo de trabajo principal. Estas son algunas funciones más de la CLI que puedes explorar:

- `/review` para pedir al agente de revisión de código que analice los cambios.
- `/rubber-duck` para explicar un problema y obtener otra perspectiva.
- `/fleet` para coordinar subtareas independientes en paralelo.
- `/worktree` para aislar otra tarea.
- `/delegate` para enviar una tarea al agente en la nube de Copilot.

## Próximos pasos

La mejor forma de aprender a usar cualquier herramienta es seguir utilizándola. Úsala con código de producción, en proyectos personales o para crear esa pequeña aplicación que llevas años imaginando. Comparte lo que aprendas con el equipo y aprende de sus experiencias. Y, como siempre, explora la documentación.

Si quieres ampliar Tailspin Toys desde el terminal, continúa con la serie opcional [Foundry Backer Concierge][foundry]. Para comparar otros entornos, explora el [taller de VS Code][vscode], el [taller de la aplicación GitHub Copilot][app] o el [taller del agente en la nube de Copilot][cloud].

## Recursos

- [Acerca de GitHub Copilot CLI][about-cli]
- [Referencia de comandos de Copilot CLI][cli-reference]
- [Personalizar Copilot CLI][customize-cli]
- [Gestionar pull requests con Copilot CLI][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
