---
seo-title: Incrustación de licencias
title: Incrustación de licencias
uuid: e3d55376-07de-479c-9a53-04bc8071ced4
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Incrustación de licencias {#embedding-licenses}

Una vez que el contenido se ha cifrado y se ha generado previamente una licencia, ésta puede incrustarse en el contenido cifrado.

Si desea incrustar una licencia, debe obtener una instancia de `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Si conoce el tipo de contenido cifrado, utilice el constructor para `FLVKeyMetaDataUpdater` o `F4VKeyMetaDataUpdater`; de lo contrario, utilice `MediaProcessorFactory.getMediaProcessor()` para devolver una instancia basada en el tipo de archivo detectado. Luego debe construir un `KeyMetaDataCallback` e invocar `modifyKeyMetaData()`. A continuación, se invoca la implementación de llamada de retorno cuando los metadatos de DRM se encuentran en el contenido cifrado. Según los metadatos encontrados, puede elegir una licencia para incrustar y establecer la licencia mediante `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Consulte `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` en el directorio Reference Implementation Command Line Tools [!DNL Samples] (Herramientas de línea de comandos de implementación de referencia) para obtener un código de muestra que muestre las licencias incrustadas.

>[!NOTE]
>
>Un cliente de Adobe Primetime DRM 2.0 ignora todas las licencias incrustadas en el contenido y luego intenta obtener una licencia del servidor de licencias especificado en los metadatos. Sin embargo, si los metadatos indican que no hay ningún servidor de licencias disponible, es necesario actualizar un cliente Primetime DRM 2.0 para poder realizar la vista del contenido.

