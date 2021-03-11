---
description: Para la inserción de anuncios en directo, es posible que tenga que salir de una pausa publicitaria antes de que todos los anuncios de la pausa se reproduzcan hasta el final.
title: Implementación de un retorno de pausa publicitaria anticipado
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 2%

---


# Implementar un retorno de pausa publicitaria anticipado {#implement-an-early-ad-break-return}

Para la inserción de anuncios en directo, es posible que tenga que salir de una pausa publicitaria antes de que todos los anuncios de la pausa se reproduzcan hasta el final.

Por ejemplo, es posible que la duración de la pausa publicitaria en ciertos eventos deportivos no se conozca antes de que comience la pausa. TVSDK proporciona una duración predeterminada, pero si el juego se reanuda antes de que finalice la pausa publicitaria, debe salir de la misma. Otro ejemplo es una señal de emergencia durante una pausa publicitaria en una emisión en directo.

1. Suscríbase a `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN` y `#EXT-X-CUE`, que son el empalme de los marcadores.
Para obtener más información sobre cómo empalmar/insertar marcadores de anuncios, consulte [Generadores de oportunidades y resoltores de contenido](../../ad-insertion/content-resolver/android-3x-content-resolver.md).
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
