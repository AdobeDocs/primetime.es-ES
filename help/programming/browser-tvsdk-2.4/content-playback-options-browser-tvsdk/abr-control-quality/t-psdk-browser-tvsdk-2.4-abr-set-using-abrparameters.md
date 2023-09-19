---
description: Puede establecer valores de control ABR sólo con ABRControlParameters, pero puede construir uno nuevo en cualquier momento.
title: Configurar tasas de bits adaptables mediante ABRControlParameters
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# Configurar tasas de bits adaptables mediante ABRControlParameters{#configure-adaptive-bit-rates-using-abrcontrolparameters}

Puede establecer valores de control ABR sólo con ABRControlParameters, pero puede construir uno nuevo en cualquier momento.

Las siguientes condiciones se aplican a `ABRControlParameters`:

* Debe proporcionar valores para todos los parámetros en tiempo de construcción.
* No se pueden cambiar valores individuales después del tiempo de construcción.
* Si los parámetros especificados están fuera del intervalo permitido, una variable `ArgumentError` se ha lanzado.

1. Determine la directiva ABR:

   * `ABRControlParameters.CONSERVATIVE_POLICY`
   * `ABRControlParameters.MODERATE_POLICY`
   * `ABRControlParameters.AGGRESSIVE_POLICY`

1. Establezca los valores del parámetro ABR en la variable `ABRControlParameters` y asignarlos al reproductor de medios.

   ```js
   var abrParams = new AdobePSDK.ABRControlParameters(); 
   abrParams.initialBitRate = nInitialBitRate; 
   abrParams.minBitRate = nMinBitRate; 
   abrParams.maxBitRate = nMaxBitRate; 
   abrParams.abrPolicy = eABRPolicy; 
   player.abrControlParameters = abrParams;
   ```
