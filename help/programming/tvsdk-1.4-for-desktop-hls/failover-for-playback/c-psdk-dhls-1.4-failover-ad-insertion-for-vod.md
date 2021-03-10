---
description: El proceso de inserción de anuncios de vídeo bajo demanda (VOD) consta de las fases de resolución, inserción y reproducción de anuncios. Para el seguimiento de anuncios, TVSDK debe informar a un servidor de seguimiento remoto sobre el progreso de reproducción de cada anuncio. Cuando surgen situaciones inesperadas, se deben tomar las medidas adecuadas.
title: inserción y conmutación por error de publicidad para VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---


# Inserción y conmutación por error de publicidad para VOD{#advertising-insertion-and-failover-for-vod}

El proceso de inserción de anuncios de vídeo bajo demanda (VOD) consta de las fases de resolución, inserción y reproducción de anuncios. Para el seguimiento de anuncios, TVSDK debe informar a un servidor de seguimiento remoto sobre el progreso de reproducción de cada anuncio. Cuando surgen situaciones inesperadas, se deben tomar las medidas adecuadas.

## Fase de resolución de publicidad {#section_0D45C6094D724B55868B48F9A3557A8B}

TVSDK se pone en contacto con un servicio de entrega de publicidad, como Adobe Primetime ad decisioning, e intenta obtener el archivo de la lista de reproducción principal que corresponde al flujo de vídeo del anuncio. Durante la fase de resolución de anuncios, TVSDK realiza una llamada HTTP al servidor de entrega de anuncios remoto y analiza la respuesta del servidor.

TVSDK admite los siguientes tipos de proveedores de publicidad:

* Proveedor de publicidad de metadatos

   Los datos de la publicidad se codifican en archivos JSON de texto sin formato.
* Proveedor de anuncios de primetime ad decisioning

   TVSDK envía una solicitud, que incluye un conjunto de parámetros de objetivo y un número de identificación de recursos, al servidor back-end de Primetime y decisioning. Primetime ad decisioning responde con un documento SMIL (lenguaje de integración multimedia sincronizada) que contiene la información de publicidad necesaria.

Durante esta fase puede producirse una de las siguientes situaciones de failover:

* Los datos no se pueden recuperar por motivos que incluyen falta de conectividad o un error del lado del servidor, como que un recurso no se puede encontrar, etc.
* Se recuperaron los datos, pero el formato no es válido.

   Esto puede deberse, por ejemplo, a un error en el análisis de los datos de entrada.

TVSDK envía una notificación de advertencia sobre el error y continúa con el procesamiento.

## Fase de inserción de publicidad {#section_1B18E8B5768B4873B3346294175B7340}

TVSDK inserta el contenido alternativo (anuncios) en la cronología que corresponde al contenido principal.

Cuando finaliza la fase de resolución de anuncios, TVSDK tiene una lista ordenada de recursos publicitarios que se agrupan en pausas publicitarias. Cada pausa publicitaria se coloca en la cronología del contenido principal utilizando un valor de tiempo de inicio expresado en milisegundos (ms). Cada anuncio de una pausa publicitaria tiene una propiedad duration que también se expresa en ms. Los anuncios de una pausa publicitaria se encadenan uno tras otro. Como resultado, la duración de una pausa publicitaria es igual a la suma de las duraciones de los anuncios compuestos individuales.

La conmutación por error puede ocurrir en esta fase con conflictos que podrían producirse en la cronología durante la inserción del anuncio. Para combinaciones específicas de valores de tiempo de inicio/duración de las pausas publicitarias, los segmentos publicitarios podrían superponerse. La superposición se produce cuando la última parte de una pausa publicitaria se cruza con el principio del primer anuncio de la siguiente pausa publicitaria. En estas situaciones, descarta la pausa publicitaria posterior y continúa el proceso de inserción con el siguiente elemento de la lista hasta que se inserten o descarten todas las pausas publicitarias.

TVSDK envía una notificación de advertencia sobre el error y continúa con el procesamiento.

## Fase de reproducción de anuncio {#section_64777BD2CDA84EACB0A4EA6D68367CF5}

TVSDK descarga los segmentos de anuncio y los procesa en la pantalla del dispositivo.

En este punto, TVSDK ha resuelto anuncios, los ha colocado en la cronología e intenta renderizar el contenido en la pantalla.

En esta fase pueden producirse las siguientes clases principales de errores:

* Errores al conectarse al servidor host
* Errores al descargar el archivo de manifiesto
* Errores al descargar los segmentos de medios

Para las tres clases de error, TVSDK reenvía a su aplicación eventos activados, incluidos:

* Eventos de notificación activados cuando se produce una conmutación por error.
* Eventos de notificación cuando se cambia el perfil debido al algoritmo de conmutación por error.
* Los eventos de notificación se activan cuando se tienen en cuenta todas las opciones de conmutación por error y no se puede realizar ninguna acción adicional automáticamente.

   La aplicación debe realizar la acción adecuada.

Se produzcan o no errores, TVSDK llama `AdBreakPlaybackEvent.AD_BREAK_COMPLETE` para cada `AdBreakPlaybackEvent.AD_BREAK_STARTED` y `AdPlaybackEvent.AD_COMPLETED` para cada `AdPLaybackEvent.AD_STARTED`. Sin embargo, si no se pueden descargar los segmentos, es posible que haya espacios en la cronología. Cuando los espacios son lo suficientemente grandes, los valores en la posición del cabezal de reproducción y el progreso del anuncio registrado pueden mostrar interrupciones.
