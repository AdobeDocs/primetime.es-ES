---
description: 'null'
seo-description: 'null'
seo-title: Medición de anuncios de Moat
title: Medición de anuncios de Moat
uuid: a29c1e74-df15-47d2-9bd6-1d366c5cdf37
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Medición de anuncios de Moat {#ad-measurement-from-moat}

TVSDK toma información de FreeWheel y otros servidores de publicidad que proporcionan respuestas VAST. FreeWheel proporciona, dentro de las respuestas VAST, información del servicio Moat. El servicio Moat cuenta e impresiones con una precisión que muestra mejor que los creativos captan o descuidan los intereses de una audiencia.

Moat es un servicio que mide la visualización de anuncios en muchos usos, desde exploradores hasta aplicaciones. Moat genera datos de análisis de marketing en tiempo real en varias plataformas.

El XML de respuesta VAST tiene una propiedad y un elemento que el código puede leer, la propiedad de identificación de publicidad más externa y el elemento de extensión más externo. De cualquier forma, el código puede utilizar TVSDK para guardar la información de identificación de publicidad y la información de extensión y organizar la información en una estructura de árbol. Con esta organización, el código puede recoger los datos de cualquier nivel y pasarlos a donde sea necesario. El valor de la propiedad de identificación de publicidad externa permite que el código coordine la información de la campaña asociada.

Por ejemplo, FreeWheel puede devolver datos en un elemento Extensions. A continuación se muestra un elemento de muestra.

```
<?xml version="1.0"?> 
    <Extensions> 
      <Extension type="FreeWheel"> 
        <Parameter name="moat"> 
          <MeasurementInfo renditionID="6398737" type="MediaFile"> 
            <MoatID><![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]></MoatID> 
          </MeasurementInfo> 
          <MeasurementInfo renditionID="6398739" type="MediaFile"> 
            <MoatID><![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]></MoatID> 
          </MeasurementInfo> 
        </Parameter> 
      </Extension> 
    </Extensions> 
```

El volante libre también puede establecer la propiedad id en el elemento Ad, como se muestra en el ejemplo siguiente.

```
<Ad id="118566" sequence="1">
```

Consulte la documentación de la API de la clase AdobePSDK.NetworkAdInfo.
