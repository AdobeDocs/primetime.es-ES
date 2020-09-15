---
description: La resolución y carga de anuncios puede provocar un retraso inaceptable para un usuario que espera la reproducción en el inicio. Las funciones de carga de publicidad diferida y resolución de publicidad diferida pueden reducir este retraso de inicio. La resolución diferida de publicidad ha cambiado significativamente en la versión 3.0. En la carga de anuncios diferidos antes de la 3.0, la resolución de anuncios se desglosó en dos pasos, resolviendo solo las publicidades anteriores al estado PREPARADO y las versiones intermedias y posteriores después del estado PREPARADO. Esto ha cambiado y los saltos de publicidad ahora se resuelven en un intervalo especificado antes de la posición de la pausa publicitaria.
keywords: Lazy;Ad resolving;Ad loading
seo-description: La resolución y carga de anuncios puede provocar un retraso inaceptable para un usuario que espera la reproducción en el inicio. Las funciones de carga de publicidad diferida y resolución de publicidad diferida pueden reducir este retraso de inicio. La resolución diferida de publicidad ha cambiado significativamente en la versión 3.0. En la carga de anuncios diferidos antes de la 3.0, la resolución de anuncios se desglosó en dos pasos, resolviendo solo las publicidades anteriores al estado PREPARADO y las versiones intermedias y posteriores después del estado PREPARADO. Esto ha cambiado y los saltos de publicidad ahora se resuelven en un intervalo especificado antes de la posición de la pausa publicitaria.
seo-title: Resolución de publicidad puntual
title: Resolución de publicidad puntual
uuid: 77028f6e-7e53-45d1-bcc0-54f8224d6d18
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---


# Información general {#just-in-time-ad-resolving-overview}

La resolución y carga de anuncios puede provocar un retraso inaceptable para un usuario que espera la reproducción en el inicio. Las funciones de carga de publicidad diferida y resolución de publicidad diferida pueden reducir este retraso de inicio. La resolución diferida de publicidad ha cambiado significativamente en la versión 3.0. En la carga de anuncios diferidos antes de la 3.0, la resolución de anuncios se desglosó en dos pasos, resolviendo solo las publicidades anteriores al estado PREPARADO y las versiones intermedias y posteriores después del estado PREPARADO. Esto ha cambiado y los saltos de publicidad ahora se resuelven en un intervalo especificado antes de la posición de la pausa publicitaria.

* Proceso básico de resolución y carga de anuncios:

   1. TVSDK descarga un manifiesto (lista de reproducción) y *resuelve* todas las publicidades.
   1. TVSDK *carga* todas las publicidades y las coloca en la línea de tiempo.
   1. TVSDK mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.

   El reproductor utiliza las direcciones URL del manifiesto para obtener el contenido de la publicidad (elementos creativos), garantiza que el contenido de la publicidad tenga un formato que TVSDK pueda reproducir y TVSDK coloca las publicidades en la línea de tiempo. Este proceso básico de resolución y carga de publicidades puede provocar un retraso inaceptablemente prolongado para un usuario que espera reproducir su contenido, especialmente si el manifiesto contiene varias direcciones URL de publicidad.

* *Carga* diferida de publicidad:

   1. TVSDK descarga una lista de reproducción y *resuelve* todas las publicidades.
   1. TVSDK *carga* anuncios preliminares, mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.
   1. TVSDK *carga* el resto de las publicidades y las coloca en la línea de tiempo a medida que se produce la reproducción.

   Esta función mejora el proceso básico al colocar el reproductor en el estado PREPARADO antes de que se carguen todas las publicidades.

* *Resolución* de publicidad diferida:

   1. TVSDK descarga la lista de reproducción.
   1. TVSDK resuelve y carga cualquier anuncio previo, mueve el reproductor al estado PREPARADO y comienza la reproducción del contenido.
   1. TVSDK se resuelve y cada uno de los anuncios restantes se interrumpe individualmente según el siguiente cálculo:

      `AdvertisingMetadata::getDelayAdLoadingTolerance() + PlayBufferTime::playBufferTime + the value defined in EXT-X-TARGETDURATION`

      De forma predeterminada, para el contenido con una duración de Destinatario de 6 segundos, será 5,0 + 30,0 + 6,0 segundos (41 segundos)

   1. Si se produce una pausa publicitaria en los 10 segundos posteriores a la posición de inicio, se resolverá junto con los anuncios previos al anuncio antes del estado PREPARADO.

>[!IMPORTANT]
>
>**Factores a tener en cuenta con la resolución de publicidad diferida:**
>
>* La resolución diferida de publicidad solo se admite para flujos VOD con los modos SERVER_MAP y MANIFEST_CUES.
>* La resolución de publicidad diferida no está habilitada de forma predeterminada. Si se deshabilita, todos los anuncios se resuelven en los flujos de VOD antes de los inicios de reproducción.
>* La resolución diferida de publicidad no es compatible con la función Activar instantáneamente. Para obtener más información sobre la activación instantánea, consulte Activado instantáneo.
>* Con la resolución de publicidad diferida, mientras se busca hacia delante durante una pausa publicitaria, la pausa publicitaria más cercana a la posición de búsqueda se resolverá durante la búsqueda.
>* Con la resolución diferida de publicidad, si existen varios saltos de publicidad al mismo tiempo (VMAP), se resolverán al mismo tiempo.
>* No se recomienda reducir el valor de *setDelayAdLoadingTolerance() *por debajo del valor predeterminado (5 segundos). Al hacerlo, el reproductor podría &quot;almacenar en búfer&quot; innecesariamente.
>* La resolución diferida de publicidad no afecta a los anuncios previos.
>* La resolución de publicidad diferida se admite actualmente en Auditude-Plugin. Se recomienda no establecer ** setDelayAdLoadingen como true si utiliza una resolución personalizada.

>


