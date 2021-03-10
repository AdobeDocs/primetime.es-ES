---
description: Puede configurar un control de interfaz de usuario para el volumen de sonido.
title: Proporcionar control de volumen
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---


# Proporcionar control de volumen{#provide-volume-control}

Puede configurar un control de interfaz de usuario para el volumen de sonido.

1. Espere a que la instancia de MediaPlayer esté en un estado válido para este comando, que es cualquiera excepto RELEASED o ERROR.
1. Llame a `setVolume` en la instancia `MediaPlayer` para configurar el volumen de audio.

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   El valor del volumen representa el volumen solicitado expresado como una proporción del volumen máximo, donde 0 no dice nada y 100 es el volumen máximo.

