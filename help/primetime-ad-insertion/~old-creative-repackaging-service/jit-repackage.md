---
description: Un reproductor de vídeo cliente o el servidor de manifiesto pueden interactuar con CRS para lograr el reempaquetado de JIT. Ambos utilizan la misma lógica de selección de anuncios.
title: Flujos de trabajo detallados para el reempaquetado de JIT
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# Flujos de trabajo detallados para el reempaquetado de JIT {#detailed-workflows-for-jit-repackaging}

Un reproductor de vídeo cliente o el servidor de manifiesto pueden interactuar con CRS para lograr el reempaquetado de JIT. Ambos utilizan la misma lógica de selección de anuncios.

## Reempaquetado de JIT iniciado por el servidor de manifiesto {#section_1F1C1B7DD146403890C2B43E24FEF0EB}

![](assets/ssai_JIT-workflow_web.png)

El flujo de trabajo para el reempaquetado de JIT en el servidor de manifiesto es el siguiente:

1. El servidor de manifiesto realiza una solicitud al servidor de publicidad.
1. El servidor de manifiesto recibe un creativo de publicidad que no está en formato HLS.
1. El servidor de manifiesto envía una solicitud al servidor de CDN para una versión HLS previamente transcodificada del creativo de publicidad.

   >[!NOTE]
   >
   >En una configuración de varias CDN, el servidor de manifiesto utiliza el parámetro `ptcdn` en la URL de arranque para identificar el servidor de CDN.

1. El servidor de manifiesto comprueba la respuesta:

   1. Si la solicitud se realiza correctamente, el servidor de manifiesto inserta la versión HLS previamente transcodificada del creativo de publicidad en el flujo de contenido.
   1. Si la solicitud falla, el servidor de manifiestos genera una entrada de registro y solicita una versión transcodificada desde CRS.

1. CRS transcodifica el creativo de publicidad y carga la versión HLS en el servidor CDN para uso futuro.

Para todas las solicitudes posteriores de ese creativo, el servidor de manifiesto recupera la versión HLS de la CDN y la inserta en el flujo de contenido.

## Reempaquetado de JIT iniciado por el cliente {#section_FBC97D40043F4FDD98247A08BB6195B0}

<!--<a id="fig_hkn_ndt_3z"></a>-->

![](assets/ssai_JIT-workflow_client_web.png)

Un cliente basado en TVSDK o con capacidades similares puede interactuar con CRS para lograr el reempaquetado de JIT, como se indica a continuación:

1. El cliente solicita una publicidad desde el servidor de publicidad.
1. El servidor de publicidad devuelve el anuncio al cliente.
1. El cliente comprueba el formato de la publicidad desde el servidor de publicidad:

   1. Si el creativo de publicidad está en formato HLS, el cliente lo inserta (puntos) en el contenido y se ha completado.
   1. Si el creativo de la publicidad no está en formato HLS, el cliente solicita uno del servidor CDN.

      >[!NOTE]
      >
      >En una configuración de varias CDN, el servidor de manifiesto utiliza el parámetro `ptcdn` en la URL de arranque para identificar el servidor de CDN.

1. El cliente comprueba la respuesta desde el servidor de CDN.

   1. Si la CDN ha proporcionado una versión HLS, el cliente la inserta (puntos) en el contenido y se completa.
   1. Si el servidor CDN no proporciona una versión HLS, el cliente solicita al servidor de publicidad que solicite una de CRS. El cliente no inserta la publicidad en el contenido.

1. El servidor de publicidad solicita que el no HLS se transcodifique a HLS.
1. CRS crea una versión HLS y la carga en el servidor CDN para uso futuro.

## Prioridades de formato de publicidad y línea de tiempo {#section_A74DE37A57BF45D7B6D09E3DE40F8E61}

El servidor de manifiesto y el cliente utilizan la misma lógica de selección para determinar las prioridades de reproducción de los anuncios disponibles. Los anuncios con formato HLS son de primera prioridad, seguidos de MP4, FLV y finalmente WebM.

CRS generalmente requiere de 2 a 4 minutos para procesar un creativo de publicidad que no sea HLS y, por lo general, menos de 3 minutos.

CRS produce diferentes velocidades de bits HLS, por lo que el anuncio puede reproducirse a una velocidad adecuada para la velocidad de conexión y el ancho de banda disponibles. Si hay varias tasas de bits disponibles, CRS elige la tasa de bits más alta disponible. Si CRS recibe un creativo publicitario que no sea HLS, produce una versión HLS con la máxima resolución disponible.