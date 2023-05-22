---
description: Más allá de los parámetros de consulta básicos, los parámetros de consulta opcionales permiten que el servidor de manifiesto funcione con distintos clientes y situaciones.
title: Parámetros de consulta opcionales por cliente y situación
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---


# Parámetros de consulta opcionales por cliente y situación {#optional-query-parameters-by-client-and-situation}

Más allá de los parámetros de consulta básicos, los parámetros de consulta opcionales permiten que el servidor de manifiesto funcione con distintos clientes y situaciones.

## Inserción de anuncios con Akamai Ad Scaler {#section_120FEC75C34D4F4587B77D842166D68A}

En la red de entrega de contenido (CDN) de Akamai, el servidor perimetral de Akamai funciona como intermediario entre el cliente y el servidor de manifiesto. Si también utiliza Ad Scaler, la variable `ptassetid` y `live` Los parámetros de consulta proporcionan la información necesaria a Akamai Edge.

El `ptassetid` parámetro es el ID del editor de su recurso. Akamai utiliza esta dirección URL, en lugar de la URL codificada en Base64 que se proporciona como parte de la dirección URL de solicitud, para identificar la lista de reproducción que se debe proporcionar al servidor de manifiesto para la inserción de publicidad.

El `live` distingue entre contenido en directo y vídeo bajo demanda (VOD). El servidor de manifiestos necesita esta información para admitir su interfaz optimizada con Akamai.

Esta es una URL de ejemplo que muestra los parámetros pertenecientes a Akamai:

```
https://. . .master.m3u8?. . .&ptassetid=pubAsset&live=true
```

## Inserción de anuncios desde TVSDK en Xbox {#section_5DB405F4647240A0B83E72DE35D5EC80}

Un reproductor basado en TVSDK de Primetime en Xbox no necesita proporcionar parámetros de consulta adicionales más allá de los básicos.

## Inserción de anuncios desde TVSDK en iOS con Safari {#section_250E493A125E4F82940D19C7DA2AAB2E}

Un reproductor basado en TVSDK de Primetime en iOS que utilice el explorador Safari debe especificar `ptplayer` y `live` además de los parámetros de consulta básicos.

El servidor de manifiestos reconoce el `ptplayer` valor `ios-mobileweb` y elimina el anuncio previo a la emisión del manifiesto vinculado a publicidad que devuelve.

El `live` indica al servidor de manifiesto si se debe devolver contenido en directo o de VOD.

Esta es una URL de ejemplo que muestra los parámetros correspondientes a iOS con Safari:

```URL
https://. . .master.m3u8?. . .&ptplayer=ios-mobileweb&live=false
```

## Inserción de publicidad con un formato personalizado de referencia de publicidad {#section_82AF880AAABE4BD4B593D906434D4D89}

El Adobe proporciona nombres para formatos de referencia de anuncio que no admite directamente en el paquete de Primetime. Para utilizar un formato de este tipo, proporcione su nombre proporcionado por el Adobe como el valor del `ptcueformat` parámetro.

Esta es una URL de ejemplo que especifica un formato personalizado de referencia de anuncio:

```URL
https://. . .master.m3u8?. . .&ptcueformat=[custom format name]
```

## Inserción de anuncios con indicaciones de anuncio para crear una cronología de FreeWheel para VOD {#section_E0D830F5EEE24639819B975B90F6999F}

Para que el contenido de VOD que contiene señales de anuncio se analice e incluya en una solicitud de anuncio de FreeWheel, establezca el valor de `ptcueformat` parámetro a `DPIsimple`.

Esta es una URL de ejemplo que especifica el uso de una cronología de FreeWheel para VOD:

```URL
https://. . .master.m3u8?. . .&ptcueformat=DPISimple&live=false
```

## Inserción de publicidad con una cronología personalizada para VOD {#section_F398F7659164463FA886A4CC787C7B5A}

Para solicitar al servidor de manifiesto que inserte anuncios en el contenido de VOD según la cronología proporcionada, establezca el valor de `pttimeline` a una cadena que especifica la cronología. Consulte [Formato de cronología de VOD](/help/primetime-ad-insertion/~old-msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md).

Esta es una URL de ejemplo que utiliza una cronología personalizada para VOD:

```URL
https://. . .master.m3u8?. . .&live=false&pttimeline=B,60,2,p;C,120,1;B,30,2,m;C,300,1
```

Especifica una pausa inicial de un minuto que contiene hasta dos anuncios, seguida de un segmento de contenido de dos minutos, seguida de una pausa de 30 segundos que contiene hasta dos anuncios, seguida de un segmento de contenido de cinco minutos.

La vinculación de anuncios para una cronología de contenido personalizada para contenido de VOD se comporta de la siguiente manera:

* El anuncio aparece en el límite de salto más cercano después del tiempo de colocación de anuncio especificado por el servidor de publicidad.

* Los segmentos duran al menos dos segundos.

## Autorizar segmentos TS {#section_BF855A4399DC42CB8C0586113A416BBC}

Adobe solo admite esta función para la CDN de Akamai. El streaming en vivo HTTP (HLS) ofrece segmentos de flujo de transporte (TS) usando una lista de reproducción M3U8 de nivel de flujo. Se proporcionan al cliente varias listas de reproducción de nivel de flujo en una lista de reproducción de variante M3U8. El cliente selecciona una secuencia de lista de reproducción de la lista de variantes y, a continuación, descarga uno a uno los segmentos TS en esa lista de reproducción de nivel de secuencia. En condiciones normales de funcionamiento, el contenido solicitado puede requerir la autorización de cookies, que el servidor de manifiestos gestiona de forma invisible en segundo plano. Extrae la cookie del contenido sin procesar y anexa un token adecuado a la URL que se utilizará para solicitar el flujo de lista de reproducción seleccionado.

Cuando los parámetros de consulta de URL del Bootstrap incluyen `pttoken=true`Sin embargo, el editor requiere una cookie para utilizar en la solicitud de cada segmento de TS, en lugar de solo una vez para todo el flujo. El servidor de manifiesto adjunta esta cookie como un parámetro de consulta a cada URL de segmento TS en la lista de reproducción de flujo que envía.
