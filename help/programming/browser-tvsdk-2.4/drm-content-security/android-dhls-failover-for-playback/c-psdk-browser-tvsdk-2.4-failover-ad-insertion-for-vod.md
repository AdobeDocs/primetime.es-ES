---
description: El proceso de inserción de anuncios de vídeo a petición (VOD) consta de las fases de resolución, inserción y reproducción de anuncios. Para el seguimiento de anuncios, el SDK del explorador debe informar a un servidor de seguimiento remoto sobre el progreso de reproducción de cada publicidad. Cuando surgen situaciones inesperadas, toma las medidas adecuadas.
seo-description: El proceso de inserción de anuncios de vídeo a petición (VOD) consta de las fases de resolución, inserción y reproducción de anuncios. Para el seguimiento de anuncios, el SDK del explorador debe informar a un servidor de seguimiento remoto sobre el progreso de reproducción de cada publicidad. Cuando surgen situaciones inesperadas, toma las medidas adecuadas.
seo-title: Inserción de publicidad y conmutación por error para VOD
title: Inserción de publicidad y conmutación por error para VOD
uuid: 33f7aad5-fc4f-459d-8c29-01ba1353dfcc
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 0%

---


# Inserción de publicidad y conmutación por error para VOD{#advertising-insertion-and-failover-for-vod}

El proceso de inserción de anuncios de vídeo a petición (VOD) consta de las fases de resolución, inserción y reproducción de anuncios. Para el seguimiento de anuncios, el SDK del explorador debe informar a un servidor de seguimiento remoto sobre el progreso de reproducción de cada publicidad. Cuando surgen situaciones inesperadas, toma las medidas adecuadas.

## Fase de resolución de publicidad {#section_F562CD6D0EF04AA9A0A3C0176A4EC340}

El SDK de explorador se pone en contacto con un servicio de envío de publicidad, como Adobe Primetime y toma decisiones de publicidad, e intenta obtener el archivo de lista de reproducción principal que corresponde al flujo de vídeo del anuncio. Durante la fase de resolución de anuncios, el TVSDK del explorador realiza una llamada HTTP al servidor remoto de envío de anuncios y analiza la respuesta del servidor.

El TVSDK del explorador admite los siguientes tipos de proveedores de publicidad:

* Proveedor de publicidad de metadatos

   Los datos de la publicidad se codifican en archivos JSON de texto sin formato.
* Proveedor de anuncios de decisiones de publicidad de Adobe Primetime

   El SDK de explorador envía una solicitud, que incluye un conjunto de parámetros de objetivo y un número de identificación de recursos, al servidor back-end de Adobe Primetime para la toma de decisiones de publicidad. La toma de decisiones de publicidad de Adobe Primetime responde con un documento SMIL (lenguaje de integración multimedia sincronizada) que contiene la información de publicidad requerida.

   Durante esta fase puede producirse una de las siguientes situaciones de failover:

   * Los datos no se pueden recuperar por motivos como la falta de conectividad o un error en el servidor, como por ejemplo un recurso, no se puede encontrar, etc.
   * Se recuperaron los datos, pero el formato no es válido.

      Esto puede ocurrir porque, por ejemplo, falló el análisis de los datos entrantes.
   El SDK del explorador emite una notificación de advertencia sobre el error y continúa el procesamiento.

## Fase de inserción de publicidad {#section_88A0E4FA12394717A9D85689BD11D59F}

El SDK del explorador inserta el contenido alternativo (publicidades) en la línea de tiempo que corresponde al contenido principal.

Cuando se completa la fase de resolución de publicidad, el SDK de TVSDK del explorador tiene una lista ordenada de los recursos publicitarios que se agrupan en saltos de publicidad. Cada pausa publicitaria se coloca en la línea de tiempo del contenido principal utilizando un valor de tiempo de inicio expresado en milisegundos (ms). Cada publicidad de una pausa publicitaria tiene una propiedad duration que también se expresa en ms. Las publicidades de una pausa publicitaria se encadenan una tras otra. Como resultado, la duración de una pausa publicitaria es igual a la suma de las duraciones de las publicidades compuestas individuales.

La conmutación por error puede ocurrir en esta fase con conflictos que pueden producirse en la línea de tiempo durante la inserción de anuncios. Para combinaciones específicas de valores de duración/tiempo del inicio de desglose de publicidad, los segmentos de publicidad podrían superponerse. La superposición se produce cuando la última parte de una pausa publicitaria se cruza con el principio del primer anuncio en la siguiente pausa publicitaria. En estas situaciones, el SDK de TVSDK del explorador descarta la pausa publicitaria posterior y continúa el proceso de inserción de publicidad con el siguiente elemento de la lista hasta que se insertan o descartan todos los saltos de publicidad.

El SDK del explorador emite una notificación de advertencia sobre el error y continúa el procesamiento.

## Fase de reproducción de publicidad {#section_7B0073BE9A744C74929263182C1243FC}

El SDK del explorador descarga los segmentos de publicidad y los procesa en la pantalla del dispositivo.

En este punto, el SDK de TVSDK del explorador ha resuelto las publicidades, las ha colocado en la línea de tiempo e intenta procesar el contenido en la pantalla.

En esta fase pueden producirse las siguientes clases principales de errores:

* Errores al conectarse al servidor host
* Errores al descargar el archivo de manifiesto
* Errores al descargar los segmentos de medios

Para las tres clases de error, el SDK de TVSDK del explorador reenvía eventos activados a la aplicación, incluidos:

* Eventos de notificación activados cuando se produce una conmutación por error.
* Eventos de notificación cuando se cambia el perfil debido al algoritmo de conmutación por error.
* Los eventos de notificación se activan cuando se consideran todas las opciones de conmutación por error y no se puede realizar ninguna acción adicional automáticamente.

   La aplicación debe realizar la acción adecuada.

Independientemente de si se producen errores o no, el SDK de TVSDK del explorador le notifica cuando se produce un inicio de pausa publicitaria y cuando se completa. Sin embargo, si no se pudieron descargar los segmentos, es posible que haya espacios en la línea de tiempo. Cuando los huecos son lo suficientemente grandes, los valores en la posición del cursor de reproducción y el progreso del anuncio informado pueden mostrar discontinuidades.
