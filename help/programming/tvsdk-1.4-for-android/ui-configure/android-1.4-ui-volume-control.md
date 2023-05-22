---
description: Puede configurar un control de interfaz de usuario para el volumen de sonido.
title: Proporcionar control de volumen
exl-id: aa8ffdf3-515b-4899-8a00-8fb5b8c595a9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
