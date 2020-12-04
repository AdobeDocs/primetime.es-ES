---
description: Puede marcar, eliminar y reemplazar intervalos de tiempo en flujos de VOD mediante diferentes modos de señalización de publicidad y combinaciones de metadatos de anuncio. Diferentes combinaciones de modo de señalización y metadatos dan como resultado comportamientos diferentes.
seo-description: Puede marcar, eliminar y reemplazar intervalos de tiempo en flujos de VOD mediante diferentes modos de señalización de publicidad y combinaciones de metadatos de anuncio. Diferentes combinaciones de modo de señalización y metadatos dan como resultado comportamientos diferentes.
seo-title: Efecto en la inserción y eliminación de publicidades en el modo de señalización de anuncios y en las combinaciones de metadatos de anuncios
title: Efecto en la inserción y eliminación de publicidades en el modo de señalización de anuncios y en las combinaciones de metadatos de anuncios
uuid: 7b2a5588-110d-4ce5-aa9c-706d357f211d
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---


# Efecto en la inserción y eliminación de publicidades del modo de señalización de anuncios y en combinaciones de metadatos de anuncios {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Puede marcar, eliminar y reemplazar intervalos de tiempo en flujos de VOD mediante diferentes modos de señalización de publicidad y combinaciones de metadatos de anuncio. Diferentes combinaciones de modo de señalización y metadatos dan como resultado comportamientos diferentes.

>[!TIP]
>
>Cuando hay un conflicto entre los intervalos de tiempo y los modos de señalización de publicidad, TVSDK da prioridad a los intervalos de tiempo.

La tabla siguiente proporciona los detalles sobre el modo de señalización y los comportamientos de combinación de metadatos:

<table id="table_6044AA1ACFA244FA814EA2D0766C6D12"> 
 <thead> 
  <tr> 
   <th class="entry"> Modo de señalización de publicidad </th> 
   <th class="entry"> Metadatos de anuncio </th> 
   <th class="entry"> Resoluciones creadas </th> 
   <th class="entry"><span class="codeph"> </span> PlacementInformationscreados </th> 
   <th class="entry"> Comportamiento resultante </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="1"> <p><b>Mapa del servidor</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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
    <ul id="ul_E0A2F885E93B4D23A486C37B305E17D8"> 
     <li id="li_D977B398D3904A44AFEC4B05AB0E3340"><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE),  </span> </li> 
     <li id="li_439886CB38AA46239C2E40352443888A"><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> Rangos eliminados, publicidades insertadas </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> Publicidades insertadas </td> 
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
   <td> Intervalos marcados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Marcar, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados, sin anuncios insertados </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p><b>Señales de manifiesto</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.PRE_ROLL, Mode.INSERT)</span> </td> 
   <td> Publicidades insertadas </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Eliminar, Auditude </td> 
   <td> Eliminar, Auditude </td> 
   <td> 
    <ul id="ul_2DD298538E9344B9BAB882485BB57747"> 
     <li id="li_F39A69EFA7ED45C18978A2C462AF7641"><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </li> 
     <li id="li_8CCDA3B1C63F4BC396F28F443D8C42F8"><span class="codeph"> PlacementInfo (Type.PRE_ROLL, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> Rangos eliminados, publicidades insertadas </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Marcar, Auditude </td> 
   <td> Marcar, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados, sin anuncios insertados </td> 
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
   <td> Intervalos marcados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Reemplazar, Auditude </td> 
   <td> Eliminar, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Rangos reemplazados </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p><b>Intervalo de tiempo personalizado</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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
   <td> Rangos eliminados, sin publicidades insertadas </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td> Ninguno </td> 
   <td> No se insertaron publicidades </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Reemplazar, Auditude </td> 
   <td> Eliminar, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervalos reemplazados por publicidades </td> 
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
   <td> Marcar, Auditude </td> 
   <td> Publicidad personalizada, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados, sin anuncios insertados </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p><b>No definido (predeterminado)</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
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
   <td> Rangos eliminados, publicidades insertadas </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> Publicidades insertadas </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Reemplazar, Auditude </td> 
   <td> Eliminar, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervalos reemplazados por publicidades </td> 
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
   <td> Marcar, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados </td> 
  </tr> 
 </tbody> 
</table>

