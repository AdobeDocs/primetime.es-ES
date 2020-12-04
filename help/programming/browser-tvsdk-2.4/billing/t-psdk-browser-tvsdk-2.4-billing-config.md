---
description: Si utiliza la configuración predeterminada, no tiene que hacer nada más para habilitar o configurar la facturación. Si ha obtenido parámetros de configuración diferentes del representante de habilitación de Adobe, utilice la clase BillingMetricsConfiguration para configurar estos parámetros antes de inicializar el reproductor de medios.
seo-description: Si utiliza la configuración predeterminada, no tiene que hacer nada más para habilitar o configurar la facturación. Si ha obtenido parámetros de configuración diferentes del representante de habilitación de Adobe, utilice la clase BillingMetricsConfiguration para configurar estos parámetros antes de inicializar el reproductor de medios.
seo-title: Configurar métricas de facturación
title: Configurar métricas de facturación
uuid: 04d3b53e-f08c-49d0-ba42-5375f1307d2e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 0%

---


# Configurar métricas de facturación{#configure-billing-metrics}

Si utiliza la configuración predeterminada, no tiene que hacer nada más para habilitar o configurar la facturación. Si ha obtenido parámetros de configuración diferentes del representante de habilitación de Adobe, utilice la clase BillingMetricsConfiguration para configurar estos parámetros antes de inicializar el reproductor de medios.

La mayoría de los clientes debe utilizar la configuración predeterminada.

>[!IMPORTANT]
>
>La configuración que defina permanecerá en vigor durante toda la vida útil del reproductor de medios. Una vez que inicialice el reproductor multimedia, no podrá cambiar la configuración.

Para configurar las métricas de facturación:

* Introduzca la siguiente muestra de código.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.billingMetricsConfiguration.isEnabled = true; 
   config.billingMetricsConfiguration.proVODBillableDurationMinutes = 60; 
   config.billingMetricsConfiguration.stdVODBillableDurationMinutes = 30; 
   config.billingMetricsConfiguration.liveBillableDurationMinutes = 15; 
   _player.replaceCurrentResource(_resource, config);
   ```

   donde `_player` es una instancia de `AdobePSDK.MediaPlayer` y `_resource` es una instancia de `AdobePSDK.MediaResource`.

