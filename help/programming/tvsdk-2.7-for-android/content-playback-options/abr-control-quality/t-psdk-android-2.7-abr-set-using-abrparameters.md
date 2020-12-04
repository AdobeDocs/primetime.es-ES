---
description: Los valores de control de ABR solo se pueden establecer con ABRControlParameters, pero se puede construir uno nuevo en cualquier momento.
seo-description: Los valores de control de ABR solo se pueden establecer con ABRControlParameters, pero se puede construir uno nuevo en cualquier momento.
seo-title: Configurar velocidades de bits adaptables mediante ABRControlParameters
title: Configurar velocidades de bits adaptables mediante ABRControlParameters
uuid: 7084e954-196b-492e-846f-f8b36bed13a9
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Configure las velocidades de bits adaptables mediante ABRControlParameters {#configure-adaptive-bit-rates-using-abrcontrolparameters}

Los valores de control de ABR solo se pueden establecer con ABRControlParameters, pero se puede construir uno nuevo en cualquier momento.

Las siguientes condiciones se aplican a `ABRControlParameters`:

* En tiempo de construcción, debe proporcionar valores para todos los parámetros.
* Después de la construcción, no se pueden cambiar los valores individuales.
* Si los parámetros que especifica están fuera del rango permitido, se genera un `ArgumentError`.

1. Determinar las velocidades de bits iniciales, mínimas y máximas.
1. Determine la directiva ABR:

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. Establezca los valores del parámetro ABR en el constructor `ABRControlParameters` y asigne los valores al Reproductor de medios.

   ```
   public ABRControlParameters(int initialBitRate, 
     int minBitRate, 
     int maxBitRate, 
     ABRControlParameters.ABRPolicy abrPolicy, 
     int minTrickPlayBitRate, 
     int maxTrickPlayBitRate, 
     int maxTrickPlayBandwidthUsage, 
     int maxPlayoutRate);
   ```

