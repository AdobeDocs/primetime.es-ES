---
seo-title: Habilitar la demostración del modelo de uso
title: Habilitar la demostración del modelo de uso
uuid: 43930ebb-e936-4f48-990d-7ad19992e326
translation-type: tm+mt
source-git-commit: 6e949c2f88deef88f0d0ac95b18c006da1c89d2f

---


# Habilitar la demostración del modelo de uso{#enable-the-usage-model-demo}

1. Especifique la propiedad personalizada `RI_UsageModelDemo=true` en el momento del empaquetado.

   Si va a empaquetar contenido con la herramienta de línea de comandos de Media Packager, introduzca:

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Si no activa el modo de demostración opcional en el momento del empaquetado, el servidor de licencias emite una licencia basada en la primera directiva DRM válida que procesa.

