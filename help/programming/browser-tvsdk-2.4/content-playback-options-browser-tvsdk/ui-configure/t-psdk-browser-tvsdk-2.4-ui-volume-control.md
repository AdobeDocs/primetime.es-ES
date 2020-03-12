---
description: Puede configurar un control de interfaz de usuario para el volumen de sonido.
seo-description: Puede configurar un control de interfaz de usuario para el volumen de sonido.
seo-title: Proporcionar control de volumen
title: Proporcionar control de volumen
uuid: 5f2f69cc-3969-4ca2-8ab9-5713fdf5cdb8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Proporcionar control de volumen{#provide-volume-control}

Puede configurar un control de interfaz de usuario para el volumen de sonido.

1. Espere a que la instancia `MediaPlayer` esté en un estado válido para este comando.

   Cualquier estado, excepto RELEASED o ERROR, es válido.
1. Establezca el atributo de volumen en la `MediaPlayer` instancia para establecer el volumen de audio.

   ```js
   player.volume = ...
   ```

   El valor del volumen representa el volumen solicitado expresado como una proporción del volumen máximo, donde 0 guarda silencio y es el volumen máximo.

