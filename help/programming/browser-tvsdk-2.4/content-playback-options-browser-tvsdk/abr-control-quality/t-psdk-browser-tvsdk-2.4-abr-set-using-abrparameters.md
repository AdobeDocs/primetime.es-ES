---
description: Los valores de control de ABR solo se pueden establecer con ABRControlParameters, pero se puede construir uno nuevo en cualquier momento.
seo-description: Los valores de control de ABR solo se pueden establecer con ABRControlParameters, pero se puede construir uno nuevo en cualquier momento.
seo-title: Configurar velocidades de bits adaptables mediante ABRControlParameters
title: Configurar velocidades de bits adaptables mediante ABRControlParameters
uuid: 99b7a463-327b-48bf-8244-e41467072b44
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Configurar velocidades de bits adaptables mediante ABRControlParameters{#configure-adaptive-bit-rates-using-abrcontrolparameters}

Los valores de control de ABR solo se pueden establecer con ABRControlParameters, pero se puede construir uno nuevo en cualquier momento.

Se aplican las siguientes condiciones a `ABRControlParameters`:

* Debe proporcionar valores para todos los parámetros en tiempo de construcción.
* No se pueden cambiar valores individuales después del tiempo de construcción.
* Si los parámetros especificados están fuera del rango permitido, se `ArgumentError` genera un error.

1. Determine la directiva ABR:

   * `ABRControlParameters.CONSERVATIVE_POLICY`
   * `ABRControlParameters.MODERATE_POLICY`
   * `ABRControlParameters.AGGRESSIVE_POLICY`

1. Establezca los valores de parámetro ABR en el constructor y asígnelos al Reproductor de medios `ABRControlParameters` .

   ```js
   var abrParams = new AdobePSDK.ABRControlParameters(); 
   abrParams.initialBitRate = nInitialBitRate; 
   abrParams.minBitRate = nMinBitRate; 
   abrParams.maxBitRate = nMaxBitRate; 
   abrParams.abrPolicy = eABRPolicy; 
   player.abrControlParameters = abrParams;
   ```

