---
description: Un reproductor de vídeo del cliente o el servidor de manifiesto pueden interactuar con CRS para lograr un reempaquetado JIT. Ambos utilizan la misma lógica de selección de anuncios.
title: Flujos de trabajo detallados para el reempaquetado JIT
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# Flujos de trabajo detallados para el reempaquetado JIT {#detailed-workflows-for-jit-repackaging}

Un reproductor de vídeo del cliente o el servidor de manifiesto pueden interactuar con CRS para lograr un reempaquetado JIT. Ambos utilizan la misma lógica de selección de anuncios.

## Reempaquetado JIT iniciado por el servidor de manifiestos {#section_1F1C1B7DD146403890C2B43E24FEF0EB}

![](assets/ssai_JIT-workflow_web.png)

El flujo de trabajo para el reempaquetado JIT en el lado del servidor de manifiesto es el siguiente:

1. El servidor de manifiesto realiza una solicitud al servidor de publicidad.
1. El servidor de manifiesto recibe un creativo de publicidad que no está en formato HLS.
1. El servidor de manifiesto envía una solicitud al servidor CDN para una versión HLS previamente transcodificada del creativo de publicidad.

   >[!NOTE]
   >
   >En una configuración de varias CDN, el servidor de manifiesto utiliza el `ptcdn` en la URL de bootstrap para identificar el servidor CDN.

1. El servidor de manifiesto comprueba la respuesta:

   1. Si la solicitud se realiza correctamente, el servidor de manifiesto inserta la versión HLS transcodificada anteriormente del creativo de publicidad en el flujo de contenido.
   1. Si la solicitud falla, el servidor de manifiesto genera una entrada de registro y solicita una versión transcodificada desde CRS.

1. CRS transcodifica el creativo de publicidad y carga la versión HLS en el servidor CDN para su uso futuro.

Para todas las solicitudes posteriores de ese creativo, el servidor de manifiesto recupera la versión de HLS de la CDN y la inserta en el flujo de contenido.

## Reempaquetado JIT iniciado por el cliente {#section_FBC97D40043F4FDD98247A08BB6195B0}

<!--<a id="fig_hkn_ndt_3z"></a>-->

![](assets/ssai_JIT-workflow_client_web.png)

Un cliente basado en TVSDK o con capacidades similares puede interactuar con CRS para lograr el reempaquetado JIT de la siguiente manera:

1. El cliente solicita un anuncio del servidor de publicidad.
1. El servidor de publicidad devuelve el anuncio al cliente.
1. El cliente comprueba el formato de la publicidad desde el servidor de publicidad:

   1. Si el creador de la publicidad está en formato HLS, el cliente lo inserta (vincula) en el contenido y lo hace.
   1. Si el creador de la publicidad no está en formato HLS, el cliente solicita una desde el servidor CDN.

      >[!NOTE]
      >
      >En una configuración de varias CDN, el servidor de manifiesto utiliza el `ptcdn` en la URL de bootstrap para identificar el servidor CDN.

1. El cliente comprueba la respuesta del servidor CDN.

   1. Si la CDN proporcionó una versión de HLS, el cliente la inserta (vincula) en el contenido y lo hace.
   1. Si el servidor CDN no proporciona una versión HLS, el cliente solicita al servidor de publicidad que solicite una a CRS. El cliente no inserta el anuncio en el contenido.

1. El servidor de publicidad solicita que los anuncios que no son HLS se transcodificen en HLS.
1. CRS crea una versión de HLS y la carga en el servidor CDN para su uso futuro.

## Prioridades y cronología de formato de anuncio clasificado {#section_A74DE37A57BF45D7B6D09E3DE40F8E61}

El servidor de manifiesto y el cliente utilizan la misma lógica de selección para determinar las prioridades de reproducción de los anuncios disponibles. Los anuncios con formato HLS son de primera prioridad, seguidos de MP4, FLV y, finalmente, WebM.

CRS generalmente requiere de 2 a 4 minutos para procesar un anuncio creativo que no sea de HLS y, por lo general, menos de 3 minutos.

CRS produce diferentes velocidades de bits HLS, por lo que el anuncio puede reproducir a una velocidad adecuada para la velocidad de conexión y el ancho de banda disponibles. Si hay varias velocidades de bits disponibles, CRS elige la velocidad de bits más alta disponible. Si CRS recibe un anuncio creativo que no es de HLS, produce una versión de HLS con la resolución más alta disponible.