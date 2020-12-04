---
description: Cuando TVSDK encuentra un VMAP dañado en una respuesta del servidor de publicidad, distribuye un error 1109 (NETWORK_AD_URL_FAILED).
keywords: 1109;NETWORK_AD_URL_FAILED;broken VMAP
seo-description: Cuando TVSDK encuentra un VMAP dañado en una respuesta del servidor de publicidad, distribuye un error 1109 (NETWORK_AD_URL_FAILED).
seo-title: Gestión de errores de cliente para VMAP dañado
title: Gestión de errores de cliente para VMAP dañado
uuid: ab2c567d-d945-4ebe-b65a-c1f13518a576
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# Administración de errores del cliente para VMAP dañado {#client-error-handling-for-broken-vmap}

Cuando TVSDK encuentra un VMAP dañado en una respuesta del servidor de publicidad, distribuye un error 1109 (NETWORK_AD_URL_FAILED).

Dependiendo de la naturaleza de la respuesta del servidor de publicidad y de la configuración de carga de publicidad, el reproductor puede recibir números diferentes de errores 1109 cuando TVSDK encuentra un VMAP dañado en una respuesta del servidor de publicidad.

Analicemos un escenario en el que la respuesta del servidor de publicidad apunta a VMAP XML. Digamos también que la respuesta del servidor de publicidad tiene cuatro ranuras de anuncios disponibles, cada una de las cuales apunta al mismo VMAP. Finalmente, digamos que este VMAP está roto.

En este escenario, si está habilitada la resolución diferida de publicidades ([Habilitar la resolución diferida de publicidades](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/t-enable-lazy-ad-resolving.md)), TVSDK enviará dos errores 1109 (no uno tal como cabría esperar): se envía un error en cada paso de análisis por la línea de tiempo. Esto se debe a que, cuando la resolución de anuncios floja está habilitada, TVSDK analiza las publicidades en 2 pasos: la primera pasada se produce justo antes de que se produzcan los inicios de reproducción del contenido para los anuncios anteriores y la segunda pasada se produce después de los inicios de reproducción, para los anuncios medios y posteriores.

>[!NOTE]
>
>En este escenario, si deshabilita la resolución diferida de anuncios, TVSDK activará solo un error 1109 (solo un pase de análisis).