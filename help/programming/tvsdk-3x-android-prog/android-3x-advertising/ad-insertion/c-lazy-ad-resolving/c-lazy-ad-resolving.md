---
description: La resolución de anuncios y la carga de anuncios pueden provocar un retraso inaceptable para un usuario que espera a que se inicie la reproducción. Las funciones de carga diferida de publicidad y de resolución diferida de publicidad pueden reducir este retraso en el inicio. La resolución de anuncios diferidos ha cambiado significativamente en la versión 3.0. En la carga de publicidad diferida anterior a la 3.0, la resolución de la publicidad se dividía en dos pasos, que resolvían solo los anuncios previos a la emisión antes del estado PREPARADO y los anuncios intermedios y posteriores a la emisión después del estado PREPARADO. Esto ha cambiado y las pausas publicitarias ahora se resuelven en un intervalo especificado antes de la posición de la pausa publicitaria.
keywords: Diferido;Resolución de publicidad;Carga de publicidad
title: Resolución de anuncios Just-In-Time
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# Información general {#just-in-time-ad-resolving-overview}

La resolución de anuncios y la carga de anuncios pueden provocar un retraso inaceptable para un usuario que espera a que se inicie la reproducción. Las funciones de carga diferida de publicidad y de resolución diferida de publicidad pueden reducir este retraso en el inicio. La resolución de anuncios diferidos ha cambiado significativamente en la versión 3.0. En la carga de publicidad diferida anterior a la 3.0, la resolución de la publicidad se dividía en dos pasos, que resolvían solo los anuncios previos a la emisión antes del estado PREPARADO y los anuncios intermedios y posteriores a la emisión después del estado PREPARADO. Esto ha cambiado y las pausas publicitarias ahora se resuelven en un intervalo especificado antes de la posición de la pausa publicitaria.

* Proceso básico de resolución y carga de anuncios:

   1. TVSDK descarga un manifiesto (lista de reproducción) y *resuelve* todos los anuncios.
   1. TVSDK *cargas* todos los anuncios y los coloca en la cronología.
   1. TVSDK mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.

  El reproductor utiliza las direcciones URL del manifiesto para obtener el contenido del anuncio (creativos), garantiza que el contenido del anuncio esté en un formato que TVSDK pueda reproducir y TVSDK coloca los anuncios en la cronología. Este proceso básico de resolución y carga de anuncios puede causar un retraso inaceptablemente largo a un usuario que espera para reproducir su contenido, especialmente si el manifiesto contiene varias direcciones URL de publicidad.

* *Carga diferida de publicidad*:

   1. TVSDK descarga una lista de reproducción y *resuelve* todos los anuncios.
   1. TVSDK *cargas* anuncio previo a la emisión, mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.
   1. TVSDK *cargas* los anuncios restantes y los coloca en la cronología a medida que se produce la reproducción.

  Esta función mejora el proceso básico al poner el reproductor en el estado PREPARADO antes de que se carguen todos los anuncios.

* *Resolución de publicidad diferida*:

   1. TVSDK descarga la lista de reproducción.
   1. TVSDK resuelve y carga los anuncios previos a la emisión, mueve el reproductor al estado PREPARADO y se inicia la reproducción del contenido.
   1. TVSDK resuelve y cada uno de los anuncios restantes se divide individualmente en función del siguiente cálculo:

      `AdvertisingMetadata::getDelayAdLoadingTolerance() + PlayBufferTime::playBufferTime + the value defined in EXT-X-TARGETDURATION`

      De forma predeterminada, para el contenido con una duración de Target de 6 segundos, será 5,0 + 30,0 + 6,0 segundos (41 segundos)

   1. Si se produce una pausa publicitaria en los 10 segundos siguientes a la posición de inicio, esta se resolverá junto con los anuncios previos a la emisión antes del estado PREPARADO.

>[!IMPORTANT]
>
>**Factores a considerar con la resolución de anuncios diferidos:**
>
>* La resolución de anuncios diferidos solo se admite para flujos de VOD con los modos SERVER_MAP y MANIFEST_CUES.
>* La resolución de anuncios diferidos no está activada de forma predeterminada. Si está desactivado, todos los anuncios se resuelven en emisiones de VOD antes de que comience la reproducción.
>* La resolución de anuncios diferida no es compatible con la función Encendido instantáneo. Para obtener más información acerca de Instant On, consulte Instant On.
>* Con la resolución de anuncios diferidos, mientras se busca hacia delante durante una pausa publicitaria, la pausa publicitaria más cercana a la posición de búsqueda se resolverá durante la búsqueda.
>* Con la resolución de anuncios diferidos, si existen varias pausas publicitarias al mismo tiempo (VMAP), se resolverán al mismo tiempo.
>* No se recomienda reducir el valor de *setDelayAdLoadingTolerance() *por debajo del valor predeterminado (5 segundos). Si lo hace, el reproductor podría &quot;amortiguar&quot; innecesariamente.
>* La resolución diferida de anuncios no afecta a los anuncios previos a la emisión.
>* Actualmente, la resolución de anuncios diferidos es compatible con el complemento Auditude. Se recomienda no configurar *setDelayAdLoading* como true si utiliza una resolución personalizada.
>
