---
title: Medición de anuncios de Moat
description: Medición de anuncios de Moat
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Medición de anuncios de Moat {#ad-measurement-from-moat}

TVSDK toma información de FreeWheel y otros adservers proporcionando respuestas VAST. FreeWheel proporciona, dentro de las respuestas VAST, información del servicio Moat. El servicio Moat cuenta las impresiones de los anuncios con una precisión que muestra mejor que los creativos capturan o descuidan los intereses de una audiencia.

Moat es un servicio que mide y visualiza muchos usos, desde navegadores hasta aplicaciones. Moat genera datos de análisis de marketing en tiempo real en varias plataformas.

El XML de respuesta VAST tiene una propiedad y un elemento que el código puede leer, la propiedad de ID de anuncio exterior y el elemento de extensión exterior. En cualquier caso, el código puede utilizar TVSDK para guardar la información del ID de anuncio y la información de extensión y organizar la información en una estructura de árbol. Con esta organización, el código puede recoger los datos de cualquier nivel y pasarlos a donde quiera que tengan que ir. El valor de la propiedad de ID de anuncio exterior permite al código coordinar la información de la campaña asociada.

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

Freewheel también puede establecer la propiedad de ID en el elemento de anuncio, como se muestra en el siguiente ejemplo.

```
<Ad id="118566" sequence="1">
```

Consulte la documentación de la API para la clase AdobePSDK.NetworkAdInfo.
