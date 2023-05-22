---
title: Incrustación de licencias
description: Incrustación de licencias
copied-description: true
exl-id: 8cd58808-73fb-4635-9a75-0520430f6b3a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Incrustación de licencias {#embedding-licenses}

Una vez que el contenido se ha cifrado y se ha generado previamente una licencia, esta puede incrustarse en el contenido cifrado.

Si desea incrustar una licencia, debe obtener una instancia de `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Si conoce el tipo de contenido cifrado, utilice el constructor para `FLVKeyMetaDataUpdater` o `F4VKeyMetaDataUpdater`; de lo contrario, utilice `MediaProcessorFactory.getMediaProcessor()` para devolver una instancia basada en el tipo de archivo detectado. Entonces necesita construir un `KeyMetaDataCallback` e invocar `modifyKeyMetaData()`. La implementación de devolución de llamada se invocará cuando los metadatos DRM se encuentren en el contenido cifrado. En función de los metadatos encontrados, puede elegir una licencia para incrustar y establecer la licencia mediante `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Consulte `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` en las herramientas de línea de comandos de implementación de referencia [!DNL Samples] directorio para código de ejemplo que muestra licencias incrustadas.

>[!NOTE]
>
>Un cliente de Adobe Primetime DRM 2.0 ignora las licencias incrustadas en el contenido y luego intenta obtener una licencia del servidor de licencias especificado en los metadatos. Sin embargo, si los metadatos indican que no hay ningún servidor de licencias disponible, es necesario actualizar un cliente de Primetime DRM 2.0 para poder ver el contenido.
