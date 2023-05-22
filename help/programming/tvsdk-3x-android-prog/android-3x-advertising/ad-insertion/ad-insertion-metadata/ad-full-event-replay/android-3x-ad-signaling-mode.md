---
description: El modo de señalización de anuncio especifica dónde debe obtener la información publicitaria el flujo de vídeo.
title: Modo de señalización de anuncio
exl-id: ddee6753-522f-46e8-8ba2-38b9593e7abe
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Modo de señalización de anuncio {#ad-signaling-mode}

El modo de señalización de anuncio especifica dónde debe obtener la información publicitaria el flujo de vídeo.

Los valores válidos son `DEFAULT`, `SERVER_MAP`, y `MANIFEST_CUES`.

En la tabla siguiente se describe el efecto de `AdSignalingMode` valores para los distintos tipos de flujos HLS:

<table frame="all" colsep="1" rowsep="1" id="table_AdSignalingMode"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> </th> 
   <th colname="2" class="entry"> <b>Predeterminado </b></th> 
   <th colname="3" class="entry"><b> Señales de manifiesto</b> </th> 
   <th colname="4" class="entry"> <b>Mapa del servidor de publicidad </b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> Vídeo bajo demanda (VOD) </td> 
   <td colname="2"> 
    <ul id="ul_E79DA79107364D0D8B46A1859CA75B5C"> 
     <li id="li_B259ED87743F463095071F58DC840E39"> Utiliza el mapa del servidor para detectar la ubicación </li> 
     <li id="li_8957E4151466467BA6C954E5010E34EA"> Se insertan los anuncios </li> 
    </ul> </td> 
   <td colname="3"> 
    <ul id="ul_D462C76717D94DE09915BDF6E9B3FB68"> 
     <li id="li_FB46108F4AD9457D99D2618ABEF7DBD1"> Utiliza indicaciones en el flujo para la detección de ubicación </li> 
     <li id="li_C3F7FBB98F524CEF97D17318C292E9EA"> Los anuncios previos a la emisión se insertan en el flujo principal </li> 
     <li id="li_A56E1545F84840DFA6D065DA60E98C31"> Los anuncios mid-rolls reemplazan el flujo principal </li> 
    </ul> </td> 
   <td colname="4"> 
    <ul id="ul_F10192B1B6F745CBB0D4C1A6D52A57B4"> 
     <li id="li_2ADACF71FA5F4A08A00A3399F5593420"> Utiliza el mapa del servidor para detectar la ubicación </li> 
     <li id="li_1201085B9C554A4BBD471E7EB2E363AC"> Se insertan los anuncios </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> Activo/lineal </td> 
   <td colname="2"> 
    <ul id="ul_82AAC9EE056F49E999F809536A96C2F8"> 
     <li id="li_73BAD2BAA95F4592808B77F8DA436237"> Utiliza indicaciones de manifiesto para la detección de ubicación </li> 
     <li id="li_A97B6F61078D4149A984B2412021E103"> Los anuncios reemplazan el flujo principal </li> 
    </ul> </td> 
   <td colname="3"> 
    <ul id="ul_CAED2D4F46334D76AE025482881BF843"> 
     <li id="li_A8023845A037482DBFDEF7EF247FECFD"> Utiliza indicaciones en el flujo para la detección de ubicación </li> 
     <li id="li_62A3CDAD249344EB89043B2AE0F4D7FF"> Los anuncios reemplazan el flujo principal </li> 
    </ul> </td> 
   <td colname="4"> No compatible </td> 
  </tr> 
 </tbody> 
</table>
