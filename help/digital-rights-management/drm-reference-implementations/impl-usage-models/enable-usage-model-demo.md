---
seo-title: Habilitar la demostración del modelo de uso
title: Habilitar la demostración del modelo de uso
uuid: 43930ebb-e936-4f48-990d-7ad19992e326
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---


# Habilitar la demostración del modelo de uso{#enable-the-usage-model-demo}

1. Especifique la propiedad personalizada `RI_UsageModelDemo=true` en el momento del empaquetado.

   Si va a empaquetar contenido con la herramienta de línea de comandos de Media Packager, introduzca:

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE]
>
>Si no activa el modo de demostración opcional en el momento del empaquetado, el servidor de licencias emite una licencia basada en la primera directiva DRM válida que procesa.

