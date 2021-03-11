---
description: Puede configurar un control de interfaz de usuario para ajustar el volumen del vídeo.
title: Proporcionar control de volumen
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 2%

---


# Proporcionar control de volumen {#provide-volume-control}

Puede configurar un control de interfaz de usuario para ajustar el volumen del vídeo.

1. En la rutina de llamada de retorno del elemento de interfaz de control de volumen, asegúrese de que el reproductor esté en un estado válido para este comando.

   >[!TIP]
   >
   >Cualquier estado es válido, excepto LANZADO.

1. Llame a `setVolume` para configurar el volumen de audio.

   Por ejemplo:

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   El valor del volumen representa el volumen solicitado expresado como una proporción del volumen máximo, donde `0` no dice nada y `1` es el volumen máximo.

