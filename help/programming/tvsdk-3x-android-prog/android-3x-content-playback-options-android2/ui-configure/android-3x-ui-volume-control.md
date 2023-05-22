---
description: Puede configurar un control de interfaz de usuario para ajustar el volumen del vídeo.
title: Proporcionar control de volumen
exl-id: 8b8b0263-9874-4e87-853e-eb394ebef3e3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Proporcionar control de volumen {#provide-volume-control}

Puede configurar un control de interfaz de usuario para ajustar el volumen del vídeo.

1. En la rutina de devolución de llamada del elemento de interfaz de control de volumen, asegúrese de que el reproductor se encuentra en un estado válido para este comando.

   >[!TIP]
   >
   >Cualquier estado, excepto RELEASED es válido.

1. Llamada `setVolume` para ajustar el volumen del audio.

   Por ejemplo:

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   El valor del volumen representa el volumen solicitado expresado como una proporción del volumen máximo, donde `0` es silencioso y `1` es el volumen máximo.
