---
title: Incrustación de licencias
description: Incrustación de licencias
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Incrustación de licencias {#embedding-licenses}

Una vez que el contenido se ha cifrado y se ha generado previamente una licencia, esta puede incrustarse en el contenido cifrado.

Si desea incrustar una licencia, debe obtener una instancia de `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Si conoce el tipo del contenido cifrado, utilice el constructor para `FLVKeyMetaDataUpdater` o `F4VKeyMetaDataUpdater`; de lo contrario, utilice `MediaProcessorFactory.getMediaProcessor()` para devolver una instancia basada en el tipo de archivo detectado. A continuación, debe construir un `KeyMetaDataCallback` e invocar `modifyKeyMetaData()`. A continuación, se invoca la implementación de la rellamada cuando los metadatos de DRM se encuentran en el contenido cifrado. Según los metadatos encontrados, puede elegir una licencia para incrustar y establecer la licencia utilizando `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Consulte `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` en el directorio Herramientas [!DNL Samples] de la línea de comandos de implementación de referencia para obtener código de ejemplo que demuestre las licencias incrustadas.

>[!NOTE]
>
>Un cliente de Adobe Primetime DRM 2.0 ignora cualquier licencia incrustada en el contenido y luego intenta obtener una licencia del servidor de licencias especificado en los metadatos. Sin embargo, si los metadatos indican que no hay ningún servidor de licencias disponible, es necesario actualizar un cliente de Primetime DRM 2.0 para poder ver el contenido.

