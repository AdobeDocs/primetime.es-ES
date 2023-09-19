---
description: Cuando TVSDK encuentra un VMAP dañado en una respuesta del servidor de publicidad, envía un error 1109 (NETWORK_AD_URL_FAILED).
keywords: 1109;NETWORK_AD_URL_FAILED;VMAP interrumpido
title: Administración de errores de cliente para VMAP dañado
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Administración de errores de cliente para VMAP dañado {#client-error-handling-for-broken-vmap}

Cuando TVSDK encuentra un VMAP dañado en una respuesta del servidor de publicidad, envía un error 1109 (NETWORK_AD_URL_FAILED).

Según la naturaleza de la respuesta del servidor de publicidad y la configuración de carga de publicidad, el reproductor podría recibir números diferentes de errores 1109 cuando TVSDK encuentre un VMAP dañado en una respuesta del servidor de publicidad.

Consideremos un escenario en el que la respuesta del servidor de publicidad apunte a VMAP XML. Digamos también que la respuesta del servidor de publicidad tiene cuatro ranuras de publicidad disponibles, cada una de las cuales apunta al mismo VMAP. Finalmente, digamos que este VMAP está roto.

En este escenario, si la resolución de anuncios diferidos está habilitada ([Habilitar la resolución de anuncios diferidos](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/t-enable-lazy-ad-resolving.md)), TVSDK enviará dos errores 1109 (no uno como cabría esperar): se envía un error en cada paso de análisis a través de la cronología. Esto se debe a que, cuando la resolución de anuncios diferidos está habilitada, TVSDK analiza los anuncios en 2 pasadas: la primera pasa se produce justo antes de que se inicie la reproducción del contenido para los anuncios previos a la emisión y la segunda pasa después de que se inicie la reproducción, para los anuncios durante la emisión y después de la emisión.

>[!NOTE]
>
>En esta situación, si deshabilita la resolución de anuncios diferidos, TVSDK activará solo un error 1109 (solo una pasada de análisis).
