---
description: TVSDK toma información de FreeWheel y otros servidores de publicidad que proporcionan respuestas VAST. FreeWheel proporciona, dentro de las respuestas VAST, información del servicio Moat. El servicio Moat cuenta e impresiones con una precisión que muestra mejor si los creativos capturan o descuidan los intereses de una audiencia.
seo-description: TVSDK toma información de FreeWheel y otros servidores de publicidad que proporcionan respuestas VAST. FreeWheel proporciona, dentro de las respuestas VAST, información del servicio Moat. El servicio Moat cuenta e impresiones con una precisión que muestra mejor si los creativos capturan o descuidan los intereses de una audiencia.
seo-title: Mediciones de anuncios de Moat
title: Mediciones de anuncios de Moat
uuid: b89f900f-50ab-4152-9c0f-11f82d92bffa
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Mediciones de anuncios de Moat{#ad-measurements-from-moat}

TVSDK toma información de FreeWheel y otros servidores de publicidad que proporcionan respuestas VAST. FreeWheel proporciona, dentro de las respuestas VAST, información del servicio Moat. El servicio Moat cuenta e impresiones con una precisión que muestra mejor si los creativos capturan o descuidan los intereses de una audiencia.

Moat es un servicio que mide la visualización de anuncios en muchos usos, desde exploradores hasta aplicaciones. Moat genera datos de análisis de marketing en tiempo real en varias plataformas.

El XML de respuesta VAST tiene una propiedad y un elemento que el código puede leer, la propiedad más externa `Ad id` y el `Extension` elemento más externo. De cualquier forma, el código puede utilizar TVSDK para guardar tanto la `Ad id` información como la `Extension` información y, a continuación, organizar la información en una estructura de árbol. Con esta organización, el código puede recoger los datos de cualquier nivel y pasarlos a donde sea necesario. El valor de la `Ad id` propiedad más externa permite que el código coordine la información de la campaña asociada.

Por ejemplo, FreeWheel puede devolver datos en un elemento Extensions. A continuación se muestra un elemento de muestra.

```xml
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

El volante también puede establecer la `id` propiedad en el `Ad` elemento, como se muestra en el ejemplo siguiente.

```xml
<Ad id="118566" sequence="1">
```

Para obtener información sobre API, consulte la documentación de API de la clase [NetworkAdInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/)
