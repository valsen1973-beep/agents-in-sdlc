---
title: "Lección 8 - Crea y combina la PR de la funcionalidad"
description: "Revisa el filtrado, las instrucciones, la actualización de la habilidad, el perfil de QA y las pruebas; después, crea una PR y usa Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

La implementación del filtrado, las actualizaciones de instrucciones, la actualización de la habilidad, el perfil de control de calidad (QA) y las pruebas están guardados en una rama. Es hora de revisarlos juntos y abrir una pull request. Combinaste manualmente la pull request (PR) de las valoraciones con estrellas; esta vez dejarás que **Agent Merge** gestione el proceso.

> [!NOTE]
> Lo habitual sería separar la funcionalidad, las actualizaciones de instrucciones, la actualización de la habilidad y el agente de QA en varias PR. Para simplificar el taller, has mantenido el flujo completo de filtrado y calidad en una conversación y una rama, y todo ese trabajo se incluirá en esta PR.

En esta lección:

- aprenderás qué es Agent Merge y cómo automatiza el ciclo de vida de una combinación.
- inspeccionarás todos los cambios de la funcionalidad y las pruebas de verificación.
- crearás la PR del filtrado.
- activarás Agent Merge solo después de la revisión y confirmarás que la PR se ha combinado.

## Situación

A lo largo del flujo de trabajo de filtrado has usado Copilot para planificar, implementar y verificar una funcionalidad. Tailspin Toys quiere automatizar el trabajo restante de la PR sin quitar al desarrollador el control sobre la autorización de la combinación.

## Presentación de Agent Merge

**Agent Merge** automatiza el trabajo que falta para integrar una pull request. Al activarlo, Copilot resuelve los bloqueos de la PR —corrige comprobaciones de integración continua (CI) fallidas, responde a comentarios de revisión y vuelve a aplicar los cambios cuando es necesario— y, después, activa la combinación automática de GitHub si el repositorio lo permite.

Hasta ahora has seleccionado **Combinar pull request** manualmente. Agent Merge puede encargarse de esa tarea. Revisa el trabajo y confirma que está listo antes de activarlo.

## Usa Agent Merge para gestionar la PR

Ya has creado el código. Revisémoslo, creemos la PR y dejemos que Agent Merge gestione el resto.

1. Vuelve a tu Codespace.
2. Abre el cuadro de diálogo del agente con `/agent`.
3. Selecciona **Default** en la lista y pulsa <kbd>Enter</kbd>.
4. Crea una PR nueva con el comando `/pr create`.
5. Activa Agent Merge con `/pr agentmerge`.
6. Copilot supervisará la integración continua de la PR. Cuando todas las comprobaciones se superen, realizará la combinación.
7. Comprueba que Copilot muestra un mensaje parecido a «PR #14 was squash-merged successfully».

> [!IMPORTANT]
> Agent Merge no omite las aprobaciones obligatorias, la protección de ramas, las colas de combinación, la configuración del repositorio ni los permisos que falten. Si se bloquea, lee el motivo y realiza manualmente la combinación revisada cuando el repositorio lo permita.

## Resumen y próximos pasos

Has automatizado varias partes del proceso de desarrollo: generar código, probarlo y validarlo, y gestionar las pull requests. En esta lección:

- aprendiste qué es Agent Merge y cómo automatiza el ciclo de vida de una combinación.
- inspeccionaste todos los cambios de la funcionalidad y las pruebas de verificación.
- creaste la PR del filtrado.
- activaste Agent Merge solo después de la revisión y confirmaste que la PR se había combinado.

A continuación, [explorarás otros comandos de barra útiles de Copilot CLI][next-lesson] para gestionar el contexto y los modelos, compartir sesiones y delegar trabajo opcionalmente en la nube.

## Recursos

- [Gestionar pull requests con Copilot CLI][manage-prs]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
