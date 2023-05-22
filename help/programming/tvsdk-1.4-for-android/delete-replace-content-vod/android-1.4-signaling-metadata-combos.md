---
description: Puede marcar, eliminar y reemplazar intervalos de tiempo en flujos de VOD mediante diferentes combinaciones de modo de señalización de publicidad y metadatos de publicidad. Las diferentes combinaciones de modo de señalización y metadatos resultan en comportamientos diferentes.
title: Efecto en la inserción y eliminación de publicidad de las combinaciones de modo de señalización de publicidad y metadatos de publicidad
exl-id: 0b265471-2d5c-432b-b1c9-c850ce99f2f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Efecto en la inserción y eliminación de publicidad de las combinaciones de modo de señalización de publicidad y metadatos de publicidad{#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Puede marcar, eliminar y reemplazar intervalos de tiempo en flujos de VOD mediante diferentes combinaciones de modo de señalización de publicidad y metadatos de publicidad. Las diferentes combinaciones de modo de señalización y metadatos resultan en comportamientos diferentes.

>[!NOTE]
>
>Cuando hay un conflicto entre los intervalos de tiempo y los modos de señalización de publicidad, TVSDK da prioridad a los intervalos de tiempo.

**Tabla 3: Comportamientos de la combinación de modo de señalización y metadatos**

<table>  
 <thead> 
  <tr> 
   <th class="entry"> Modo de señalización de anuncio </th> 
   <th class="entry"> Metadatos de anuncio </th> 
   <th class="entry"> Resoluciones creadas </th> 
   <th class="entry"><span class="codeph"> Información de ubicación</span> created </th> 
   <th class="entry"> Comportamiento resultante </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <b>Mapa del servidor</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> Eliminar </td> 
   <td> Eliminar </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Intervalos eliminados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Eliminar, audiencia </td> 
   <td> Eliminar, audiencia </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), </span> </li> 
     <li><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> Intervalos eliminados, anuncios insertados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> Anuncios insertados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Reemplazar, Audiencia </td> 
   <td> Eliminar, audiencia </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervalos reemplazados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Marcar </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Marcar, audiencia </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados, sin anuncios insertados </td> 
  </tr> 
  <tr> 
   <td> <b>Señales de manifiesto</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.PRE_ROLL, Mode.INSERT)</span> </td> 
   <td> Anuncios insertados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Eliminar, audiencia </td> 
   <td> Eliminar, audiencia </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </li> 
     <li><span class="codeph"> PlacementInfo (Type.PRE_ROLL, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> Intervalos eliminados, anuncios insertados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Marcar, audiencia </td> 
   <td> Marcar, audiencia </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados, sin anuncios insertados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Eliminar </td> 
   <td> Eliminar </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Intervalos eliminados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Marcar </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Reemplazar, Audiencia </td> 
   <td> Eliminar, audiencia </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervalos reemplazados </td> 
  </tr> 
  <tr> 
   <td> <b>Intervalo de tiempo personalizado</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Eliminar </td> 
   <td> Eliminar </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Intervalos eliminados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Eliminar, audiencia </td> 
   <td> Eliminar, audiencia </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Intervalos eliminados, sin anuncios insertados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td> Ninguno </td> 
   <td> No hay anuncios insertados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Reemplazar, Audiencia </td> 
   <td> Eliminar, audiencia </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervalos reemplazados por anuncios </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Marcar </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Marcar, audiencia </td> 
   <td> Anuncio personalizado, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados, sin anuncios insertados </td> 
  </tr> 
  <tr> 
   <td> <b>Sin configurar (predeterminado)</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Eliminar </td> 
   <td> Eliminar </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Intervalos eliminados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Eliminar, audiencia </td> 
   <td> Eliminar, audiencia </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> Intervalos eliminados, anuncios insertados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> Anuncios insertados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Reemplazar, Audiencia </td> 
   <td> Eliminar, audiencia </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervalos reemplazados por anuncios </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Marcar </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Marcar, audiencia </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados </td> 
  </tr> 
 </tbody> 
</table>
