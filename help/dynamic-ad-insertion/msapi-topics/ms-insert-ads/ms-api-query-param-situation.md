---
description: Más allá de los parámetros de consulta básicos, los parámetros de consulta opcionales permiten que el servidor de manifiesto funcione con diferentes clientes y situaciones.
seo-description: Más allá de los parámetros de consulta básicos, los parámetros de consulta opcionales permiten que el servidor de manifiesto funcione con diferentes clientes y situaciones.
seo-title: Parámetros de consulta opcionales por cliente y situación
title: Parámetros de consulta opcionales por cliente y situación
uuid: e3fae41e-9f7d-4f01-9a01-52a1d5f5dad5
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---


# Parámetros de consulta opcionales por cliente y situación {#optional-query-parameters-by-client-and-situation}

Más allá de los parámetros de consulta básicos, los parámetros de consulta opcionales permiten que el servidor de manifiesto funcione con diferentes clientes y situaciones.

## Inserción de publicidad con el escalador de publicidad Akamai {#section_120FEC75C34D4F4587B77D842166D68A}

En la red de envío de contenido de Akamai (CDN), el servidor de Akamai Edge funciona como intermediario entre el cliente y el servidor de manifiesto. Si también utiliza el escalador de publicidad, los parámetros de consulta `ptassetid` y `live` proporcionan la información necesaria a Akamai Edge.

El parámetro `ptassetid` es el ID del editor para su recurso. Akamai utiliza esta URL, en lugar de la URL con codificación base64 que se proporciona como parte de la URL de solicitud, para identificar la lista de reproducción que se debe proporcionar al servidor de manifiesto para la inserción de anuncios.

El parámetro `live` distingue entre contenido en directo y vídeo a petición (VOD). El servidor de manifiesto necesita esta información para admitir su interfaz optimizada con Akamai.

Esta es una URL de muestra que muestra los parámetros que pertenecen a Akamai:

```
https://. . .master.m3u8?. . .&ptassetid=pubAsset&live=true
```

## Inserción de publicidad desde TVSDK en Xbox {#section_5DB405F4647240A0B83E72DE35D5EC80}

Un reproductor basado en Primetime TVSDK en Xbox no necesita proporcionar parámetros de consulta adicionales más allá de los básicos.

## Inserción de anuncios desde TVSDK en iOS con Safari {#section_250E493A125E4F82940D19C7DA2AAB2E}

Un reproductor basado en Primetime TVSDK en iOS que utilice el navegador Safari debe especificar los parámetros `ptplayer` y `live` además de los parámetros de consulta básicos.

El servidor de manifiesto reconoce el valor `ptplayer` `ios-mobileweb` y elimina el registro previo del manifiesto con la publicidad que devuelve.

El parámetro `live` indica al servidor de manifiesto si debe devolver contenido activo o VOD.

Esta es una URL de muestra que muestra los parámetros que pertenecen a iOS con Safari:

```
https://. . .master.m3u8?. . .&ptplayer=ios-mobileweb&live=false
```

## Inserción de anuncios con un formato de aviso de publicidad personalizado {#section_82AF880AAABE4BD4B593D906434D4D89}

Adobe proporciona nombres para los formatos de señal de publicidad que no admite directamente en el paquete Primetime. Para utilizar este formato, proporcione el nombre proporcionado por el Adobe como valor del parámetro `ptcueformat`.

A continuación se muestra una URL de ejemplo que especifica un formato de señal de anuncio personalizado:

```
https://. . .master.m3u8?. . .&ptcueformat=[custom format name]
```

## Inserción de anuncios con indicaciones de anuncios para crear una línea de tiempo de FreeWheel para VOD {#section_E0D830F5EEE24639819B975B90F6999F}

Para que el contenido de VOD que contenga indicaciones de publicidad se analice e incluya en una solicitud de publicidad de FreeWheel, establezca el valor del parámetro `ptcueformat` en `DPIsimple`.

Esta es una URL de ejemplo que especifica el uso de una línea de tiempo de FreeWheel para VOD:

```
https://. . .master.m3u8?. . .&ptcueformat=DPISimple&live=false
```

## Inserción de anuncios con una línea de tiempo personalizada para VOD {#section_F398F7659164463FA886A4CC787C7B5A}

Para solicitar al servidor de manifiesto que inserte publicidades en el contenido de VOD según la línea de tiempo proporcionada, establezca el valor del parámetro `pttimeline` en una cadena que especifique la línea de tiempo. Consulte [Formato de línea de tiempo de VOD](../../msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)

Esta es una URL de ejemplo que utiliza una línea de tiempo personalizada para VOD:

```
https://. . .master.m3u8?. . .&live=false&pttimeline=B,60,2,p;C,120,1;B,30,2,m;C,300,1
```

Especifica un salto inicial de un minuto que contiene hasta dos anuncios, seguido de un segmento de contenido de dos minutos, seguido de un desglose de 30 segundos que contiene hasta dos anuncios, seguido de un segmento de contenido de cinco minutos.

La identificación de anuncios para una línea de tiempo de contenido personalizado para contenido de VOD se comporta de la siguiente manera:

* La publicidad aparece en el límite de salto más cercano después del tiempo de colocación de publicidad especificado por el servidor de publicidad.
* Los segmentos duran al menos dos segundos.

## Autorización de segmentos TS {#section_BF855A4399DC42CB8C0586113A416BBC}

Adobe solo admite esta función para la CDN de Akamai. El flujo en directo HTTP (HLS) ofrece segmentos de flujo de transporte (TS) mediante una lista de reproducción M3U8 de nivel de flujo. Se proporcionan varias listas de reproducción de nivel de flujo al cliente en una lista de reproducción variante M3U8. El cliente selecciona un flujo de lista de reproducción de la lista variante y, a continuación, descarga segmentos de TS en esa lista de reproducción de nivel de flujo uno a uno. En un funcionamiento normal, el contenido solicitado puede requerir la autorización de cookies, que el servidor de manifiesto gestiona de forma invisible en segundo plano. Extrae la cookie del contenido sin procesar y anexa un token apropiado a la URL que se utilizará al solicitar el flujo de la lista de reproducción seleccionada.

Cuando los parámetros de consulta de URL de Bootstrap incluyen `pttoken=true`, el editor requiere que se utilice una cookie para solicitar cada segmento de TS, en lugar de una sola vez para todo el flujo. El servidor de manifiesto adjunta esta cookie como parámetro de consulta a cada URL de segmento de TS en la lista de reproducción de flujo que devuelve.
