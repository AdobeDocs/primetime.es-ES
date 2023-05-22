---
description: La inserción de anuncios resuelve los anuncios para vídeo bajo demanda (VOD) , para flujo en directo y para flujo lineal con seguimiento de anuncios y reproducción de anuncios. TVSDK realiza las solicitudes necesarias al servidor de publicidad, recibe información sobre los anuncios del contenido especificado y coloca los anuncios en el contenido por fases.
title: Inserción de anuncios
exl-id: 3a472435-2e37-46d6-8c08-dd6e953c7a7a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# Información general {#inserting-ads-overview}

La inserción de anuncios resuelve los anuncios para vídeo bajo demanda (VOD) , para flujo en directo y para flujo lineal con seguimiento de anuncios y reproducción de anuncios. TVSDK realiza las solicitudes necesarias al servidor de publicidad, recibe información sobre los anuncios del contenido especificado y coloca los anuncios en el contenido por fases.

Un *`ad break`* contiene uno o más anuncios que se reproducen en secuencia. TVSDK inserta anuncios en el contenido principal como miembros de una o más pausas publicitarias.

## Deshabilitar anuncios previos a la emisión {#disable-preroll-ads}

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
