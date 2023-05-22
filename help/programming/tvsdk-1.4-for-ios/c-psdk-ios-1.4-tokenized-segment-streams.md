---
description: Las secuencias HLS que se entregan a través de una red de distribución de contenido (CDN) a veces pueden utilizar tokens de autenticación en las solicitudes de manifiesto y segmento para la verificación. Estos tokens se pueden proporcionar como parámetros de URL o como encabezados de cookie.
title: Flujos de segmentos tokenizados
exl-id: 20a3e8a2-2e9d-4c0d-abea-66edcbcf0003
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Flujos de segmentos tokenizados{#tokenized-segment-streams}

Las secuencias HLS que se entregan a través de una red de distribución de contenido (CDN) a veces pueden utilizar tokens de autenticación en las solicitudes de manifiesto y segmento para la verificación. Estos tokens se pueden proporcionar como parámetros de URL o como encabezados de cookie.

Los tokens proporcionados como cookies en la respuesta del manifiesto maestro (m3u8) no se comparten con las solicitudes de segmento (ts) aunque las solicitudes de segmento sean para el mismo dominio. Para habilitar el uso compartido de estas cookies en una solicitud de segmento, establezca la siguiente propiedad en la `PTMetadata` instancia proporcionada al elemento de reproductor: 

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

Se realiza una solicitud adicional al manifiesto maestro (m3u8) antes de que el flujo comience a reproducirse.

>[!IMPORTANT]
>
>Esta función de uso compartido de cookies solo se admite en dispositivos con iOS 8 o posterior.
