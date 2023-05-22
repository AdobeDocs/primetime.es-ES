---
title: Deshabilitar anuncios previos a la emisión
description: Deshabilitar anuncios previos a la emisión
copied-description: true
exl-id: ff52588e-540e-4072-bec0-e531c8cb6fe3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '43'
ht-degree: 0%

---

# Deshabilitar anuncios previos a la emisión{#disable-pre-roll-ads}

Para deshabilitar el anuncio previo a la emisión, cambie los generadores de oportunidades predeterminados para que no realicen la llamada previa a la emisión. Los generadores de oportunidades predeterminados son:

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

Para deshabilitar el anuncio previo a la emisión en directo, cambie lo anterior para incluir solo SpliceOutOpportunityGenerator:

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
