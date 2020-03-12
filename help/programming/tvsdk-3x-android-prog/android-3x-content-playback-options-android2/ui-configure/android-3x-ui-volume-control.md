---
description: Puede configurar un control de interfaz de usuario para ajustar el volumen del vídeo.
seo-description: Puede configurar un control de interfaz de usuario para ajustar el volumen del vídeo.
seo-title: Proporcionar control de volumen
title: Proporcionar control de volumen
uuid: c87fe656-0329-4c9c-b65b-43be48c77062
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Proporcionar control de volumen {#provide-volume-control}

Puede configurar un control de interfaz de usuario para ajustar el volumen del vídeo.

1. En la rutina de llamada de retorno del elemento de interfaz de control de volumen, asegúrese de que el reproductor está en un estado válido para este comando.

   >[!TIP]
   >
   >Cualquier estado, excepto RELEASED, es válido.

1. Llame `setVolume` para establecer el volumen del audio.

   Por ejemplo:

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   El valor del volumen representa el volumen solicitado expresado como una proporción del volumen máximo, donde `0` es silencioso y `1` es el volumen máximo.