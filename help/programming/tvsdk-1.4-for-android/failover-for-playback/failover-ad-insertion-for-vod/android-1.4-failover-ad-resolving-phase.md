---
description: TVSDK se pone en contacto con un servicio de envío de anuncios, como Adobe Primetime y toma decisiones de anuncios, e intenta obtener el archivo de lista de reproducción principal que corresponde al flujo de vídeo del anuncio. Durante la fase de resolución de anuncios, TVSDK realiza una llamada HTTP al servidor remoto de envío de anuncios y analiza la respuesta del servidor.
seo-description: TVSDK se pone en contacto con un servicio de envío de anuncios, como Adobe Primetime y toma decisiones de anuncios, e intenta obtener el archivo de lista de reproducción principal que corresponde al flujo de vídeo del anuncio. Durante la fase de resolución de anuncios, TVSDK realiza una llamada HTTP al servidor remoto de envío de anuncios y analiza la respuesta del servidor.
seo-title: Fase de resolución de publicidad
title: Fase de resolución de publicidad
uuid: b3e62a57-7e62-4e4e-8fa6-0d416785db67
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---


# Fase de resolución de publicidad{#ad-resolving-phase}

TVSDK se pone en contacto con un servicio de envío de anuncios, como Adobe Primetime y toma decisiones de anuncios, e intenta obtener el archivo de lista de reproducción principal que corresponde al flujo de vídeo del anuncio. Durante la fase de resolución de anuncios, TVSDK realiza una llamada HTTP al servidor remoto de envío de anuncios y analiza la respuesta del servidor.

TVSDK admite los siguientes tipos de proveedores de publicidad:

* Proveedor de publicidad de metadatos

   Los datos de la publicidad se codifican en archivos JSON de texto sin formato.
* Proveedor de anuncios de primetime y decisiones

   TVSDK envía una solicitud, incluido un conjunto de parámetros de objetivo y un número de identificación de recursos, al servidor back-end de Primetime y de decisiones. Primetime y decisioning responde con un documento SMIL (lenguaje de integración multimedia sincronizada) que contiene la información de publicidad requerida.
* Proveedor de marcadores de publicidad personalizados

   Gestiona la situación en la que los anuncios se queman en el flujo, desde el servidor. TVSDK no realiza la inserción de publicidad real, pero debe realizar un seguimiento de las publicidades insertadas en el servidor. Este proveedor establece los marcadores de publicidad que utiliza TVSDK para realizar el seguimiento de publicidad.

Durante esta fase puede producirse una de las siguientes situaciones de failover:

* Los datos no se pueden recuperar por motivos como la falta de conectividad o un error en el servidor, como por ejemplo un recurso, no se puede encontrar, etc.
* Se recuperaron los datos, pero el formato no es válido.

   Esto puede ocurrir porque, por ejemplo, falló el análisis de los datos entrantes.

TVSDK emite una notificación de advertencia sobre el error y continúa el procesamiento.
