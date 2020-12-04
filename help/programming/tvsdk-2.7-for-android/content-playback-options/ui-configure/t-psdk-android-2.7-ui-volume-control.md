---
description: Puede configurar un control de interfaz de usuario para ajustar el volumen del vídeo.
seo-description: Puede configurar un control de interfaz de usuario para ajustar el volumen del vídeo.
seo-title: Proporcionar control de volumen
title: Proporcionar control de volumen
uuid: f1e959e0-1817-4ccb-8adc-3eba09c91887
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 1%

---


# Proporcionar control de volumen {#provide-volume-control}

Puede configurar un control de interfaz de usuario para ajustar el volumen del vídeo.

1. En la rutina de llamada de retorno del elemento de interfaz de control de volumen, asegúrese de que el reproductor está en un estado válido para este comando.

   >[!TIP]
   >
   >Cualquier estado, excepto RELEASED, es válido.

1. Llame a `setVolume` para configurar el volumen de audio.

   Por ejemplo:

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   El valor del volumen representa el volumen solicitado expresado como una proporción del volumen máximo, donde `0` es silencioso y `1` es el volumen máximo.

