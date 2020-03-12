---
description: Los valores de control de ABR solo se pueden establecer con ABRControlParameters, pero se puede construir uno nuevo en cualquier momento.
seo-description: Los valores de control de ABR solo se pueden establecer con ABRControlParameters, pero se puede construir uno nuevo en cualquier momento.
seo-title: Configurar velocidades de bits adaptables mediante ABRControlParameters
title: Configurar velocidades de bits adaptables mediante ABRControlParameters
uuid: 7084e954-196b-492e-846f-f8b36bed13a9
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Configurar velocidades de bits adaptables mediante ABRControlParameters {#configure-adaptive-bit-rates-using-abrcontrolparameters}

Los valores de control de ABR solo se pueden establecer con ABRControlParameters, pero se puede construir uno nuevo en cualquier momento.

Se aplican las siguientes condiciones a `ABRControlParameters`:

* En tiempo de construcción, debe proporcionar valores para todos los parámetros.
* Después de la construcción, no se pueden cambiar los valores individuales.
* Si los parámetros especificados están fuera del rango permitido, se `ArgumentError` genera un error.

1. Determinar las velocidades de bits iniciales, mínimas y máximas.
1. Determine la directiva ABR:

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. Establezca los valores de parámetro ABR en el constructor y asigne los valores al Reproductor de medios `ABRControlParameters` .

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

