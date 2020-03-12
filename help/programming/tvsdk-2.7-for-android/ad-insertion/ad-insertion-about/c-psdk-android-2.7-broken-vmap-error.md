---
description: Cuando TVSDK encuentra un VMAP dañado en una respuesta del servidor de publicidad, distribuye un error 1109 (NETWORK_AD_URL_FAILED).
keywords: 1109;NETWORK_AD_URL_FAILED;broken VMAP
seo-description: Cuando TVSDK encuentra un VMAP dañado en una respuesta del servidor de publicidad, distribuye un error 1109 (NETWORK_AD_URL_FAILED).
seo-title: Gestión de errores de cliente para VMAP dañado
title: Gestión de errores de cliente para VMAP dañado
uuid: 7cc68c86-bb49-4a1b-a1ec-65ca4c94d75d
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Gestión de errores de cliente para VMAP dañado {#client-error-handling-for-broken-vmap}

Cuando TVSDK encuentra un VMAP dañado en una respuesta del servidor de publicidad, distribuye un error 1109 (NETWORK_AD_URL_FAILED).

Dependiendo de la naturaleza de la respuesta del servidor de publicidad y de la configuración de carga de publicidad, el reproductor puede recibir números diferentes de errores 1109 cuando TVSDK encuentra un VMAP dañado en una respuesta del servidor de publicidad.

Analicemos un escenario en el que la respuesta del servidor de publicidad apunta a VMAP XML. Digamos también que la respuesta del servidor de publicidad tiene cuatro ranuras de anuncios disponibles, cada una de las cuales apunta al mismo VMAP. Finalmente, digamos que este VMAP está roto.

En este escenario, si la resolución de anuncios floja está habilitada ( [Habilitar la resolución](../../../tvsdk-2.7-for-android/ad-insertion/c-psdk-android-2.7-lazy-ad-resolving/t-psdk-android-2.7-enable-lazy-ad-resolving.md)de anuncios diferida), TVSDK distribuirá dos errores 1109 (no uno como cabría esperar): se envía un error en cada paso de análisis por la línea de tiempo. Esto se debe a que, cuando la resolución de anuncios floja está habilitada, TVSDK analiza las publicidades en 2 pasos: el primer paso se produce justo antes de que se inicie la reproducción del contenido para los anuncios anteriores y el segundo paso se produce después de que se inicie la reproducción, para los anuncios en versión intermedia y posterior.

>[!NOTE]
>
>En este escenario, si deshabilita la resolución diferida de anuncios, TVSDK activará solo un error 1109 (solo un pase de análisis).

