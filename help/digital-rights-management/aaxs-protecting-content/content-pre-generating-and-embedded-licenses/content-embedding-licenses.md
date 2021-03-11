---
title: Incrustación de licencias
description: Incrustación de licencias
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Incrustación de licencias {#embedding-licenses}

Una vez que el contenido se ha cifrado y se ha generado previamente una licencia, esta puede incrustarse en el contenido cifrado.

Para incrustar una licencia, obtenga una instancia de `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Si conoce el tipo del contenido cifrado, utilice el constructor para `FLVKeyMetaDataUpdater` o `F4VKeyMetaDataUpdater`; de lo contrario, utilice `MediaProcessorFactory.getMediaProcessor()` para devolver una instancia basada en el tipo de archivo detectado. Construya un `KeyMetaDataCallback` e invoque `modifyKeyMetaData()`. La implementación de la rellamada se invocará cuando los metadatos de DRM se encuentren en el contenido cifrado. Según los metadatos encontrados, puede elegir una licencia para incrustar y establecer la licencia utilizando `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Para obtener un ejemplo de código que demuestre las licencias incrustadas, consulte `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` en el directorio &quot;Muestras&quot; de las herramientas de la línea de comandos de implementación de referencia.

>[!NOTE]
>
>Los clientes de Adobe Access 2.0 ignorarán cualquier licencia incrustada en el contenido e intentarán obtener una licencia del servidor de licencias especificado en los metadatos. Sin embargo, si los metadatos indican que no hay ningún servidor de licencias disponible, un cliente de Adobe Access 2.0 tendrá que actualizarse para ver el contenido.

Consulte [Licencias fuera de banda](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md).
