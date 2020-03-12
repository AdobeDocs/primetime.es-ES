---
seo-title: Habilitar la demostración del modelo de uso
title: Habilitar la demostración del modelo de uso
uuid: 43930ebb-e936-4f48-990d-7ad19992e326
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Habilitar la demostración del modelo de uso{#enable-the-usage-model-demo}

1. Especifique la propiedad personalizada `RI_UsageModelDemo=true` en el momento del empaquetado.

   Si va a empaquetar contenido con la herramienta de línea de comandos de Media Packager, introduzca:

   ```
   java -jar AdobeMediaPackager.jar [
   
<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true

```
>[!NOTE] {class="- topic/note "}
>
>If you do not activate the optional demo mode at packaging time, the license server issues a license based on the first valid DRM policy it processes.

