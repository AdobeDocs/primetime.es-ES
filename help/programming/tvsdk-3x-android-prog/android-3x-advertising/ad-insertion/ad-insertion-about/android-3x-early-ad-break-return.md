---
description: Para la inserción de anuncios en directo, es posible que tenga que salir de una pausa publicitaria antes de que todas las publicidades del desglose se reproduzcan hasta la finalización.
seo-description: Para la inserción de anuncios en directo, es posible que tenga que salir de una pausa publicitaria antes de que todas las publicidades del desglose se reproduzcan hasta la finalización.
seo-title: Implementar un retorno de pausa publicitaria anticipado
title: Implementar un retorno de pausa publicitaria anticipado
uuid: 0e77414e-86f5-4979-9caa-eaf2f39144a2
translation-type: tm+mt
source-git-commit: 3fdae2b6babb578d2cacff970fd9c7b53ad2c5dc
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 1%

---


# Implementar un retorno de pausa publicitaria anticipado {#implement-an-early-ad-break-return}

Para la inserción de anuncios en directo, es posible que tenga que salir de una pausa publicitaria antes de que todas las publicidades del desglose se reproduzcan hasta la finalización.

Por ejemplo, es posible que la duración de la pausa publicitaria en determinados eventos deportivos no se conozca antes de los inicios de interrupción. TVSDK proporciona una duración predeterminada, pero si el juego se reanuda antes de que finalice la pausa, la pausa publicitaria se debe salir. Otro ejemplo es una señal de emergencia durante una pausa publicitaria en un flujo en directo.

1. Suscríbase a `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN` y `#EXT-X-CUE`, que son el empalme de salida/empalme en los marcadores.
Para obtener más información acerca de cómo dividir los marcadores de publicidad, consulte [Generadores de oportunidades y solucionadores de contenido](../../ad-insertion/content-resolver/android-3x-content-resolver.md).
1. Utilice un `ContentFactory` personalizado.
1. En `retrieveGenerators`, utilice el `SpliceInPlacementOpportunityGenerator`.

   Por ejemplo:

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   Para obtener más información sobre el uso de un `ContentFactory` personalizado, consulte el paso 1 en [Implementar un generador de oportunidades personalizado](../../ad-insertion/content-resolver/android-3x-opp-detector-impl-android.md).

1. En el mismo `ContentFactory` personalizado, implemente `retrieveResolvers` e incluya `AuditudeResolver` y `SpliceInCustomResolver`.

   Por ejemplo:

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```
