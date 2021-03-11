---
description: El proceso de inserción de anuncios de vídeo bajo demanda (VOD) consta de las fases de resolución, inserción y reproducción de anuncios. Para el seguimiento de anuncios, TVSDK debe informar a un servidor de seguimiento remoto sobre el progreso de reproducción de cada anuncio. Cuando se presentan situaciones inesperadas, TVSDK adopta las medidas adecuadas.
title: inserción y conmutación por error de publicidad para VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---


# Inserción y conmutación por error de publicidad para VOD {#advertising-insertion-and-failover-for-vod}

El proceso de inserción de anuncios de vídeo bajo demanda (VOD) consta de las fases de resolución, inserción y reproducción de anuncios. Para el seguimiento de anuncios, TVSDK debe informar a un servidor de seguimiento remoto sobre el progreso de reproducción de cada anuncio. Cuando se presentan situaciones inesperadas, TVSDK adopta las medidas adecuadas.

## Fase de resolución de publicidad {#section_5DD3A7DA79E946298BFF829A60202E1C}

TVSDK se pone en contacto con un servicio de entrega de publicidad, como Adobe Primetime ad decisioning, e intenta obtener el archivo de la lista de reproducción principal que corresponde al flujo de vídeo del anuncio. Durante la fase de resolución de anuncios, TVSDK realiza una llamada HTTP al servidor de entrega de anuncios remoto y analiza la respuesta del servidor.

TVSDK admite los siguientes tipos de proveedores de publicidad:

* Proveedor de publicidad de metadatos

   Los datos de la publicidad se codifican en archivos JSON de texto sin formato.
* Proveedor de anuncios de primetime ad decisioning

   TVSDK envía una solicitud, que incluye un conjunto de parámetros de objetivo y un número de identificación de recursos, al servidor back-end de Primetime ad decisioning. Primetime ad decisioningresponde con un documento de lenguaje de integración multimedia sincronizada (SMIL) que contiene la información de publicidad necesaria.
* Proveedor de marcadores de anuncio personalizado

   Gestiona la situación en la que se queman anuncios en el flujo, desde el lado del servidor. TVSDK no realiza la inserción de publicidad real, pero debe realizar un seguimiento de las publicidades insertadas en el servidor. Este proveedor establece los marcadores de anuncio que utiliza TVSDK para realizar el seguimiento de anuncios.

Durante esta fase puede producirse una de las siguientes situaciones de failover:

* No se pueden recuperar los datos debido, por ejemplo, a la falta de conectividad o a un error del lado del servidor, como que no se encuentra un recurso, etc.
* Se recuperaron los datos, pero el formato no es válido.

   Esto puede deberse, por ejemplo, a un error en el análisis de los datos de entrada.

TVSDK envía una notificación de advertencia sobre el error y continúa con el procesamiento.

## Fase de inserción de publicidad {#section_29F7F7756C8B40B99AD4C3DD16B72B5B}

TVSDK inserta el contenido alternativo (anuncios) en la cronología que corresponde al contenido principal.

Cuando finaliza la fase de resolución de anuncios, TVSDK tiene una lista ordenada de recursos publicitarios que se agrupan en pausas publicitarias. Cada pausa publicitaria se coloca en la cronología de contenido principal utilizando un valor de tiempo de inicio expresado en milisegundos (ms). Cada anuncio de una pausa publicitaria tiene una propiedad duration que también se expresa en ms. Los anuncios de una pausa publicitaria están encadenados y, como resultado, la duración de una pausa publicitaria es igual a la suma de las duraciones de los anuncios compuestos individuales.

La conmutación por error puede ocurrir en esta fase con conflictos que podrían producirse en la cronología durante la inserción del anuncio. Para combinaciones específicas de valores de tiempo de inicio/duración de las pausas publicitarias, los segmentos publicitarios podrían superponerse. Esta superposición se produce cuando la última parte de una pausa publicitaria se cruza con el principio del primer anuncio de la siguiente pausa publicitaria. En estas situaciones, TVSDK descarta la pausa publicitaria posterior y continúa el proceso de inserción con el siguiente elemento de la lista hasta que se insertan o descartan todas las pausas publicitarias.

TVSDK envía una notificación de advertencia sobre el error y continúa con el procesamiento.

## Fase de reproducción de anuncio {#section_DA816F88AF8A4A5A8FD0DE2D54A86031}

TVSDK descarga los segmentos de anuncio y los procesa en la pantalla del dispositivo.

Ahora, TVSDK ha resuelto anuncios, colocado los anuncios en la cronología e intenta representar el contenido en la pantalla.

Las siguientes clases principales de errores pueden ocurrir durante las siguientes fases:

* Al conectarse al servidor host.
* Al descargar el archivo de manifiesto.
* Al descargar los segmentos de medios.

TVSDK reenvía los eventos activados a su aplicación, incluidos los eventos de notificación que se activan cuando:

* Se produce una conmutación por error.
* El perfil se cambia debido al algoritmo de conmutación por error.
* Se han considerado todas las opciones de failover, y no se puede realizar ninguna acción adicional automáticamente.

   La aplicación debe realizar la acción adecuada.

Independientemente de si se producen errores, TVSDK llama `onAdBreakComplete` para cada `onAdBreakStart` y `onAdComplete` para cada `onAdStart`. Sin embargo, si no se pueden descargar los segmentos, es posible que haya espacios en la cronología. Cuando los espacios son lo suficientemente grandes, los valores en la posición del cabezal de reproducción y el progreso del anuncio registrado pueden mostrar interrupciones.
