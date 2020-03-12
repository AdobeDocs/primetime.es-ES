---
description: La clase de utilidad TimeRangeCollection abstrae la noción de una colección ordenada de especificaciones de TimeRange y proporciona servicios para traducirse en una instancia de metadatos.
seo-description: La clase de utilidad TimeRangeCollection abstrae la noción de una colección ordenada de especificaciones de TimeRange y proporciona servicios para traducirse en una instancia de metadatos.
seo-title: Clase TimeRangeCollection
title: Clase TimeRangeCollection
uuid: da781df4-6b19-47e1-8dc5-ea83c139f061
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Clase TimeRangeCollection{#timerangecollection-class}

La clase de utilidad TimeRangeCollection abstrae la noción de una colección ordenada de especificaciones de TimeRange y proporciona servicios para traducirse en una instancia de metadatos.

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```
public final class TimeRangeCollection { 
    public static const MARK_RANGES:String = "mark_ranges"; 
  
    public function TimeRangeCollection(timeRanges:Vector.<TimeRange>) {…} 
    public function addTimeRange(timeRange:TimeRange):void {…} 
    public function toMetadata(options:Metadata):Metadata {…} 
}
```

El valor definido para el tipo de colección es `MARK_RANGES`, `DELETE_RANGES`y `REPLACE_RANGES`. Puede crear `TimeRangeCollection`s usando estos tres tipos.
