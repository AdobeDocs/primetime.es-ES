---
description: El SDK de explorador envía métricas de facturación a Adobes en formato XML.
title: Transmitir métricas de facturación
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 0%

---


# Transmitir métricas de facturación{#transmit-billing-metrics}

El SDK de explorador envía métricas de facturación a Adobes en formato XML.

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

Si utiliza una herramienta de captura de red para monitorizar las estadísticas que TVSDK del explorador transmite al Adobe, debería ver unidades como las siguientes:

```
<?xml version="1.0" encoding="UTF-8"?>
<request>
    <sc_xml_ver>1.0</sc_xml_ver>
    <reportSuiteID>primesample2</reportSuiteID>
    <visitorID>947310128cb56f41</visitorID>
    <pageURL>https://. . ..m3u8</pageURL>
    <timestamp>2016-4-7T10:1:4</timestamp>
    <contextData>
        <billingMetrics>
            <publisherID>com.adobe.primetime.reference.PrimetimeReference</publisherID>
            <contentType>vod</contentType>
            <adsEnabled>true</adsEnabled>
            <midrollEnabled>true</midrollEnabled>
            <platform>Mac OSX 10.11.5</platform>
            <tvsdkVersion>2,4,0,1559</tvsdkVersion>
            <contentURL>https://. . ..m3u8</contentURL>
        </billingMetrics>
    </contextData>
</request>
```

Las propiedades booleanas `drmProtected`, `adsEnabled` y `midrollEnabled` solo aparecen si son verdaderas.