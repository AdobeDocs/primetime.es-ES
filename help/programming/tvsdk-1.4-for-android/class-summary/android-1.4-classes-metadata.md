---
description: Estas clases proporcionan metadatos para publicidad, áreas de nombres y seguimiento.
title: Clases de metadatos
exl-id: 3d98c5e1-6792-419b-9638-f156f1eafd1b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Clases de metadatos{#metadata-classes}

Estas clases proporcionan metadatos para publicidad, áreas de nombres y seguimiento.

Paquete: [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/package-summary.html)

| Nombre | Descripción |
|---|---|
| [AdvertisingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html) | Clase que proporciona propiedades que deben configurarse para resolver anuncios de un elemento de medios determinado. Se deben configurar todas las propiedades necesarias para configurar el reproductor y resolver correctamente los anuncios. |
| AuditudeMetadata | Obsoleto. Utilice AuditudeSettings. |
| [AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | Clase que amplía Java `AdvertisingMetadata` específicamente para Frase. Proporciona propiedades que se deben configurar para resolver anuncios de frases para un elemento de medios determinado. Debe establecer todas las propiedades necesarias, incluido el ID de zona, el ID de medios y la URL del servidor de publicidad, para configurar el reproductor y resolver correctamente los anuncios. |
| [Metadatos](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/Metadata.html) | Define la interfaz genérica para configurar todos los metadatos disponibles para el reproductor y los objetos adicionales. |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | Clase genérica similar a una estructura de datos para almacenar pares de clave-valor arbitrarios. |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | Clase para la representación sin procesar de los metadatos cronometrados insertados en un flujo de medios. |
