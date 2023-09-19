---
description: El proceso de inserción de anuncios de vídeo bajo demanda (VOD) consiste en las fases de resolución de anuncios, inserción de anuncios y reproducción de anuncios. Para el seguimiento de anuncios, el TVSDK del explorador debe informar a un servidor de seguimiento remoto sobre el progreso de reproducción de cada anuncio. Cuando surgen situaciones inesperadas, se deben tomar las medidas adecuadas.
title: Inserción de publicidad y failover para VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---

# Inserción de publicidad y failover para VOD{#advertising-insertion-and-failover-for-vod}

El proceso de inserción de anuncios de vídeo bajo demanda (VOD) consiste en las fases de resolución de anuncios, inserción de anuncios y reproducción de anuncios. Para el seguimiento de anuncios, el TVSDK del explorador debe informar a un servidor de seguimiento remoto sobre el progreso de reproducción de cada anuncio. Cuando surgen situaciones inesperadas, se deben tomar las medidas adecuadas.

## Fase de resolución de anuncios {#section_F562CD6D0EF04AA9A0A3C0176A4EC340}

El TVSDK del explorador se pone en contacto con un servicio de entrega de anuncios, como Adobe Primetime ad Decisioning, e intenta obtener el archivo de lista de reproducción principal que corresponde al flujo de vídeo del anuncio. Durante la fase de resolución de anuncios, el TVSDK del explorador realiza una llamada HTTP al servidor de entrega de anuncios remoto y analiza la respuesta del servidor.

El TVSDK del explorador es compatible con los siguientes tipos de proveedores de publicidad:

* Proveedor de publicidad de metadatos

  Los datos del anuncio se codifican en archivos JSON de texto sin formato.
* Proveedor de publicidad de Adobe Primetime ad decisioning

  TVSDK del explorador envía una solicitud, que incluye un conjunto de parámetros de segmentación y un número de identificación de recurso, al servidor back-end de Adobe Primetime y Decisioning. Adobe Primetime ad decisioning responde con un documento SMIL (sincronizado multimedia integration language) que contiene la información de publicidad necesaria.

  Durante esta fase se puede producir una de las siguientes situaciones de conmutación por error:

   * Los datos no se pueden recuperar por motivos como falta de conectividad o un error del lado del servidor, como que no se puede encontrar un recurso, etc.
   * Se recuperaron los datos, pero el formato no es válido.

     Esto puede deberse, por ejemplo, a un error en el análisis de los datos de entrada.

  TVSDK del explorador emite una notificación de advertencia sobre el error y continúa procesando.

## Fase de inserción de publicidad {#section_88A0E4FA12394717A9D85689BD11D59F}

TVSDK del explorador inserta el contenido alternativo (anuncios) en la cronología que corresponde al contenido principal.

Cuando se completa la fase de resolución de anuncios, el TVSDK del explorador tiene una lista ordenada de recursos publicitarios agrupados en pausas publicitarias. Cada pausa publicitaria se coloca en la cronología del contenido principal mediante un valor de tiempo de inicio que se expresa en milisegundos (ms). Cada anuncio de una pausa publicitaria tiene una propiedad duration que también se expresa en ms. Los anuncios de una pausa publicitaria se encadenan uno tras otro. Como resultado, la duración de una pausa publicitaria es igual a la suma de las duraciones de los anuncios individuales que se componen.

La conmutación por error puede producirse en esta fase con conflictos que pueden producirse en la cronología durante la inserción del anuncio. Para combinaciones específicas de valores de tiempo de inicio/duración de pausa publicitaria, los segmentos de publicidad pueden superponerse. La superposición se produce cuando la última parte de una pausa publicitaria se cruza con el principio del primer anuncio en la siguiente pausa publicitaria. En estas situaciones, TVSDK del explorador descarta la pausa publicitaria posterior y continúa el proceso de inserción de publicidad con el siguiente elemento de la lista hasta que se insertan o descartan todas las pausas publicitarias.

TVSDK del explorador emite una notificación de advertencia sobre el error y continúa procesando.

## Fase de reproducción del anuncio {#section_7B0073BE9A744C74929263182C1243FC}

TVSDK del explorador descarga los segmentos de publicidad y los procesa en la pantalla del dispositivo.

En este punto, TVSDK del explorador ha resuelto anuncios, los ha colocado en la cronología e intenta procesar el contenido en la pantalla.

En esta fase pueden producirse las siguientes clases principales de errores:

* Errores al conectar con el servidor host
* Errores al descargar el archivo de manifiesto
* Errores al descargar los segmentos de medios

Para las tres clases de error, el TVSDK del explorador reenvía eventos activados a la aplicación, incluidos los siguientes:

* Eventos de notificación activados cuando se produce una conmutación por error.
* Eventos de notificación cuando se cambia el perfil debido al algoritmo de failover.
* Los eventos de notificación se activan cuando se han tenido en cuenta todas las opciones de conmutación por error y no se puede realizar ninguna acción adicional de forma automática.

  La aplicación debe realizar la acción adecuada.

Si se producen errores o no, Browser TVSDK le notifica cuando se inicia una pausa publicitaria y cuando se completa. Sin embargo, si no se pueden descargar los segmentos, puede haber espacios en la cronología. Cuando los huecos son lo suficientemente grandes, los valores de la posición del cabezal de reproducción y el progreso del anuncio notificado pueden mostrar discontinuidades.
