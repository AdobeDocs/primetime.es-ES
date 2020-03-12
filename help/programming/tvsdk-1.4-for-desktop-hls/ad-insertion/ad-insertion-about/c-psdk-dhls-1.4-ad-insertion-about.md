---
description: La inserción de anuncios resuelve anuncios para vídeo a petición (VOD), para flujo continuo en directo y para flujo continuo lineal con seguimiento de anuncios y reproducción de anuncios. TVSDK realiza las solicitudes necesarias al servidor de publicidad, recibe información sobre las publicidades del contenido especificado y coloca las publicidades en el contenido en fases.
seo-description: La inserción de anuncios resuelve anuncios para vídeo a petición (VOD), para flujo continuo en directo y para flujo continuo lineal con seguimiento de anuncios y reproducción de anuncios. TVSDK realiza las solicitudes necesarias al servidor de publicidad, recibe información sobre las publicidades del contenido especificado y coloca las publicidades en el contenido en fases.
seo-title: Inserción de publicidades
title: Inserción de publicidades
uuid: 25c79822-a861-427b-b6a8-24714b21aae4
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Información general {#inserting-ads-overview}

La inserción de anuncios resuelve anuncios para vídeo a petición (VOD), para flujo continuo en directo y para flujo continuo lineal con seguimiento de anuncios y reproducción de anuncios. TVSDK realiza las solicitudes necesarias al servidor de publicidad, recibe información sobre las publicidades del contenido especificado y coloca las publicidades en el contenido en fases.

Una *`ad break`* publicación contiene una o más publicidades que se reproducen en secuencia. TVSDK inserta las publicidades en el contenido principal como miembros de uno o varios saltos de publicidad.

## Deshabilitar las publicidades previas al lanzamiento {#disable-preroll-ads}

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
