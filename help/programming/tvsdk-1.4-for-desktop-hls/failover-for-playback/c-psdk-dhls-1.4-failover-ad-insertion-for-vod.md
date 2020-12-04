---
description: El proceso de inserción de anuncios de vídeo a petición (VOD) consta de las fases de resolución, inserción y reproducción de anuncios. Para el seguimiento de anuncios, TVSDK debe informar a un servidor de seguimiento remoto sobre el progreso de reproducción de cada anuncio. Cuando surgen situaciones inesperadas, toma las medidas adecuadas.
seo-description: El proceso de inserción de anuncios de vídeo a petición (VOD) consta de las fases de resolución, inserción y reproducción de anuncios. Para el seguimiento de anuncios, TVSDK debe informar a un servidor de seguimiento remoto sobre el progreso de reproducción de cada anuncio. Cuando surgen situaciones inesperadas, toma las medidas adecuadas.
seo-title: Inserción de publicidad y conmutación por error para VOD
title: Inserción de publicidad y conmutación por error para VOD
uuid: 98505f63-ac43-4ff5-9f7b-895b6135df47
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---


# Inserción de publicidad y conmutación por error para VOD{#advertising-insertion-and-failover-for-vod}

El proceso de inserción de anuncios de vídeo a petición (VOD) consta de las fases de resolución, inserción y reproducción de anuncios. Para el seguimiento de anuncios, TVSDK debe informar a un servidor de seguimiento remoto sobre el progreso de reproducción de cada anuncio. Cuando surgen situaciones inesperadas, toma las medidas adecuadas.

## Fase de resolución de publicidad {#section_0D45C6094D724B55868B48F9A3557A8B}

TVSDK se pone en contacto con un servicio de envío de anuncios, como Adobe Primetime y toma decisiones de anuncios, e intenta obtener el archivo de lista de reproducción principal que corresponde al flujo de vídeo del anuncio. Durante la fase de resolución de anuncios, TVSDK realiza una llamada HTTP al servidor remoto de envío de anuncios y analiza la respuesta del servidor.

TVSDK admite los siguientes tipos de proveedores de publicidad:

* Proveedor de publicidad de metadatos

   Los datos de la publicidad se codifican en archivos JSON de texto sin formato.
* Proveedor de anuncios de primetime y decisiones

   TVSDK envía una solicitud, incluido un conjunto de parámetros de objetivo y un número de identificación de recursos, al servidor back-end de Primetime y de decisiones. Primetime y decisioning responde con un documento SMIL (lenguaje de integración multimedia sincronizada) que contiene la información de publicidad requerida.

Durante esta fase puede producirse una de las siguientes situaciones de failover:

* Los datos no se pueden recuperar por motivos como la falta de conectividad o un error en el servidor, como por ejemplo un recurso, no se puede encontrar, etc.
* Se recuperaron los datos, pero el formato no es válido.

   Esto puede ocurrir porque, por ejemplo, falló el análisis de los datos entrantes.

TVSDK emite una notificación de advertencia sobre el error y continúa el procesamiento.

## Fase de inserción de publicidad {#section_1B18E8B5768B4873B3346294175B7340}

TVSDK inserta el contenido alternativo (publicidades) en la línea de tiempo que corresponde al contenido principal.

Cuando se completa la fase de resolución de publicidad, TVSDK tiene una lista ordenada de los recursos publicitarios que se agrupan en saltos de publicidad. Cada pausa publicitaria se coloca en la línea de tiempo del contenido principal utilizando un valor de tiempo de inicio expresado en milisegundos (ms). Cada publicidad de una pausa publicitaria tiene una propiedad duration que también se expresa en ms. Las publicidades de una pausa publicitaria se encadenan una tras otra. Como resultado, la duración de una pausa publicitaria es igual a la suma de las duraciones de las publicidades compuestas individuales.

La conmutación por error puede ocurrir en esta fase con conflictos que pueden producirse en la línea de tiempo durante la inserción de anuncios. Para combinaciones específicas de valores de duración/tiempo del inicio de desglose de publicidad, los segmentos de publicidad podrían superponerse. La superposición se produce cuando la última parte de una pausa publicitaria se cruza con el principio del primer anuncio en la siguiente pausa publicitaria. En estas situaciones, descarta la pausa publicitaria posterior y continúa el proceso de inserción con el siguiente elemento de la lista hasta que se inserten o descarten todos los saltos de publicidad.

TVSDK emite una notificación de advertencia sobre el error y continúa el procesamiento.

## Fase de reproducción de publicidad {#section_64777BD2CDA84EACB0A4EA6D68367CF5}

TVSDK descarga los segmentos de publicidad y los procesa en la pantalla del dispositivo.

En este punto, TVSDK ha resuelto las publicidades, las ha colocado en la línea de tiempo e intenta procesar el contenido en la pantalla.

En esta fase pueden producirse las siguientes clases principales de errores:

* Errores al conectarse al servidor host
* Errores al descargar el archivo de manifiesto
* Errores al descargar los segmentos de medios

Para las tres clases de error, TVSDK reenvía eventos activados a la aplicación, incluidos:

* Eventos de notificación activados cuando se produce una conmutación por error.
* Eventos de notificación cuando se cambia el perfil debido al algoritmo de conmutación por error.
* Los eventos de notificación se activan cuando se consideran todas las opciones de conmutación por error y no se puede realizar ninguna acción adicional automáticamente.

   La aplicación debe realizar la acción adecuada.

Independientemente de si se producen errores o no, TVSDK llama a `AdBreakPlaybackEvent.AD_BREAK_COMPLETE` por cada `AdBreakPlaybackEvent.AD_BREAK_STARTED` y `AdPlaybackEvent.AD_COMPLETED` por cada `AdPLaybackEvent.AD_STARTED`. Sin embargo, si no se pudieron descargar los segmentos, es posible que haya espacios en la línea de tiempo. Cuando los huecos son lo suficientemente grandes, los valores en la posición del cursor de reproducción y el progreso del anuncio informado pueden mostrar discontinuidades.
