---
description: El SDK del explorador envía métricas de facturación al Adobe en formato XML.
seo-description: El SDK del explorador envía métricas de facturación al Adobe en formato XML.
seo-title: Transmitir métricas de facturación
title: Transmitir métricas de facturación
uuid: ed2638d2-7894-4840-b31a-51e48e0a3f49
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# Transmitir métricas de facturación{#transmit-billing-metrics}

El SDK del explorador envía métricas de facturación al Adobe en formato XML.

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

Si utiliza una herramienta de captura de red para supervisar las estadísticas que el SDK TVSDK del explorador transmite a Adobe, debería ver unidades como las siguientes:

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

Las propiedades booleanas `drmProtected`, `adsEnabled` y `midrollEnabled` sólo aparecen si son verdaderas.