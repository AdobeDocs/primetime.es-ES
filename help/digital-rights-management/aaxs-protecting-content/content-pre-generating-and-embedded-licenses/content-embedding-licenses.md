---
seo-title: Incrustación de licencias
title: Incrustación de licencias
uuid: b8d8ee9b-7430-4899-9caf-47d6b64021b8
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Incrustación de licencias {#embedding-licenses}

Una vez que el contenido se ha cifrado y se ha generado previamente una licencia, ésta puede incrustarse en el contenido cifrado.

Para incrustar una licencia, obtenga una instancia de `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Si conoce el tipo de contenido cifrado, utilice el constructor para `FLVKeyMetaDataUpdater` o `F4VKeyMetaDataUpdater`; en caso contrario, utilice `MediaProcessorFactory.getMediaProcessor()` para devolver una instancia basada en el tipo de archivo detectado. Construya un `KeyMetaDataCallback` e invoque `modifyKeyMetaData()`. La implementación de llamada de retorno se invocará cuando los metadatos de DRM se encuentren en el contenido cifrado. En función de los metadatos encontrados, puede elegir una licencia para incrustar y establecer la licencia mediante `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Para obtener un código de muestra que muestre las licencias incrustadas, consulte `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` en el directorio Reference Implementation Command Line Tools &quot;Samples&quot; (Ejemplos).

>[!NOTE]
>
>Los clientes de Adobe Access 2.0 ignorarán todas las licencias incrustadas en el contenido e intentarán obtener una licencia del servidor de licencias especificado en los metadatos. Sin embargo, si los metadatos indican que no hay ningún servidor de licencias disponible, un cliente de Adobe Access 2.0 tendrá que actualizarse para realizar la vista del contenido.

Consulte Licencias [fuera de banda](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md).
