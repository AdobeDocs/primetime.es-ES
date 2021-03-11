---
description: Puede establecer valores de control de ABR solo con ABRControlParameters, pero puede construir uno nuevo en cualquier momento.
title: Configurar las tasas de bits adaptables mediante ABRControlParameters
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# Configurar las tasas de bits adaptables mediante ABRControlParameters {#configure-adaptive-bit-rates-using-abrcontrolparameters}

Puede establecer valores de control de ABR solo con ABRControlParameters, pero puede construir uno nuevo en cualquier momento.

Las siguientes condiciones se aplican a `ABRControlParameters`:

* En el momento de la construcción, debe proporcionar valores para todos los parámetros.
* Después de la construcción, no se pueden cambiar valores individuales.
* Si los parámetros especificados están fuera del rango permitido, se genera un `ArgumentError`.

1. Determine las tasas de bits inicial, mínima y máxima.
1. Determine la política ABR:

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
