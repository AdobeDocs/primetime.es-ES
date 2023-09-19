---
description: Puede marcar, eliminar y reemplazar intervalos de tiempo en flujos de VOD mediante diferentes combinaciones de modo de señalización de publicidad y metadatos de publicidad. Las diferentes combinaciones de modo de señalización y metadatos resultan en comportamientos diferentes.
title: Efecto en la inserción y eliminación de publicidad de las combinaciones de modo de señalización de publicidad y metadatos de publicidad
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Efecto en la inserción y eliminación de publicidad de las combinaciones de modo de señalización de publicidad y metadatos de publicidad {#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

Puede marcar, eliminar y reemplazar intervalos de tiempo en flujos de VOD mediante diferentes combinaciones de modo de señalización de publicidad y metadatos de publicidad. Las diferentes combinaciones de modo de señalización y metadatos resultan en comportamientos diferentes.

>[!TIP]
>
>Cuando hay un conflicto entre los intervalos de tiempo y los modos de señalización de publicidad, TVSDK da prioridad a los intervalos de tiempo.

En la tabla siguiente se proporcionan los detalles sobre el modo de señalización y los comportamientos de combinación de metadatos:

<table id="table_6044AA1ACFA244FA814EA2D0766C6D12"> 
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
   <td> Intervalos eliminados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Eliminar, Auditude </td> 
   <td> Eliminar, Auditude </td> 
   <td> 
    <ul id="ul_E0A2F885E93B4D23A486C37B305E17D8"> 
     <li id="li_D977B398D3904A44AFEC4B05AB0E3340"><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), </span> </li> 
     <li id="li_439886CB38AA46239C2E40352443888A"><span class="codeph"> PlacementInfo (Type.SERVER_MAP, Mode.INSERT)</span> </li> 
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
   <td> Reemplazar, Auditude </td> 
   <td> Eliminar, Auditude </td> 
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
   <td> Mark, Auditude </td> 
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
   <td> Anuncios insertados </td> 
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
   <td> Intervalos eliminados, anuncios insertados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> Mark, Auditude </td> 
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
   <td> Reemplazar, Auditude </td> 
   <td> Eliminar, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.DELETE), PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> Intervalos reemplazados </td> 
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
   <td> Intervalos eliminados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Eliminar, Auditude </td> 
   <td> Eliminar, Auditude </td> 
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
   <td> Reemplazar, Auditude </td> 
   <td> Eliminar, Auditude </td> 
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
   <td> Mark, Auditude </td> 
   <td> Anuncio personalizado, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados, sin anuncios insertados </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p><b>Sin configurar (predeterminado)</b> </p> </td> 
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
   <td> Intervalos eliminados </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Eliminar, Auditude </td> 
   <td> Eliminar, Auditude </td> 
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
   <td> Reemplazar, Auditude </td> 
   <td> Eliminar, Auditude </td> 
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
   <td> Mark, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> Intervalos marcados </td> 
  </tr> 
 </tbody> 
</table>
