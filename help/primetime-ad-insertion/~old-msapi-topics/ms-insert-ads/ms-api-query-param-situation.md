---
description: Más allá de los parámetros de consulta básicos, los parámetros de consulta opcionales permiten que el servidor de manifiesto funcione con diferentes clientes y situaciones.
title: Parámetros de consulta opcionales por cliente y situación
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---


# Parámetros de consulta opcionales por cliente y situación {#optional-query-parameters-by-client-and-situation}

Más allá de los parámetros de consulta básicos, los parámetros de consulta opcionales permiten que el servidor de manifiesto funcione con diferentes clientes y situaciones.

## Inserción de publicidad con el escalador de anuncios de Akamai {#section_120FEC75C34D4F4587B77D842166D68A}

En la red de entrega de contenido (CDN) de Akamai, el servidor de Akamai Edge funciona como intermediario entre el cliente y el servidor de manifiesto. Si también utiliza el escalador de anuncios, los parámetros de consulta `ptassetid` y `live` proporcionan la información necesaria a Akamai Edge.

El parámetro `ptassetid` es el ID del editor para su recurso. Akamai utiliza esta URL, en lugar de la URL con codificación base64 que se proporciona como parte de la URL de solicitud, para identificar la lista de reproducción que se debe proporcionar al servidor de manifiesto para la inserción de anuncios.

El parámetro `live` distingue entre contenido en directo y vídeo bajo demanda (VOD). El servidor de manifiesto necesita esta información para admitir su interfaz optimizada con Akamai.

Esta es una URL de ejemplo que muestra los parámetros que pertenecen a Akamai:

```
https://. . .master.m3u8?. . .&ptassetid=pubAsset&live=true
```

## Inserción de publicidad desde TVSDK en Xbox {#section_5DB405F4647240A0B83E72DE35D5EC80}

Un reproductor basado en TVSDK de Primetime en Xbox no necesita proporcionar parámetros de consulta adicionales más allá de los básicos.

## Inserción de publicidad desde TVSDK en iOS con Safari {#section_250E493A125E4F82940D19C7DA2AAB2E}

Un reproductor basado en TVSDK de Primetime en iOS que utilice el explorador Safari debe especificar los parámetros `ptplayer` y `live` además de los parámetros de consulta básicos.

El servidor de manifiestos reconoce el valor `ptplayer` `ios-mobileweb` y elimina el anuncio previo a la emisión del manifiesto identificado que devuelve.

El parámetro `live` indica al servidor de manifiesto si debe devolver contenido activo o VOD.

Esta es una URL de ejemplo que muestra los parámetros que pertenecen a iOS con Safari:

```URL
https://. . .master.m3u8?. . .&ptplayer=ios-mobileweb&live=false
```

## Inserción de publicidad con un formato de señal de anuncio personalizado {#section_82AF880AAABE4BD4B593D906434D4D89}

Adobe proporciona nombres para formatos de señal de anuncio que no admite directamente en el paquete Primetime. Para utilizar este formato, proporcione su nombre proporcionado por el Adobe como el valor del parámetro `ptcueformat`.

Esta es una URL de ejemplo que especifica un formato de señal de anuncio personalizado:

```URL
https://. . .master.m3u8?. . .&ptcueformat=[custom format name]
```

## Inserción de publicidad utilizando señales de publicidad para crear una cronología de FreeWheel para VOD {#section_E0D830F5EEE24639819B975B90F6999F}

Para el contenido de VOD que contenga indicaciones de anuncio que se van a analizar e incluir en una solicitud de publicidad de FreeWheel, establezca el valor del parámetro `ptcueformat` en `DPIsimple`.

Esta es una URL de ejemplo que especifica el uso de una línea de tiempo de FreeWheel para VOD:

```URL
https://. . .master.m3u8?. . .&ptcueformat=DPISimple&live=false
```

## Inserción de anuncios con una cronología personalizada para VOD {#section_F398F7659164463FA886A4CC787C7B5A}

Para pedir al servidor de manifiesto que inserte anuncios en el contenido de VOD según la cronología proporcionada, establezca el valor del parámetro `pttimeline` en una cadena que especifique la cronología. Consulte [Formato de cronología de VOD](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md).

Esta es una URL de ejemplo que utiliza una cronología personalizada para VOD:

```URL
https://. . .master.m3u8?. . .&live=false&pttimeline=B,60,2,p;C,120,1;B,30,2,m;C,300,1
```

Especifica una pausa inicial de un minuto que contiene hasta dos anuncios, seguida de un segmento de contenido de dos minutos, seguido de una pausa de 30 segundos que contiene hasta dos anuncios, seguidos de un segmento de contenido de cinco minutos.

La vinculación de anuncios para una línea de tiempo de contenido personalizada para contenido de VOD se comporta de la siguiente manera:

* El anuncio aparece en el límite de salto más cercano después del tiempo de colocación de anuncio especificado por el servidor de publicidad.

* Los segmentos tienen una duración de al menos dos segundos.

## Autorización de segmentos de TS {#section_BF855A4399DC42CB8C0586113A416BBC}

Adobe solo admite esta función para la CDN de Akamai. El flujo en directo HTTP (HLS) envía segmentos de flujo de transporte (TS) utilizando una lista de reproducción M3U8 de nivel de flujo. Se proporcionan al cliente varias listas de reproducción de nivel de flujo en una lista de reproducción de la variante M3U8. El cliente selecciona un flujo de lista de reproducción de la lista de variantes y, a continuación, descarga segmentos TS en esa lista de reproducción de nivel de flujo uno a uno. En un funcionamiento normal, el contenido solicitado puede requerir la autorización de cookies, que el servidor de manifiestos gestiona de forma invisible en segundo plano. Extrae la cookie del contenido sin procesar y adjunta un token apropiado a la URL que se utilizará para solicitar el flujo de la lista de reproducción seleccionada.

Cuando los parámetros de consulta de URL del Bootstrap incluyen `pttoken=true`, el editor requiere que se utilice una cookie para solicitar cada segmento de TS, en lugar de solo una vez para todo el flujo. El servidor de manifiestos adjunta esta cookie como parámetro de consulta a cada URL de segmento TS en la lista de reproducción de flujo que envía.
