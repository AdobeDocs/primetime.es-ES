---
description: TVSDK se pone en contacto con un servicio de entrega de publicidad, como Adobe Primetime ad decisioning, e intenta obtener el archivo de la lista de reproducción principal que corresponde al flujo de vídeo del anuncio. Durante la fase de resolución de anuncios, TVSDK realiza una llamada HTTP al servidor de entrega de anuncios remoto y analiza la respuesta del servidor.
title: Fase de resolución de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# Fase de resolución de publicidad{#ad-resolving-phase}

TVSDK se pone en contacto con un servicio de entrega de publicidad, como Adobe Primetime ad decisioning, e intenta obtener el archivo de la lista de reproducción principal que corresponde al flujo de vídeo del anuncio. Durante la fase de resolución de anuncios, TVSDK realiza una llamada HTTP al servidor de entrega de anuncios remoto y analiza la respuesta del servidor.

TVSDK admite los siguientes tipos de proveedores de publicidad:

* Proveedor de publicidad de metadatos

   Los datos de la publicidad se codifican en archivos JSON de texto sin formato.
* Proveedor de anuncios de primetime ad decisioning

   TVSDK envía una solicitud, que incluye un conjunto de parámetros de objetivo y un número de identificación de recursos, al servidor back-end de Primetime y decisioning. Primetime ad decisioning responde con un documento SMIL (lenguaje de integración multimedia sincronizada) que contiene la información de publicidad necesaria.
* Proveedor de marcadores de anuncio personalizado

   Gestiona la situación en la que se queman anuncios en el flujo, desde el lado del servidor. TVSDK no realiza la inserción de publicidad real, pero debe realizar un seguimiento de las publicidades insertadas en el servidor. Este proveedor establece los marcadores de anuncio que utiliza TVSDK para realizar el seguimiento de anuncios.

Durante esta fase puede producirse una de las siguientes situaciones de failover:

* Los datos no se pueden recuperar por motivos que incluyen falta de conectividad o un error del lado del servidor, como que un recurso no se puede encontrar, etc.
* Se recuperaron los datos, pero el formato no es válido.

   Esto puede deberse, por ejemplo, a un error en el análisis de los datos de entrada.

TVSDK envía una notificación de advertencia sobre el error y continúa con el procesamiento.
