---
title: Incrustación de licencias
description: Incrustación de licencias
copied-description: true
exl-id: 63b1bf18-b93d-4305-885a-3a9eee783a03
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Incrustación de licencias {#embedding-licenses}

Una vez que el contenido se ha cifrado y se ha generado previamente una licencia, esta puede incrustarse en el contenido cifrado.

Para incrustar una licencia, obtenga una instancia de `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Si conoce el tipo de contenido cifrado, utilice el constructor para `FLVKeyMetaDataUpdater` o `F4VKeyMetaDataUpdater`; de lo contrario, utilice `MediaProcessorFactory.getMediaProcessor()` para devolver una instancia basada en el tipo de archivo detectado. Construir un `KeyMetaDataCallback` e invocar `modifyKeyMetaData()`. La implementación de devolución de llamada se invocará cuando los metadatos DRM se encuentren en el contenido cifrado. En función de los metadatos encontrados, puede elegir una licencia para incrustar y establecer la licencia mediante `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Para ver el código de ejemplo que muestra las licencias incrustadas, consulte `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` en el directorio &quot;Samples&quot; de las herramientas de línea de comandos de implementación de referencia.

>[!NOTE]
>
>Los clientes de Adobe Access 2.0 ignorarán las licencias incrustadas en el contenido e intentarán obtener una licencia del servidor de licencias especificado en los metadatos. Sin embargo, si los metadatos indican que no hay ningún servidor de licencias disponible, un cliente de Adobe Access 2.0 deberá actualizar para ver el contenido.

Consulte [Licencias fuera de banda](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md).
