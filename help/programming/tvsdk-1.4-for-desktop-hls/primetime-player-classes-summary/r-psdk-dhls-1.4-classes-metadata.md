---
description: Estas clases proporcionan metadatos para publicidad, áreas de nombres y seguimiento.
title: Clases de metadatos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# Clases de metadatos {#metadata-classes}

Estas clases proporcionan metadatos para publicidad, áreas de nombres y seguimiento.

Paquete: [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/package-detail.html)

| Nombre | Descripción |
|---|---|
| [AdSignalingMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/AdSignalingMode.html) | Clase de enumeración que expone los modos de señalización admitidos en la frase. |
| [AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | Clase que amplía `Metadata` específicamente para Frase. Proporciona propiedades que se deben configurar para resolver la publicidad de Frase de un elemento multimedia determinado. Debe establecer todas las propiedades requeridas, incluido el ID de zona, el ID de medios y la URL del servidor de publicidad, para configurar el reproductor para que resuelva los anuncios correctamente. |
| [ByteArrayMetadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/ByteArrayMetadata.html) | Obsoleto. Utilice `Metadata`. |
| [DefaultMetadataKeys](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/DefaultMetadataKeys.html) | Clase. |
| [Metadatos](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/Metadata.html) | Define la interfaz genérica para configurar todos los metadatos disponibles para el reproductor y los objetos adicionales. |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | Obsoleto. Utilice `Metadata`. |
| [MetadataUtils](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/MetadataUtils.html) | Clase de métodos para trabajar con metadatos. |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | Clase para la representación sin procesar de los metadatos temporizados insertados en un flujo de medios. |
| [TimedMetadataType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/TimedMetadataType.html) | Clase que contiene los tipos admitidos para los metadatos temporizados (en la lista de reproducción o flujo), como los metadatos o etiquetas ID3. |