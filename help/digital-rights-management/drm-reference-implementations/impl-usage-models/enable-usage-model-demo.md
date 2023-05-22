---
title: Habilitar la demostración del modelo de uso
description: Habilitar la demostración del modelo de uso
copied-description: true
exl-id: 5d546f1a-ebf6-4c93-9a73-fa812cd71086
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---

# Habilitar la demostración del modelo de uso{#enable-the-usage-model-demo}

1. Especificar la propiedad personalizada `RI_UsageModelDemo=true` en el momento del embalaje.

   Si está empaquetando contenido mediante la herramienta de línea de comandos de Media Packager, introduzca:

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE]
>
>Si no activa el modo de demostración opcional en el momento del empaquetado, el servidor de licencias emite una licencia basada en la primera directiva DRM válida que procese.
