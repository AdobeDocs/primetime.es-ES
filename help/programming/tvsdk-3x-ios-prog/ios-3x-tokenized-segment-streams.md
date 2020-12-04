---
description: Los flujos HLS que se entregan a través de una red de Envío de contenido (CDN) a veces pueden utilizar tokens de autenticación en las solicitudes de manifiesto y segmento para la verificación. Estos tokens se pueden proporcionar como parámetros de URL o como encabezados de cookies.
seo-description: Los flujos HLS que se entregan a través de una red de Envío de contenido (CDN) a veces pueden utilizar tokens de autenticación en las solicitudes de manifiesto y segmento para la verificación. Estos tokens se pueden proporcionar como parámetros de URL o como encabezados de cookies.
seo-title: Flujos de segmentos con autentificación
title: Flujos de segmentos con autentificación
uuid: 62e3b858-2605-4960-b504-9010674f80ad
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# Flujos de segmentos con autentificación {#tokenized-segment-streams}

Los flujos HLS que se entregan a través de una red de Envío de contenido (CDN) a veces pueden utilizar tokens de autenticación en las solicitudes de manifiesto y segmento para la verificación. Estos tokens se pueden proporcionar como parámetros de URL o como encabezados de cookies.

Los tokens proporcionados como cookies en la respuesta de manifiesto maestro (m3u8) no se comparten con las solicitudes de segmento (ts) aunque las solicitudes de segmento sean para el mismo dominio. Para habilitar el uso compartido de estas cookies en una solicitud de segmento, establezca la siguiente propiedad en la instancia `PTMetadata` proporcionada al elemento del reproductor: 

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

Se realiza una solicitud adicional al manifiesto maestro (m3u8) antes de que el flujo empiece a reproducirse.

>[!IMPORTANT]
>
>Esta función de uso compartido de cookies solo se admite en dispositivos con iOS 8 o superior.

