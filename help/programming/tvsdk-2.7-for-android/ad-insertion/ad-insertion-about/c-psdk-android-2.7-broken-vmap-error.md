---
description: Cuando TVSDK encuentra un VMAP roto en una respuesta del servidor de publicidad, envía un error 1109 (NETWORK_AD_URL_FAILED).
keywords: 1109;NETWORK_AD_URL_FAILED;VMAP roto
title: Tratamiento de errores de cliente para VMAP roto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# Tratamiento de errores de cliente para VMAP dañado {#client-error-handling-for-broken-vmap}

Cuando TVSDK encuentra un VMAP roto en una respuesta del servidor de publicidad, envía un error 1109 (NETWORK_AD_URL_FAILED).

Dependiendo de la naturaleza de la respuesta del servidor de publicidad y de la configuración de carga de publicidad, el reproductor podría recibir diferentes números de errores 1109 cuando TVSDK encuentre un VMAP roto en una respuesta del servidor de publicidad.

Consideremos un escenario en el que la respuesta del servidor de publicidad apunta a VMAP XML. Digamos también que la respuesta del servidor de publicidad tiene cuatro espacios de anuncios disponibles, cada uno de los cuales apunta al mismo VMAP. Finalmente, digamos que este VMAP está roto.

En este caso, si la resolución de anuncios diferida está habilitada ( [Habilitar la resolución de anuncios diferida](../../../tvsdk-2.7-for-android/ad-insertion/c-psdk-android-2.7-lazy-ad-resolving/t-psdk-android-2.7-enable-lazy-ad-resolving.md)), TVSDK enviará dos errores 1109 (no uno como cabría esperar): se envía un error en cada paso de análisis a través de la cronología. Esto se debe a que cuando la resolución de anuncios diferida está habilitada, TVSDK analiza los anuncios en 2 pasos: la primera pasada se produce justo antes de que se inicie la reproducción del contenido para los anuncios previos a la emisión y la segunda pasada se produce después de iniciarse la reproducción, para los anuncios mid-roll y post-roll.

>[!NOTE]
>
>En esta situación, si desactiva la resolución de anuncios diferidos, TVSDK activará solo un error 1109 (solo un pase de análisis).

