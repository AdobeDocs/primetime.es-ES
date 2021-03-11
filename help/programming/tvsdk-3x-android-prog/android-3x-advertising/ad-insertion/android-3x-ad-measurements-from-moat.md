---
description: TVSDK toma información de FreeWheel y otros servidores de publicidad que proporcionan respuestas VAST. FreeWheel proporciona, dentro de las respuestas VAST, información del servicio Moat. El servicio Moat cuenta las impresiones de los anuncios con una precisión que muestra mejor si los creativos capturan o descuidan los intereses de la audiencia.
title: Mediciones de anuncios de Moat
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---


# Mediciones de anuncios de Moat {#ad-measurements-from-moat}

TVSDK toma información de FreeWheel y otros servidores de publicidad que proporcionan respuestas VAST. FreeWheel proporciona, dentro de las respuestas VAST, información del servicio Moat. El servicio Moat cuenta las impresiones de los anuncios con una precisión que muestra mejor si los creativos capturan o descuidan los intereses de la audiencia.

Moat es un servicio que mide la visualización de anuncios en muchos usos, desde exploradores hasta aplicaciones. Moat genera datos de análisis de marketing en tiempo real en varias plataformas.

El XML de respuesta VAST tiene una propiedad y un elemento que el código puede leer, la propiedad `Ad id` más externa y el elemento `Extension` más externo. De cualquier manera, el código puede utilizar TVSDK para guardar tanto la información `Ad id` como la información `Extension` y, a continuación, organizar la información en una estructura de árbol. Con esta organización, su código puede recoger los datos de cualquier nivel y pasarlos a donde quiera que deban ir. El valor de la propiedad `Ad id` externa permite que el código coordine la información de la campaña asociada.

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

La rueda libre también puede establecer la propiedad `id` en el elemento `Ad`, como se muestra en el ejemplo siguiente.

```xml
<Ad id="118566" sequence="1">
```

Para obtener información de la API, consulte la documentación de la API para la clase `NetworkAdInfo`.