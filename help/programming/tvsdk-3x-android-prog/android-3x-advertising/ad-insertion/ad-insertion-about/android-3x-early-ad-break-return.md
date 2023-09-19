---
description: Para la inserción de anuncios de flujo en directo, es posible que tenga que salir de una pausa publicitaria antes de que se reproduzcan todos los anuncios de la pausa hasta su finalización.
title: Implementar un retorno de pausa publicitaria anticipado
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Implementar un retorno de pausa publicitaria anticipado {#implement-an-early-ad-break-return}

Para la inserción de anuncios de flujo en directo, es posible que tenga que salir de una pausa publicitaria antes de que se reproduzcan todos los anuncios de la pausa hasta su finalización.

Por ejemplo, es posible que la duración de la pausa publicitaria en ciertos eventos deportivos no se conozca antes de que comience la pausa. TVSDK proporciona una duración predeterminada, pero si el juego se reanuda antes de que termine el descanso, se debe salir de la pausa publicitaria. Otro ejemplo es una señal de emergencia durante una pausa publicitaria en una emisión en directo.

1. Suscribirse a `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN`, y `#EXT-X-CUE`, que son el empalme/empalme en los marcadores.
Para obtener más información sobre cómo unir/unir marcadores de publicidad, consulte [Generadores de oportunidades y solucionadores de contenido](../../ad-insertion/content-resolver/android-3x-content-resolver.md).
1. Usar un personalizado `ContentFactory`.
1. Entrada `retrieveGenerators`, use el `SpliceInPlacementOpportunityGenerator`.

   Por ejemplo:

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   Para obtener más información sobre el uso de un personalizado `ContentFactory`, consulte el paso 1 de [Implementar un generador de oportunidades personalizado](../../ad-insertion/content-resolver/android-3x-opp-detector-impl-android.md).

1. En el mismo personalizado `ContentFactory`, implementar `retrieveResolvers` e incluyen `AuditudeResolver` y `SpliceInCustomResolver`.

   Por ejemplo:

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```
