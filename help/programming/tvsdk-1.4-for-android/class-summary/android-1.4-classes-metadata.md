---
description: Estas clases proporcionan metadatos para publicidad, Áreas de nombres y seguimiento.
seo-description: Estas clases proporcionan metadatos para publicidad, Áreas de nombres y seguimiento.
seo-title: Clases de metadatos
title: Clases de metadatos
uuid: 6d5099c8-d562-4635-9ef0-068cc6fb9f82
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# Clases de metadatos{#metadata-classes}

Estas clases proporcionan metadatos para publicidad, Áreas de nombres y seguimiento.

Paquete: [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/package-summary.html)

| Nombre | Descripción |
|---|---|
| [AdvertisingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html) | Clase que proporciona propiedades que deben configurarse para resolver publicidades para un elemento de medios determinado. Todas las propiedades requeridas deben configurarse para configurar el reproductor y resolver las publicidades correctamente. |
| AuditudeMetadata | Obsoleto. Utilice AuditudeSettings. |
| [AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | Clase que amplía Java `AdvertisingMetadata` específicamente para Phrase. Proporciona propiedades que se configurarán para resolver publicidades de frase para un elemento de medios determinado. Debe establecer todas las propiedades requeridas, incluido el ID de zona, el ID de medios y la URL del servidor de publicidad, para configurar el reproductor y resolver las publicidades correctamente. |
| [Metadatos](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/Metadata.html) | Define la interfaz genérica para configurar todos los metadatos disponibles para el reproductor y objetos adicionales. |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | Clase genérica tipo estructura de datos para almacenar pares de clave-valor arbitrarios. |
| [Metadatos temporizados](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | Clase para la representación sin procesar de los metadatos temporizados insertados en un flujo de medios. |