---
description: La clase de utilidad TimeRangeCollection abstrae la noción de una colección ordenada de especificaciones de TimeRange y proporciona servicios para traducirse a sí misma en una instancia de metadatos.
title: clase TimeRangeCollection
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---

# clase TimeRangeCollection{#timerangecollection-class}

La clase de utilidad TimeRangeCollection abstrae la noción de una colección ordenada de especificaciones de TimeRange y proporciona servicios para traducirse a sí misma en una instancia de metadatos.

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```
public final class TimeRangeCollection { 
    public static const MARK_RANGES:String = "mark_ranges"; 
  
    public function TimeRangeCollection(timeRanges:Vector.<TimeRange>) {…} 
    public function addTimeRange(timeRange:TimeRange):void {…} 
    public function toMetadata(options:Metadata):Metadata {…} 
}
```

Los valores definidos para el tipo de colección son `MARK_RANGES`, `DELETE_RANGES`, y `REPLACE_RANGES`. Puede crear `TimeRangeCollection`usa estos tres tipos.
