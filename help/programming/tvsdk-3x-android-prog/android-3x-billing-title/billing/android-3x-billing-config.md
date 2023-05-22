---
description: Si utiliza la configuración predeterminada, no tiene que hacer nada más para habilitar o configurar la facturación. Si ha obtenido parámetros de configuración diferentes de su representante de habilitación de Adobe, utilice la clase BillingMetricsConfiguration para configurar estos parámetros antes de inicializar el reproductor de medios.
title: Configurar métricas de facturación
exl-id: e3b97de6-8442-463f-b5b0-0dec34aa7735
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Configurar métricas de facturación {#configure-billing-metrics}

Si utiliza la configuración predeterminada, no tiene que hacer nada más para habilitar o configurar la facturación. Si ha obtenido parámetros de configuración diferentes de su representante de habilitación de Adobe, utilice la clase BillingMetricsConfiguration para configurar estos parámetros antes de inicializar el reproductor de medios.

>[!TIP]
>
>La mayoría de los clientes deben utilizar la configuración predeterminada.

>[!IMPORTANT]
>
>La configuración que establezca permanecerá vigente durante toda la vida útil del reproductor de contenidos. Una vez inicializado el reproductor de contenido, no se puede cambiar la configuración.

Para configurar métricas de facturación:

Introduzca el siguiente ejemplo de código.

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(); 
BillingMetricsConfiguration billingConfig = new BillingMetricsConfiguration(); 
billingConfig.setEnabled(true); 
billingConfig.setProVODBillableDurationMinutes(60); 
billingConfig.setStdVODBillableDurationMinutes(30); 
billingConfig.setLiveBillableDurationMinutes(15); 
config.setBillingMetricsConfiguration(billingConfig); 
mediaPlayer.replaceCurrentResource(mediaResource, config);
```
