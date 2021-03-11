---
description: Cuando el reproductor de contenidos cambia su perfil actual a un nuevo perfil, puede recuperar información sobre el conmutador, incluido el momento en que se cambió, la información de ancho y alto o el motivo por el que se usó una velocidad de bits diferente.
title: Obtener información sobre el conmutador de perfil
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---


# Obtener información sobre el conmutador de perfil{#get-information-about-profile-switch}

Cuando el reproductor de contenidos cambia su perfil actual a un nuevo perfil, puede recuperar información sobre el conmutador, incluido el momento en que se cambió, la información de ancho y alto o el motivo por el que se usó una velocidad de bits diferente.

1. Escuche el evento `AdobePSDK.PSDKEventType.PROFILE_CHANGED`.

   El reproductor multimedia TVSDK del explorador envía este evento cuando su algoritmo de conmutación de velocidad de bits adaptable cambia a otro perfil debido a condiciones de red o de equipo. (Cuando cambia la velocidad de bits o el período).
1. Cuando se produce el evento, compruebe las siguientes propiedades para obtener información sobre el conmutador:

   * `profile`: Identificador del nuevo perfil que se está utilizando.
   * `time`: La hora de emisión a la que se produjo el cambio.
   * `description`: Descripción textual del motivo de un cambio en la velocidad de bits, como una cadena de pares de clave/valor separados por punto y coma. Incluye un máximo de un `Reason` y un `Bitrate`. Si la información no está disponible o la velocidad de bits no ha cambiado, esta cadena está vacía.

   <table id="table_E400FD9C57FF40CBAC14AF6847CD8301"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> Nombre de clave </th> 
      <th colname="col2" class="entry"> Valores posibles </th> 
      </tr> 
    </thead>
    <tbody> 
      <tr> 
      <td colname="col1"> <span class="codeph"> Razón  </span> </td> 
      <td colname="col2"> 
        <ul id="ul_37DDE3F297634ED6B47DF5D73F969369"> 
        <li id="li_E374B029E1AF40689D70A9D30E057C5B">Adaptación de red </li> 
        <li id="li_753862EEF1C9474EA8E20C89F5EF5D8D">Buscar </li> 
        <li id="li_EC14923F92CF4D11A47928A8D2DE6D8B">Perfil no admitido </li> 
        <li id="li_695AB4A89C9D4833AF6D8B6424FC912B">Failover </li> 
        </ul> </td> 
      </tr> 
      <tr> 
      <td colname="col1"> <span class="codeph"> Velocidad de bits  </span> </td> 
      <td colname="col2"> 
        <ul id="ul_1B49BD90A91147359712E1AFD8877E23"> 
        <li id="li_1C8E593C65D34742B14A8D0EAD43E0A9"> <span class="codeph"> arriba  </span>: La tasa de bits ha aumentado </li> 
        <li id="li_B1A00E3985A849B6855E15CF70D79BB8"> <span class="codeph"> abajo  </span>: La velocidad de bits disminuyó </li> 
        </ul> </td> 
      </tr> 
    </tbody> 
    </table>

   A continuación se muestran algunos ejemplos de cadenas devueltas `description`:

   ```
   "Bitrate::=up;Reason::=Network Adaptation;" 
   
   "Bitrate::=down;Reason::=Failover;"
   ```

   * `width`: Número entero que indica la anchura en píxeles.
   * `height`: Número entero que indica la altura en píxeles.

   >[!NOTE]
   >
   >Los datos de ancho y alto solo están disponibles cuando se incluyen en la etiqueta `RESOLUTION` del manifiesto M3U8. Si la información no está incluida en la M3U8, las propiedades de anchura y altura se establecen en 0, ya que no forman parte de la información de perfil.
