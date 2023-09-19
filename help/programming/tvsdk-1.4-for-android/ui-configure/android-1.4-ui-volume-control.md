---
description: Puede configurar un control de interfaz de usuario para el volumen de sonido.
title: Proporcionar control de volumen
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# Proporcionar control de volumen{#provide-volume-control}

Puede configurar un control de interfaz de usuario para el volumen de sonido.

1. Espere a que la instancia de MediaPlayer esté en un estado válido para este comando, que es cualquiera excepto RELEASED o ERROR.
1. Llamada `setVolume` en el `MediaPlayer` para configurar el volumen de audio.

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   El valor del volumen representa el volumen solicitado expresado como una proporción del volumen máximo, donde 0 es silencioso y 100 es el volumen máximo.
