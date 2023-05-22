---
description: Puede configurar un control de interfaz de usuario para el volumen de sonido.
title: Proporcionar control de volumen
exl-id: 5c446081-5491-46b6-9259-293131af80cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
