---
title: Habilitar la demostración del modelo de uso
description: Habilitar la demostración del modelo de uso
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---


# Habilitar la demostración del modelo de uso{#enable-the-usage-model-demo}

1. Especifique la propiedad personalizada `RI_UsageModelDemo=true` en el momento del empaquetado.

   Si empaqueta contenido con la herramienta de línea de comandos de Media Packager, introduzca:

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE]
>
>Si no activa el modo de demostración opcional en el momento del empaquetado, el servidor de licencias emite una licencia basada en la primera directiva DRM válida que procesa.

