---
description: Un reproductor de vídeo cliente o el servidor de manifiesto pueden interactuar con CRS para lograr el reempaquetado JIT. Ambos utilizan la misma lógica de selección de publicidad.
seo-description: Un reproductor de vídeo cliente o el servidor de manifiesto pueden interactuar con CRS para lograr el reempaquetado JIT. Ambos utilizan la misma lógica de selección de publicidad.
seo-title: Flujos de trabajo detallados para el reempaquetado JIT
title: Flujos de trabajo detallados para el reempaquetado JIT
uuid: 11b6eb3c-f6aa-4018-9b20-ab6f5910508b
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# Flujos de trabajo detallados para el reempaquetado JIT {#detailed-workflows-for-jit-repackaging}

Un reproductor de vídeo cliente o el servidor de manifiesto pueden interactuar con CRS para lograr el reempaquetado JIT. Ambos utilizan la misma lógica de selección de publicidad.

## Reempaquetado JIT iniciado por el servidor de manifiestos {#section_1F1C1B7DD146403890C2B43E24FEF0EB}

![](assets/ssai_JIT-workflow_web.png)

El flujo de trabajo para el reempaquetado JIT en el servidor de manifiesto es el siguiente:

1. El servidor de manifiesto realiza una solicitud al servidor de publicidad.
1. El servidor de manifiesto recibe un elemento creativo de publicidad que no está en formato HLS.
1. El servidor de manifiesto envía una solicitud al servidor CDN para una versión HLS previamente transcodificada del elemento creativo de la publicidad.

   >[!NOTE]
   >
   >En una configuración multiCDN, el servidor de manifiesto utiliza el `ptcdn` parámetro en la URL de arranque para identificar el servidor CDN.

1. El servidor de manifiesto comprueba la respuesta:

   1. Si la solicitud se realiza correctamente, el servidor de manifiesto inserta la versión HLS previamente transcodificada del elemento creativo de publicidad en el flujo de contenido.
   1. Si la solicitud falla, el servidor de manifiesto genera una entrada de registro y solicita una versión transcodificada de CRS.

1. CRS transcodifica el elemento creativo de la publicidad y carga la versión de HLS en el servidor CDN para su uso futuro.

Para todas las solicitudes posteriores de ese elemento creativo, el servidor de manifiesto recupera la versión HLS de la CDN y la inserta en el flujo de contenido.

## Reempaquetado JIT iniciado por el cliente {#section_FBC97D40043F4FDD98247A08BB6195B0}

<!--<a id="fig_hkn_ndt_3z"></a>-->

![](assets/ssai_JIT-workflow_client_web.png)

Un cliente basado en TVSDK o con capacidades similares puede interactuar con CRS para lograr el reempaquetado JIT, como se indica a continuación:

1. El cliente solicita una publicidad desde el servidor de publicidad.
1. El servidor de publicidad devuelve la publicidad al cliente.
1. El cliente comprueba el formato de la publicidad desde el servidor de publicidad:

   1. Si el elemento creativo de la publicidad está en formato HLS, el cliente lo inserta (lo pone en puntos) en el contenido y se realiza.
   1. Si el elemento creativo de la publicidad no está en formato HLS, el cliente solicita uno desde el servidor CDN.

      >[!NOTE]
      >
      >En una configuración multiCDN, el servidor de manifiesto utiliza el `ptcdn` parámetro en la URL de arranque para identificar el servidor CDN.

1. El cliente comprueba la respuesta desde el servidor CDN.

   1. Si la CDN ha proporcionado una versión de HLS, el cliente la inserta (establece puntos) en el contenido y se realiza.
   1. Si el servidor CDN no proporciona una versión HLS, el cliente solicita al servidor de publicidad que solicite una de CRS. El cliente no inserta la publicidad en el contenido.

1. El servidor de publicidad solicita que se transcodifique el no HLS a HLS.
1. CRS crea una versión HLS y la carga en el servidor CDN para su uso futuro.

## Prioridades y cronología del formato de publicidad {#section_A74DE37A57BF45D7B6D09E3DE40F8E61}

El servidor de manifiesto y el cliente utilizan la misma lógica de selección para determinar las prioridades para reproducir publicidades disponibles. Los anuncios con formato HLS son de primera prioridad, seguidos de MP4, FLV y finalmente WebM.

CRS generalmente requiere de 2 a 4 minutos para procesar un elemento creativo de publicidad que no sea HLS y, por lo general, menos de 3 minutos.

CRS produce diferentes velocidades de bits HLS, de modo que el anuncio puede reproducirse a una velocidad adecuada a la velocidad de conexión y al ancho de banda disponibles. Si hay varias velocidades de bits disponibles, CRS elige la velocidad de bits más alta disponible. Si CRS recibe un elemento creativo de publicidad que no es HLS, produce una versión HLS con la máxima resolución disponible.