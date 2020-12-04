---
description: Para dar cabida a los clientes que desean pagar solamente por lo que utilizan, en lugar de una tasa fija independientemente del uso real, Adobe recopila métricas de uso y utiliza estas métricas para determinar cuánto facturar a los clientes.
seo-description: Para dar cabida a los clientes que desean pagar solamente por lo que utilizan, en lugar de una tasa fija independientemente del uso real, Adobe recopila métricas de uso y utiliza estas métricas para determinar cuánto facturar a los clientes.
seo-title: Métricas de facturación
title: Métricas de facturación
uuid: 658ffbcd-dedc-464c-8ec7-aa3bdfcb1512
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---


# Métricas de facturación {#billing-metrics}

Para dar cabida a los clientes que desean pagar solamente por lo que utilizan, en lugar de una tasa fija independientemente del uso real, Adobe recopila métricas de uso y utiliza estas métricas para determinar cuánto facturar a los clientes.

Cada vez que el reproductor genera un evento de inicio de flujo, TVSDK inicio enviar mensajes HTTP periódicamente al sistema de facturación del Adobe. El período, conocido como duración facturable, puede ser diferente para VOD estándar, VOD pro (anuncios intermedios habilitados) y contenido activo. La duración predeterminada para cada tipo de contenido es de 30 minutos, pero el contrato con Adobe determina los valores reales.

Los mensajes contienen la siguiente información:

* Tipo de contenido (activo, lineal o VOD)
* Dirección URL del contenido
* Indica si las publicidades están habilitadas
* Indica si los anuncios medios están activados (solo VOD)
* Si el flujo está protegido por DRM
* La versión y la plataforma TVSDK

Adobe configura previamente esta disposición, pero si desea cambiar la disposición, trabaje con su representante de habilitación de Adobe.

Para supervisar las estadísticas que TVSDK envía a Adobe, obtenga la URL de su representante de habilitación de Adobe y utilice una herramienta de captura de red, por ejemplo Charles, para ver los datos.

## Configurar métricas de facturación {#configure-billing-metrics}

Si utiliza la configuración predeterminada, no tiene que hacer nada más para habilitar o configurar la facturación. Si ha obtenido parámetros de configuración diferentes del representante de habilitación de Adobe, utilice la clase PTBillingMetricsConfiguration para configurar estos parámetros antes de inicializar el reproductor de medios.

La mayoría de los clientes debe utilizar la configuración predeterminada.

>[!IMPORTANT]
>
>La configuración que defina permanecerá en vigor durante toda la vida útil del reproductor de medios. Una vez que inicialice el reproductor multimedia, no podrá cambiar la configuración.

Para configurar las métricas de facturación:

1. Introduzca la siguiente muestra de código.

   ```
   PTBillingMetricsConfiguration *billingConfig = [[[PTBillingMetricsConfiguration alloc] init] autorelease]; 
   billingConfig.enabled = YES; 
   billingConfig.stdVODBillableDurationMinutes = 60.0; 
   billingConfig.proVODBillableDurationMinutes = 30.0; 
   billingConfig.liveBillableDurationMinutes = 15.0; 
   
   // metadata is the PTMetadata instance set on PTMediaPlayerItem 
   [metadata setMetadata:billingConfig forKey:PTBillingMetricsConfigurationMetadataKey];
   ```

## Transmitir métricas de facturación {#transmit-billing-metrics}

TVSDK envía métricas de facturación al Adobe en formato XML.

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

Si utiliza una herramienta de captura de red para supervisar las estadísticas que TVSDK transmite a Adobe, debería ver unidades como las siguientes:

```
<request> 
     <sc_xml_ver>1.0</sc_xml_ver> 
     <reportSuiteID>ptebilling</reportSuiteID> 
     <visitorID>5536C629-5EF7-4F02-8E5D-9FA136CB3CED</visitorID> 
     <pageName>com.adobe.primetime.psdksample</pageName> 
     <timestamp>2016-11-22T18:06:30+0000</timestamp> 
     <userAgent>Mozilla/5.0 (iPad; CPU OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Mobile/13B143</userAgent> 
     <contextData> 
         <billingMetrics> 
                 <contentDuration>1799111</contentDuration> 
                 <contentURL>https%3A%2F%2Fdevimages.apple.com.edgekey.net%2Fstreaming%2Fexamples%2Fbipbop_16x9%2Fbipbop_16x9_variant.m3u8</contentURL> 
                 <contentType>vod</contentType> 
                 <midrollEnabled>true</midrollEnabled> 
                 <tvsdkVersion>1.0.211</tvsdkVersion> 
                 <platform>Mozilla/5.0 (iPad; CPU OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Mobile/13B143</platform> 
                 <publisherID>com.adobe.primetime.psdksample</publisherID> 
                 <adsEnabled>true</adsEnabled> 
                 <type>start</type> 
         </billingMetrics> 
     </contextData> 
</request>
```

Las propiedades booleanas `drmProtected`, `adsEnabled` y `midrollEnabled` sólo aparecen si son verdaderas.