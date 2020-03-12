---
description: El proceso de inserción de anuncios de vídeo a petición (VOD) consta de las fases de resolución, inserción y reproducción de anuncios. Para el seguimiento de anuncios, TVSDK debe informar a un servidor de seguimiento remoto sobre el progreso de reproducción de cada anuncio. Cuando surgen situaciones inesperadas, TVSDK realiza la acción adecuada.
seo-description: El proceso de inserción de anuncios de vídeo a petición (VOD) consta de las fases de resolución, inserción y reproducción de anuncios. Para el seguimiento de anuncios, TVSDK debe informar a un servidor de seguimiento remoto sobre el progreso de reproducción de cada anuncio. Cuando surgen situaciones inesperadas, TVSDK realiza la acción adecuada.
seo-title: Inserción de publicidad y conmutación por error para VOD
title: Inserción de publicidad y conmutación por error para VOD
uuid: 74cc35e6-6479-4572-a3b3-05ff6344272a
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Inserción de publicidad y conmutación por error para VOD {#advertising-insertion-and-failover-for-vod}

El proceso de inserción de anuncios de vídeo a petición (VOD) consta de las fases de resolución, inserción y reproducción de anuncios. Para el seguimiento de anuncios, TVSDK debe informar a un servidor de seguimiento remoto sobre el progreso de reproducción de cada anuncio. Cuando surgen situaciones inesperadas, TVSDK realiza la acción adecuada.

## Fase de resolución de publicidad {#section_5DD3A7DA79E946298BFF829A60202E1C}

TVSDK se pone en contacto con un servicio de entrega de publicidad, como Adobe Primetime y decisiones, e intenta obtener el archivo de lista de reproducción principal que corresponde al flujo de vídeo del anuncio. Durante la fase de resolución de anuncios, TVSDK realiza una llamada HTTP al servidor remoto de entrega de anuncios y analiza la respuesta del servidor.

TVSDK admite los siguientes tipos de proveedores de publicidad:

* Proveedor de publicidad de metadatos

   Los datos de la publicidad se codifican en archivos JSON de texto sin formato.
* Proveedor de anuncios de primetime y decisiones

   TVSDK envía una solicitud, incluido un conjunto de parámetros de objetivo y un número de identificación de recursos, al servidor de back-end Primetime y decisioningback-end. Primetime y decisioningresponde con un documento SMIL (Lenguaje de integración multimedia sincronizada) que contiene la información de publicidad requerida.
* Proveedor de marcadores de publicidad personalizados

   Gestiona la situación en la que los anuncios se queman en el flujo, desde el servidor. TVSDK no realiza la inserción de publicidad real, pero debe realizar un seguimiento de las publicidades insertadas en el servidor. Este proveedor establece los marcadores de publicidad que utiliza TVSDK para realizar el seguimiento de publicidad.

Durante esta fase puede producirse una de las siguientes situaciones de failover:

* No se pueden recuperar los datos debido, por ejemplo, a la falta de conectividad o a un error en el servidor, como no se puede encontrar un recurso, etc.
* Se recuperaron los datos, pero el formato no es válido.

   Esto puede ocurrir porque, por ejemplo, falló el análisis de los datos entrantes.

TVSDK emite una notificación de advertencia sobre el error y continúa el procesamiento.

## Fase de inserción de publicidad {#section_29F7F7756C8B40B99AD4C3DD16B72B5B}

TVSDK inserta el contenido alternativo (publicidades) en la línea de tiempo que corresponde al contenido principal.

Cuando se completa la fase de resolución de publicidad, TVSDK tiene una lista ordenada de recursos publicitarios que se agrupan en saltos de publicidad. Cada pausa publicitaria se coloca en la línea de tiempo del contenido principal mediante un valor de tiempo de inicio expresado en milisegundos (ms). Cada publicidad de una pausa publicitaria tiene una propiedad duration que también se expresa en ms. Las publicidades de una pausa publicitaria están encadenadas y, como resultado, la duración de una pausa publicitaria es igual a la suma de las duraciones de las publicidades compuestas individuales.

La conmutación por error puede ocurrir en esta fase con conflictos que pueden producirse en la línea de tiempo durante la inserción de anuncios. Para combinaciones específicas de valores de tiempo de inicio/duración de desglose de publicidad, los segmentos de publicidad podrían superponerse. Esta superposición se produce cuando la última parte de una pausa publicitaria se cruza con el principio del primer anuncio en la siguiente pausa publicitaria. En estas situaciones, TVSDK descarta la pausa publicitaria posterior y continúa el proceso de inserción con el siguiente elemento de la lista hasta que se insertan o descarten todos los saltos de publicidad.

TVSDK emite una notificación de advertencia sobre el error y continúa el procesamiento.

## Fase de reproducción de publicidad {#section_DA816F88AF8A4A5A8FD0DE2D54A86031}

TVSDK descarga los segmentos de publicidad y los procesa en la pantalla del dispositivo.

Ahora, TVSDK ha resuelto las publicidades, las ha colocado en la línea de tiempo e intenta procesar el contenido en la pantalla.

Las siguientes clases principales de errores pueden producirse durante las siguientes fases:

* Al conectarse al servidor host.
* Al descargar el archivo de manifiesto.
* Al descargar los segmentos de medios.

TVSDK envía los eventos activados a la aplicación, incluidos los eventos de notificación que se activan cuando:

* Se produce una conmutación por error.
* El perfil se cambia debido al algoritmo de conmutación por error.
* Se han considerado todas las opciones de conmutación por error y no se puede realizar ninguna acción adicional automáticamente.

   La aplicación debe realizar la acción adecuada.

Independientemente de si se producen errores, TVSDK llama `onAdBreakComplete` para cada `onAdBreakStart` y `onAdComplete` para cada `onAdStart`. Sin embargo, si no se pudieron descargar los segmentos, es posible que haya espacios en la línea de tiempo. Cuando los huecos son lo suficientemente grandes, los valores en la posición del cursor de reproducción y el progreso del anuncio informado pueden mostrar discontinuidades.