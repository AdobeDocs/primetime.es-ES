---
description: 'null'
seo-description: 'null'
seo-title: Deshabilitar las publicidades previas al lanzamiento
title: Deshabilitar las publicidades previas al lanzamiento
uuid: 2e307a58-49f2-43d6-908b-97684ad6e3d3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '45'
ht-degree: 0%

---


# Deshabilitar anuncios previos{#disable-pre-roll-ads}

Para desactivar el prelanzamiento, cambie los generadores de oportunidades predeterminados para que no realicen la llamada previa al lanzamiento. Los generadores de oportunidades predeterminados son:

```
@inheritDoc 
*/ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
result.push(new AdSignalingModeOpportunityGenerator()); 
result.push(new SpliceOutOpportunityGenerator()); 
return result; 
}
```

Para desactivar el prelanzamiento en los flujos en directo, cambie lo anterior para incluir solo SpliceOutOpportunityGenerator:

```
@inheritDoc 
*/ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
if (preroll_enabled == true) { result.push(new AdSignalingModeOpportunityGenerator()); } 
 
result.push(new SpliceOutOpportunityGenerator()); 
return result; 
}
```

