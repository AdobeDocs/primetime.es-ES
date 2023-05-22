---
description: Cuando el reproductor multimedia cambia su perfil actual a un nuevo perfil, puede recuperar información sobre el conmutador, incluso cuándo ha cambiado, la información de anchura y altura o por qué se ha utilizado una velocidad de bits diferente.
title: Obtener información sobre el conmutador de perfil
exl-id: 3ef4b319-dd78-4abd-9c2d-ab1d608f6cea
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---

# Obtener información sobre el conmutador de perfil{#get-information-about-profile-switch}

Cuando el reproductor multimedia cambia su perfil actual a un nuevo perfil, puede recuperar información sobre el conmutador, incluso cuándo ha cambiado, la información de anchura y altura o por qué se ha utilizado una velocidad de bits diferente.

1. Escuche el `AdobePSDK.PSDKEventType.PROFILE_CHANGED` evento.

   El reproductor multimedia TVSDK del explorador envía este evento cuando su algoritmo de conmutación de velocidad de bits adaptable cambia a otro perfil debido a condiciones de red o del equipo. (Cuando cambia la velocidad de bits o el período.)
1. Cuando se produzca el evento, compruebe las siguientes propiedades para obtener información sobre el modificador:

   * `profile`: Identificador del nuevo perfil que se está utilizando.
   * `time`: tiempo de flujo en el que se produjo el cambio.
   * `description`: Descripción textual del motivo del cambio de la velocidad de bits, como una cadena de pares de clave/valor separados por punto y coma. Incluye un máximo de uno `Reason` y uno `Bitrate`. Si la información no está disponible o la velocidad de bits no ha cambiado, esta cadena está vacía.

   <table id="table_E400FD9C57FF40CBAC14AF6847CD8301"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> Nombre de clave </th> 
      <th colname="col2" class="entry"> Valores posibles </th> 
      </tr> 
    </thead>
    <tbody> 
      <tr> 
      <td colname="col1"> <span class="codeph"> Motivo </span> </td> 
      <td colname="col2"> 
        <ul id="ul_37DDE3F297634ED6B47DF5D73F969369"> 
        <li id="li_E374B029E1AF40689D70A9D30E057C5B">Adaptación de red </li> 
        <li id="li_753862EEF1C9474EA8E20C89F5EF5D8D">Buscar </li> 
        <li id="li_EC14923F92CF4D11A47928A8D2DE6D8B">Perfil no admitido </li> 
        <li id="li_695AB4A89C9D4833AF6D8B6424FC912B">Failover </li> 
        </ul> </td> 
      </tr> 
      <tr> 
      <td colname="col1"> <span class="codeph"> Velocidad de bits </span> </td> 
      <td colname="col2"> 
        <ul id="ul_1B49BD90A91147359712E1AFD8877E23"> 
        <li id="li_1C8E593C65D34742B14A8D0EAD43E0A9"> <span class="codeph"> arriba </span>: velocidad de bits aumentada </li> 
        <li id="li_B1A00E3985A849B6855E15CF70D79BB8"> <span class="codeph"> abajo </span>: velocidad de bits disminuida </li> 
        </ul> </td> 
      </tr> 
    </tbody> 
    </table>

   Estos son algunos ejemplos de `description` cadenas:

   ```
   "Bitrate::=up;Reason::=Network Adaptation;" 
   
   "Bitrate::=down;Reason::=Failover;"
   ```

   * `width`: Entero que indica la anchura en píxeles.
   * `height`: Entero que indica la altura en píxeles.

   >[!NOTE]
   >
   >Los datos de anchura y altura solo están disponibles cuando están incluidos en la variable `RESOLUTION` en el manifiesto M3U8. Si la información no se incluye en el M3U8, las propiedades de anchura y altura se establecen en 0, ya que no forman parte de la información de perfil.
