---
description: TVSDK se pone en contacto con un servicio de entrega de anuncios, como Adobe Primetime ad Decisioning, e intenta obtener el archivo de lista de reproducción principal que corresponde al flujo de vídeo del anuncio. Durante la fase de resolución de anuncios, TVSDK realiza una llamada HTTP al servidor de entrega de anuncios remoto y analiza la respuesta del servidor.
title: Fase de resolución de anuncios
exl-id: 5dd96709-1a65-442f-a753-a4343c6e8762
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# Fase de resolución de anuncios{#ad-resolving-phase}

TVSDK se pone en contacto con un servicio de entrega de anuncios, como Adobe Primetime ad Decisioning, e intenta obtener el archivo de lista de reproducción principal que corresponde al flujo de vídeo del anuncio. Durante la fase de resolución de anuncios, TVSDK realiza una llamada HTTP al servidor de entrega de anuncios remoto y analiza la respuesta del servidor.

TVSDK admite los siguientes tipos de proveedores de publicidad:

* Proveedor de publicidad de metadatos

   Los datos del anuncio se codifican en archivos JSON de texto sin formato.
* Proveedor de publicidad de Primetime ad decisioning

   TVSDK envía una solicitud, que incluye un conjunto de parámetros de objetivo y un número de identificación de recurso, al servidor back-end de Primetime y Decisioning. Primetime ad decisioning responde con un documento SMIL (lenguaje de integración multimedia sincronizado) que contiene la información de publicidad necesaria.
* Proveedor de marcadores de publicidad personalizados

   Gestiona la situación en la que los anuncios se queman en el flujo, desde el servidor. TVSDK no realiza la inserción real de anuncios, pero debe realizar un seguimiento de los anuncios insertados en el servidor. Este proveedor establece los marcadores de anuncio que utiliza TVSDK para realizar el seguimiento de anuncios.

Durante esta fase se puede producir una de las siguientes situaciones de conmutación por error:

* Los datos no se pueden recuperar por motivos como falta de conectividad o un error del lado del servidor, como que no se puede encontrar un recurso, etc.
* Se recuperaron los datos, pero el formato no es válido.

   Esto puede deberse, por ejemplo, a un error en el análisis de los datos de entrada.

TVSDK envía una notificación de advertencia sobre el error y continúa el procesamiento.
