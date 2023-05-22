---
description: Estas clases proporcionan metadatos para publicidad, áreas de nombres y seguimiento.
title: Clases de metadatos
exl-id: 15b7548f-bd9c-42cb-b9f3-477fc4415f8d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Clases de metadatos{#metadata-classes}

Estas clases proporcionan metadatos para publicidad, áreas de nombres y seguimiento.

| Nombre | Descripción |
|---|---|
| [PTAdMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdMetadata.html) | Clase que proporciona propiedades que deben configurarse para resolver anuncios de un elemento de medios determinado. Se deben configurar todas las propiedades necesarias para configurar el reproductor y resolver correctamente los anuncios. |
| [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) | Clase que extiende `PTAdMetadata` específicamente para Adobe Primetime ad decisioning. Proporciona propiedades que se deben configurar para resolver anuncios de Adobe Primetime y Decisioning para un elemento de medios determinado. Debe establecer todas las propiedades necesarias, incluido el ID de zona, el ID de medios y la URL del servidor de publicidad, para configurar el reproductor y resolver correctamente los anuncios. |
| [PTMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMetadata.html) | Define la clase base para configurar todos los metadatos disponibles para el reproductor y los objetos adicionales. |
| [PTTimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTimedMetadata.html) | Clase que representa una etiqueta HLS personalizada en el flujo. |
| [PTTtrackingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTrackingMetadata.html) | Define una clase base para todos los metadatos relacionados con el seguimiento y el análisis. |
