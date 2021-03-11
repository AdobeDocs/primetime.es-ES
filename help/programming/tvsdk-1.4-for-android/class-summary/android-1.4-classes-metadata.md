---
description: Estas clases proporcionan metadatos para publicidad, áreas de nombres y seguimiento.
title: Clases de metadatos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# Clases de metadatos{#metadata-classes}

Estas clases proporcionan metadatos para publicidad, áreas de nombres y seguimiento.

Paquete: [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/package-summary.html)

| Nombre | Descripción |
|---|---|
| [AdvertisingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html) | Clase que proporciona propiedades que deben configurarse para resolver anuncios de un elemento multimedia determinado. Se deben configurar todas las propiedades necesarias para configurar el reproductor y resolver las publicidades correctamente. |
| AuditudeMetadata | Obsoleto. Utilice AuditudeSettings. |
| [AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | Clase que amplía Java `AdvertisingMetadata` específicamente para Frase. Proporciona propiedades que se deben configurar para resolver la publicidad de Frase de un elemento multimedia determinado. Debe establecer todas las propiedades requeridas, incluido el ID de zona, el ID de medios y la URL del servidor de publicidad, para configurar el reproductor para que resuelva los anuncios correctamente. |
| [Metadatos](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/Metadata.html) | Define la interfaz genérica para configurar todos los metadatos disponibles para el reproductor y los objetos adicionales. |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | Clase genérica similar a la estructura de datos para almacenar pares de clave-valor arbitrarios. |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | Clase para la representación sin procesar de los metadatos temporizados insertados en un flujo de medios. |