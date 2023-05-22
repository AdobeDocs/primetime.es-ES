---
description: El proceso de inserción de anuncios de vídeo bajo demanda (VOD) consiste en las fases de resolución de anuncios, inserción de anuncios y reproducción de anuncios. Para el seguimiento de anuncios, TVSDK debe informar a un servidor de seguimiento remoto sobre el progreso de reproducción de cada anuncio. Cuando se producen situaciones inesperadas, TVSDK realiza las acciones adecuadas.
title: Inserción de publicidad y failover para VOD
exl-id: 0f5929eb-b6cf-4454-904a-2d4637177b68
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# Inserción de publicidad y failover para VOD {#advertising-insertion-and-failover-for-vod}

El proceso de inserción de anuncios de vídeo bajo demanda (VOD) consiste en las fases de resolución de anuncios, inserción de anuncios y reproducción de anuncios. Para el seguimiento de anuncios, TVSDK debe informar a un servidor de seguimiento remoto sobre el progreso de reproducción de cada anuncio. Cuando se producen situaciones inesperadas, TVSDK realiza las acciones adecuadas.

## Fase de resolución de anuncios {#section_5DD3A7DA79E946298BFF829A60202E1C}

TVSDK se pone en contacto con un servicio de entrega de anuncios, como Adobe Primetime ad Decisioning, e intenta obtener el archivo de lista de reproducción principal que corresponde al flujo de vídeo del anuncio. Durante la fase de resolución de anuncios, TVSDK realiza una llamada HTTP al servidor de entrega de anuncios remoto y analiza la respuesta del servidor.

TVSDK admite los siguientes tipos de proveedores de publicidad:

* Proveedor de publicidad de metadatos

   Los datos del anuncio se codifican en archivos JSON de texto sin formato.
* Proveedor de publicidad de Primetime ad decisioning

   TVSDK envía una solicitud, que incluye un conjunto de parámetros de objetivo y un número de identificación de recurso, al servidor back-end de Primetime y Decisioning. Primetime ad decisioningresponde con un documento de lenguaje de integración multimedia (SMIL) sincronizado que contiene la información de publicidad necesaria.
* Proveedor de marcadores de publicidad personalizados

   Gestiona la situación en la que los anuncios se queman en el flujo, desde el servidor. TVSDK no realiza la inserción real de anuncios, pero debe realizar un seguimiento de los anuncios insertados en el servidor. Este proveedor establece los marcadores de anuncio que utiliza TVSDK para realizar el seguimiento de anuncios.

Durante esta fase se puede producir una de las siguientes situaciones de conmutación por error:

* No se pueden recuperar los datos porque, por ejemplo, no hay conectividad o se ha producido un error en el lado del servidor, como no se puede encontrar un recurso, etc.
* Se recuperaron los datos, pero el formato no es válido.

   Esto puede deberse, por ejemplo, a un error en el análisis de los datos de entrada.

TVSDK envía una notificación de advertencia sobre el error y continúa el procesamiento.

## Fase de inserción de publicidad {#section_29F7F7756C8B40B99AD4C3DD16B72B5B}

TVSDK inserta el contenido alternativo (anuncios) en la cronología que corresponde al contenido principal.

Cuando se completa la fase de resolución de anuncios, TVSDK tiene una lista ordenada de recursos publicitarios agrupados en pausas publicitarias. Cada pausa publicitaria se coloca en la cronología del contenido principal mediante un valor de tiempo de inicio expresado en milisegundos (ms). Cada anuncio de una pausa publicitaria tiene una propiedad duration que también se expresa en ms. Los anuncios de una pausa publicitaria están encadenados y, como resultado, la duración de una pausa publicitaria es igual a la suma de las duraciones de los anuncios individuales que los componen.

La conmutación por error puede producirse en esta fase con conflictos que pueden producirse en la cronología durante la inserción del anuncio. Para combinaciones específicas de valores de tiempo de inicio/duración de pausa publicitaria, los segmentos de publicidad pueden superponerse. Esta superposición se produce cuando la última parte de una pausa publicitaria se cruza con el principio del primer anuncio en la siguiente pausa publicitaria. En estas situaciones, TVSDK descarta la pausa publicitaria posterior y continúa el proceso de inserción de publicidad con el siguiente elemento de la lista hasta que se insertan o descartan todas las pausas publicitarias.

TVSDK envía una notificación de advertencia sobre el error y continúa el procesamiento.

## Fase de reproducción del anuncio {#section_DA816F88AF8A4A5A8FD0DE2D54A86031}

TVSDK descarga los segmentos de publicidad y los procesa en la pantalla del dispositivo.

Ahora, TVSDK ha resuelto anuncios, colocado los anuncios en la cronología e intenta representar el contenido en la pantalla.

Las siguientes clases principales de errores pueden producirse durante las siguientes fases:

* Al conectarse al servidor host.
* Al descargar el archivo de manifiesto.
* Al descargar los segmentos de medios.

TVSDK reenvía los eventos activados a la aplicación, incluidos los eventos de notificación que se activan cuando:

* Se produce un failover.
* El perfil se cambia debido al algoritmo de conmutación por error.
* Se han tenido en cuenta todas las opciones de conmutación por error y no se puede realizar ninguna acción adicional de forma automática.

   La aplicación debe realizar la acción adecuada.

Independientemente de si se producen errores, TVSDK llama a `onAdBreakComplete` para cada `onAdBreakStart` y `onAdComplete` para cada `onAdStart`. Sin embargo, si no se pueden descargar los segmentos, puede haber espacios en la cronología. Cuando los huecos son lo suficientemente grandes, los valores de la posición del cabezal de reproducción y el progreso del anuncio notificado pueden mostrar discontinuidades.
