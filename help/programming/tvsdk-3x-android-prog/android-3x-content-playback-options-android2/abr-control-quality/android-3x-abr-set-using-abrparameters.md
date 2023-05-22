---
description: Puede establecer valores de control ABR sólo con ABRControlParameters, pero puede construir uno nuevo en cualquier momento.
title: Configurar tasas de bits adaptables mediante ABRControlParameters
exl-id: 1f8a4a97-0341-43e7-afdf-801275bc8c94
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Configurar tasas de bits adaptables mediante ABRControlParameters {#configure-adaptive-bit-rates-using-abrcontrolparameters}

Puede establecer valores de control ABR sólo con ABRControlParameters, pero puede construir uno nuevo en cualquier momento.

Las siguientes condiciones se aplican a `ABRControlParameters`:

* En el momento de la construcción, debe proporcionar valores para todos los parámetros.
* Después de la construcción, no se pueden cambiar valores individuales.
* Si los parámetros especificados están fuera del intervalo permitido, una variable `ArgumentError` se ha lanzado.

1. Determine las velocidades de bits iniciales, mínimas y máximas.
1. Determine la directiva ABR:

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. Establezca los valores del parámetro ABR en la variable `ABRControlParameters` y asigne los valores al reproductor de medios.

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
