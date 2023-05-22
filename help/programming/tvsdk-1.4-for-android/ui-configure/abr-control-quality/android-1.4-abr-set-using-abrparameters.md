---
description: Puede establecer valores de control ABR sólo con ABRControlParameters, pero puede construir uno nuevo en cualquier momento.
title: Configurar tasas de bits adaptables mediante ABRControlParameters
exl-id: 787e962c-371f-4ac8-ae13-8b38a230593f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# Configurar tasas de bits adaptables mediante ABRControlParameters{#configure-adaptive-bit-rates-using-abrcontrolparameters}

Puede establecer valores de control ABR sólo con ABRControlParameters, pero puede construir uno nuevo en cualquier momento.

Las siguientes condiciones se aplican a `ABRControlParameters`:

* Debe proporcionar valores para todos los parámetros en tiempo de construcción.
* No se pueden cambiar valores individuales después del tiempo de construcción.
* Si los parámetros especificados están fuera del intervalo permitido, una variable `ArgumentError` se ha lanzado.

1. Decida la velocidad de bits inicial, mínima y máxima.
1. Determine la directiva ABR:

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. Establezca los valores del parámetro ABR en la variable `ABRControlParameters` y asignarlos al reproductor de medios.

   ```java
   public ABRControlParameters(int initialBitRate, 
     int minBitRate, 
     int maxBitRate, 
     ABRControlParameters.ABRPolicy abrPolicy, 
     int minTrickPlayBitRate, 
     int maxTrickPlayBitRate, 
     int maxTrickPlayBandwidthUsage, 
     int maxPlayoutRate);
   ```
