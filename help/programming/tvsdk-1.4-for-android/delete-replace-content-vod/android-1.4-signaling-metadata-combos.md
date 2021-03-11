---
description: Puede marcar, eliminar y reemplazar intervalos de tiempo en flujos de VOD mediante el uso de diferentes modos de señalización de anuncios y combinaciones de metadatos de anuncios. Las diferentes combinaciones de modo de señalización y metadatos dan como resultado comportamientos diferentes.
title: Efecto en la inserción y eliminación de anuncios del modo de señalización de anuncios y las combinaciones de metadatos de anuncios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# Efectos en la inserción y eliminación de anuncios del modo de señalización de anuncios y las combinaciones de metadatos de anuncios{#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Puede marcar, eliminar y reemplazar intervalos de tiempo en flujos de VOD mediante el uso de diferentes modos de señalización de anuncios y combinaciones de metadatos de anuncios. Las diferentes combinaciones de modo de señalización y metadatos dan como resultado comportamientos diferentes.

>[!NOTE]
>
>Cuando hay un conflicto entre intervalos de tiempo y modos de señalización de anuncios, TVSDK da prioridad a los intervalos de tiempo.

**Tabla 3: Comportamientos de combinación de modo de señalización/metadatos**

<table>  
 <thead> 
  <tr> 
   <th class="entry"> Modo de señalización de publicidad </th> 
   <th class="entry"> Metadatos de publicidad </th> 
   <th class="entry"> Resoluciones creadas </th> 
   <th class="entry"><span class="codeph"> </span> Información de ubicación creada </th> 
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
   <td> Rangos eliminados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Eliminar, Auditude </td> 
   <td> Eliminar, Auditude </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),  </span> </li> 
     <li><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> Rangos eliminados, anuncios insertados </td> 
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
   <td> Reemplazar, Auditude </td> 
   <td> Eliminar, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Rangos reemplazados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Marcar </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Rangos marcados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Marcar, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Rangos marcados, sin anuncios insertados </td> 
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
   <td> Eliminar, Auditude </td> 
   <td> Eliminar, Auditude </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </li> 
     <li><span class="codeph"> PlacementInfo (Type.PRE_ROLL, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> Rangos eliminados, anuncios insertados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Marcar, Auditude </td> 
   <td> Marcar, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Rangos marcados, sin anuncios insertados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Eliminar </td> 
   <td> Eliminar </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Rangos eliminados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Marcar </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Rangos marcados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Reemplazar, Auditude </td> 
   <td> Eliminar, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Rangos reemplazados </td> 
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
   <td> Rangos eliminados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Eliminar, Auditude </td> 
   <td> Eliminar, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> Rangos eliminados, sin anuncios insertados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td> Ninguna </td> 
   <td> No se insertaron anuncios </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Reemplazar, Auditude </td> 
   <td> Eliminar, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Rangos reemplazados por anuncios </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Marcar </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Rangos marcados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Marcar, Auditude </td> 
   <td> Publicidad personalizada, audiencia </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Rangos marcados, sin anuncios insertados </td> 
  </tr> 
  <tr> 
   <td> <b>Sin establecer (predeterminado)</b> </td> 
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
   <td> Rangos eliminados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Eliminar, Auditude </td> 
   <td> Eliminar, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> Rangos eliminados, anuncios insertados </td> 
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
   <td> Reemplazar, Auditude </td> 
   <td> Eliminar, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Rangos reemplazados por anuncios </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Marcar </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Rangos marcados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Marcar, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Rangos marcados </td> 
  </tr> 
 </tbody> 
</table>

