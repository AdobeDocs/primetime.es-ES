---
description: Puede configurar un control de interfaz de usuario para el volumen de sonido.
title: Proporcionar control de volumen
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 0%

---

# Proporcionar control de volumen{#provide-volume-control}

Puede configurar un control de interfaz de usuario para el volumen de sonido.

1. Espere a que `MediaPlayer` la instancia debe estar en un estado válido para este comando.

   Cualquier estado excepto RELEASED o ERROR es válido.
1. Establezca el atributo de volumen en `MediaPlayer` para configurar el volumen de audio.

   ```js
   player.volume = ...
   ```

   El valor del volumen representa el volumen solicitado expresado como una proporción del volumen máximo, donde 0 es silencioso y es el volumen máximo.
