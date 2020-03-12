---
description: Puede configurar un control de interfaz de usuario para el volumen de sonido.
seo-description: Puede configurar un control de interfaz de usuario para el volumen de sonido.
seo-title: Proporcionar control de volumen
title: Proporcionar control de volumen
uuid: 63e96424-54d0-4c16-bd94-2366722f752a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Proporcionar control de volumen{#provide-volume-control}

Puede configurar un control de interfaz de usuario para el volumen de sonido.

1. Espere a que la instancia de MediaPlayer esté en un estado válido para este comando, que es cualquiera excepto RELEASED o ERROR.
1. Llame `setVolume` a la `MediaPlayer` instancia para configurar el volumen de audio.

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   El valor del volumen representa el volumen solicitado expresado como una proporción del volumen máximo, donde 0 es silencioso y 100 es el volumen máximo.

