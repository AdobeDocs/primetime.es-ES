---
description: La resolución de anuncios y la carga de anuncios pueden causar un retraso inaceptable para un usuario que espera a que se inicie la reproducción. Las funciones de Lazy Ad Loading y Lazy Ad Resolving pueden reducir este retraso del inicio. La resolución de publicidad diferida ha cambiado significativamente en la versión 3.0. En la carga de anuncios diferidos antes de la versión 3.0, la resolución de anuncios se dividió en dos pasos, resolviendo solo los anuncios previos a la emisión antes del estado PREPARADO y los anuncios intermedios y posteriores después del estado PREPARADO. Esto ha cambiado y las pausas publicitarias ahora se resuelven en un intervalo especificado antes de la posición de la pausa publicitaria.
keywords: Flotante;resolución de publicidad;carga de publicidad
title: Resolución de anuncios en tiempo real
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---


# Información general {#just-in-time-ad-resolving-overview}

La resolución de anuncios y la carga de anuncios pueden causar un retraso inaceptable para un usuario que espera a que se inicie la reproducción. Las funciones de Lazy Ad Loading y Lazy Ad Resolving pueden reducir este retraso del inicio. La resolución de publicidad diferida ha cambiado significativamente en la versión 3.0. En la carga de anuncios diferidos antes de la versión 3.0, la resolución de anuncios se dividió en dos pasos, resolviendo solo los anuncios previos a la emisión antes del estado PREPARADO y los anuncios intermedios y posteriores después del estado PREPARADO. Esto ha cambiado y las pausas publicitarias ahora se resuelven en un intervalo especificado antes de la posición de la pausa publicitaria.

* Proceso básico de resolución y carga de anuncios:

   1. TVSDK descarga un manifiesto (lista de reproducción) y *resuelve* todos los anuncios.
   1. TVSDK *carga* todos los anuncios y los coloca en la cronología.
   1. TVSDK mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.

   El reproductor utiliza las URL del manifiesto para obtener el contenido de la publicidad (creativos), garantiza que el contenido de la publicidad tenga un formato que TVSDK pueda reproducir y TVSDK coloca los anuncios en la cronología. Este proceso básico de resolución y carga de anuncios puede causar un retraso inaceptablemente largo para un usuario que espera reproducir su contenido, especialmente si el manifiesto contiene varias direcciones URL de anuncios.

* *Carga* de publicidad diferida:

   1. TVSDK descarga una lista de reproducción y *resuelve* todos los anuncios.
   1. TVSDK *carga* anuncios previos a la emisión, mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.
   1. TVSDK *carga* los anuncios restantes y los coloca en la cronología a medida que se produce la reproducción.

   Esta función mejora con respecto al proceso básico al poner el reproductor en el estado PREPARADO antes de cargar todos los anuncios.

* *Resolución de publicidad diferida*:

   1. TVSDK descarga la lista de reproducción.
   1. TVSDK resuelve y carga cualquier anuncio previo a la emisión, mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.
   1. TVSDK se resuelve y cada uno de los anuncios restantes se interrumpe individualmente en función del siguiente cálculo:

      `AdvertisingMetadata::getDelayAdLoadingTolerance() + PlayBufferTime::playBufferTime + the value defined in EXT-X-TARGETDURATION`

      De forma predeterminada, para el contenido con una duración de Target de 6 segundos, será de 5,0 + 30,0 + 6,0 segundos (41 segundos)

   1. Si se produce una pausa publicitaria en los 10 segundos posteriores a la posición de inicio, se resolverá junto con los anuncios previos a la emisión antes del estado PREPARADO.

>[!IMPORTANT]
>
>**Factores a tener en cuenta con la resolución de publicidad diferida:**
>
>* La resolución de anuncios diferidos solo es compatible con flujos de VOD con los modos SERVER_MAP y MANIFEST_CUES.
>* La resolución de publicidad diferida no está habilitada de forma predeterminada. Si está desactivado, todos los anuncios se resuelven en los flujos de VOD antes de que se inicie la reproducción.
>* La resolución de publicidad diferida es incompatible con la función Instant On. Para obtener más información sobre la activación instantánea, consulte Activación instantánea.
>* Con la resolución de publicidad diferida, mientras se intenta avanzar durante una pausa publicitaria, la pausa publicitaria más cercana a la posición de búsqueda se resolverá durante la búsqueda.
>* Con la resolución de publicidad diferida, si existen varias pausas publicitarias al mismo tiempo (VMAP), se resolverán al mismo tiempo.
>* No se recomienda reducir el valor de *setDelayAdLoadingTolerance() *por debajo del valor predeterminado (5 segundos). Si lo hace, el reproductor podría &quot;almacenar en búfer&quot; innecesariamente.
>* La resolución de anuncios diferidos no afecta a los anuncios previos a la emisión.
>* La resolución de publicidad diferida actualmente es compatible con el complemento Auditude-Plugin. Se recomienda no establecer *setDelayAdLoading* en true si utiliza una resolución personalizada.

>


