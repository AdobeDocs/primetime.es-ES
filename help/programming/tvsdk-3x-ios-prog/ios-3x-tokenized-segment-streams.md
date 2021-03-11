---
description: Los flujos HLS que se entregan a través de una red de entrega de contenido (CDN) a veces pueden utilizar tokens de autenticación en el manifiesto y segmentar las solicitudes de verificación. Estos tokens se pueden proporcionar como parámetros de URL o como encabezados de cookies.
title: Flujos de segmentos con token
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# Flujos de segmento autenticados {#tokenized-segment-streams}

Los flujos HLS que se entregan a través de una red de entrega de contenido (CDN) a veces pueden utilizar tokens de autenticación en el manifiesto y segmentar las solicitudes de verificación. Estos tokens se pueden proporcionar como parámetros de URL o como encabezados de cookies.

Los tokens proporcionados como cookies en la respuesta del manifiesto maestro (m3u8) no se comparten con las solicitudes de segmento (ts) aunque las solicitudes de segmento correspondan al mismo dominio. Para permitir el uso compartido de estas cookies en una solicitud de segmento, establezca la siguiente propiedad en la instancia `PTMetadata` proporcionada al elemento del reproductor: 

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

Se realiza una solicitud adicional al manifiesto maestro (m3u8) antes de que comience a reproducirse el flujo.

>[!IMPORTANT]
>
>Esta función de uso compartido de cookies solo es compatible con dispositivos que ejecutan iOS 8 o superior.

