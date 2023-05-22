---
description: TVSDK toma información de FreeWheel y otros adservers proporcionando respuestas VAST. FreeWheel proporciona, dentro de las respuestas VAST, información del servicio Moat. El servicio Moat cuenta las impresiones de los anuncios con una precisión que muestra mejor que los creativos capturan o descuidan los intereses de una audiencia.
title: Mediciones de anuncios de Moat
exl-id: f8f68e0b-985c-43bb-878e-e24fed54e0c3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# Mediciones de anuncios de Moat{#ad-measurements-from-moat}

TVSDK toma información de FreeWheel y otros adservers proporcionando respuestas VAST. FreeWheel proporciona, dentro de las respuestas VAST, información del servicio Moat. El servicio Moat cuenta las impresiones de los anuncios con una precisión que muestra mejor que los creativos capturan o descuidan los intereses de una audiencia.

Moat es un servicio que mide y visualiza muchos usos, desde navegadores hasta aplicaciones. Moat genera datos de análisis de marketing en tiempo real en varias plataformas.

El XML de respuesta VAST tiene una propiedad y un elemento que el código puede leer, la propiedad de ID de anuncio exterior y el elemento de extensión exterior. En cualquier caso, el código puede utilizar TVSDK para guardar la información del ID de anuncio y la información de extensión y organizar la información en una estructura de árbol. Con esta organización, el código puede recoger los datos de cualquier nivel y pasarlos a donde quiera que tengan que ir. El valor de la propiedad de ID de anuncio exterior permite al código coordinar la información de la campaña asociada.

Por ejemplo, FreeWheel puede devolver datos en un elemento Extensions. A continuación se muestra un elemento de muestra.

```xml
<Extensions> 
   <Extension type="FreeWheel"> 
    <Parameter name="moat"> 
     <MeasurementInfo renditionID="6398737" type="MediaFile"> 
      <MoatID> 
       <![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]]]> 
       <![CDATA[> 
        </MoatID> 
      </MeasurementInfo> 
      <MeasurementInfo renditionID="6398739" type="MediaFile"> 
        <MoatID> 
        <![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]]]> 
        <![CDATA[> 
        </MoatID> 
      </MeasurementInfo> 
    </Parameter> 
  </Extension> 
</Extensions>
```

Freewheel también puede establecer la propiedad de ID en el elemento de anuncio, como se muestra en el siguiente ejemplo.

```
<Ad id="118566" sequence="1">
```

Consulte la documentación de la API para la clase `PTNetworkAdInfo` in `PTAdAsset`.
