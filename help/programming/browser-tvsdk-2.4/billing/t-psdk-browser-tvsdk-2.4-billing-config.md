---
description: Si utiliza la configuración predeterminada, no hay nada más que hacer para habilitar o configurar la facturación. Si ha obtenido parámetros de configuración diferentes de su representante de habilitación de Adobe, utilice la clase BillingMetricsConfiguration para establecer estos parámetros antes de inicializar el reproductor de medios.
title: Configurar métricas de facturación
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# Configurar métricas de facturación{#configure-billing-metrics}

Si utiliza la configuración predeterminada, no hay nada más que hacer para habilitar o configurar la facturación. Si ha obtenido parámetros de configuración diferentes de su representante de habilitación de Adobe, utilice la clase BillingMetricsConfiguration para establecer estos parámetros antes de inicializar el reproductor de medios.

La mayoría de los clientes deben utilizar la configuración predeterminada.

>[!IMPORTANT]
>
>La configuración que establezca permanecerá en vigor durante toda la vida útil del reproductor de contenidos. Una vez que inicialice el reproductor de contenidos, no podrá cambiar la configuración.

Para configurar las métricas de facturación:

* Introduzca el siguiente ejemplo de código.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.billingMetricsConfiguration.isEnabled = true; 
   config.billingMetricsConfiguration.proVODBillableDurationMinutes = 60; 
   config.billingMetricsConfiguration.stdVODBillableDurationMinutes = 30; 
   config.billingMetricsConfiguration.liveBillableDurationMinutes = 15; 
   _player.replaceCurrentResource(_resource, config);
   ```

   donde `_player` es una instancia de `AdobePSDK.MediaPlayer` y `_resource` es una instancia de `AdobePSDK.MediaResource`.

