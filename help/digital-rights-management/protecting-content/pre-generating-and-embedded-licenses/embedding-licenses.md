---
seo-title: Incrustación de licencias
title: Incrustación de licencias
uuid: e3d55376-07de-479c-9a53-04bc8071ced4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Incrustación de licencias {#embedding-licenses}

Una vez que el contenido se ha cifrado y se ha generado previamente una licencia, ésta puede incrustarse en el contenido cifrado.

Si desea incrustar una licencia, debe obtener una instancia de `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Si conoce el tipo de contenido cifrado, utilice el constructor para `FLVKeyMetaDataUpdater` o `F4VKeyMetaDataUpdater`; en caso contrario, utilice `MediaProcessorFactory.getMediaProcessor()` para devolver una instancia basada en el tipo de archivo detectado. Luego debe construir un `KeyMetaDataCallback` e invocar `modifyKeyMetaData()`. A continuación, se invoca la implementación de llamada de retorno cuando los metadatos de DRM se encuentran en el contenido cifrado. En función de los metadatos encontrados, puede elegir una licencia para incrustar y establecer la licencia mediante `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Consulte `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` en el directorio Reference Implementation Command Line Tools (Herramientas de la línea de comandos de implementación de referencia) [!DNL Samples] para obtener un código de muestra que muestre las licencias incrustadas.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Un cliente de Adobe Primetime DRM 2.0 ignora todas las licencias incrustadas en el contenido y luego intenta obtener una licencia del servidor de licencias especificado en los metadatos. Sin embargo, si los metadatos indican que no hay ningún servidor de licencias disponible, es necesario actualizar un cliente Primetime DRM 2.0 para poder ver el contenido.

