---
title: "Lección 12 - Publicar el sitio con GitHub Pages"
description: "Usa la aplicación GitHub Copilot para configurar un flujo de trabajo de Pages, revisar su pull request y verificar que Space Quiz está disponible."
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

Publica Space Quiz para que todo el mundo pueda acceder. Copilot puede preparar el flujo de trabajo y guiar la publicación, pero tú eres responsable de revisar los cambios y confirmar que el sitio está disponible.

En esta lección:

- pedirás a Copilot que configure una publicación en GitHub Pages.
- revisarás el flujo de trabajo y la pull request antes de combinarla.
- seguirás el proceso de publicación y verificarás el sitio publicado.

## Situación

Space Quiz ya está en un repositorio de GitHub, pero a la gente todavía le falta una forma sencilla de probarlo. Publicar el sitio de un solo archivo con GitHub Pages permite acceder a él mediante una URL pública sin añadir un servidor ni dependencias de ejecución.

## Pide a Copilot que prepare la publicación

> [!WARNING]
> Crear una pull request puede confirmar y enviar código. Revisa la configuración de aprobación y el repositorio de destino antes de enviar este prompt. Si está seleccionada la opción **Aprobar todo**, no esperes otro aviso de confirmación.

En la sesión de la aplicación Copilot para `space-quiz`, envía este prompt:

```plaintext
Prepare a GitHub Pages deployment for this repository. Create a GitHub Actions workflow that builds the website if needed and deploys it to GitHub Pages after changes reach the default branch. Add a README describing the app and how to run it locally if one does not already exist. Create a pull request with these changes and report its link and any required Pages settings or permissions. Do not merge, enable auto-merge, change Pages settings, or deploy. Stop and wait for my review.
```

## Revisa el flujo de trabajo y la pull request

1. Confirma que el archivo README solo se añade si el repositorio aún no tiene uno.
2. Revisa los cambios de la pull request, incluidos los pasos de compilación y publicación del flujo de trabajo, sus activadores y permisos.
3. Confirma que el flujo de trabajo publica desde la rama predeterminada, no desde una pull request que aún no se ha combinado.
4. Solicita las correcciones necesarias y revisa las diferencias actualizadas. Espera a que se superen las comprobaciones obligatorias de la pull request antes de autorizar la combinación.

## Autoriza la combinación y la publicación

> [!WARNING]
> El siguiente prompt autoriza al agente a combinar la pull request revisada, cambiar la configuración de Pages del repositorio y publicar el sitio. Envíalo solo después de completar la revisión y confirmar el repositorio y la pull request. Según la configuración de aprobación, estas acciones podrían realizarse sin otro aviso.

Sustituye `<PR_NUMBER>` por el número de la pull request que has revisado y envía este prompt por separado:

```plaintext
I have reviewed pull request <PR_NUMBER> in this repository and authorize its merge and deployment. Enable GitHub Pages using GitHub Actions, merge that pull request only after required checks pass, and monitor the deployment until it succeeds. Report the final URL of the live website. If you lack permission to enable Pages or merge, tell me exactly what I need to approve or do; do not report success until the site is live.
```

![Diagrama de tres fases: una pull request de space-quiz combinada; una ejecución correcta de Deploy website en GitHub Actions con los pasos Build website, Upload artifact y Deploy to Pages; y Space Quiz publicado en yourname.github.io/space-quiz/.](../../../_images/first-steps-app-pages-deploy.svg)

## Verifica la publicación

1. Sigue la ejecución de publicación de GitHub Actions hasta que finalice correctamente.
2. Abre la URL proporcionada y confirma que Space Quiz se carga.

Si el agente no puede habilitar Pages o combinar la pull request, sigue las instrucciones concretas que te proporcione. No des la tarea por terminada hasta que la publicación finalice correctamente y el sitio esté disponible.

## Resumen y próximos pasos

Space Quiz ya está publicado y has comprobado que funciona, en lugar de confiar únicamente en el informe del agente. Continúa con la [lección 13: Revisión y próximos pasos][next-lesson].

[next-lesson]: ../13-review/
