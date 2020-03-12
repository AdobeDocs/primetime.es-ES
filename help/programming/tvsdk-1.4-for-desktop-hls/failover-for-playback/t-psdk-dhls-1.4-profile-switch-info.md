---
description: Cuando el reproductor de medios cambia su perfil actual a un nuevo perfil, puede recuperar información sobre el conmutador, incluso cuando se cambia, información sobre la anchura y la altura o por qué se ha utilizado una velocidad de bits diferente.
seo-description: Cuando el reproductor de medios cambia su perfil actual a un nuevo perfil, puede recuperar información sobre el conmutador, incluso cuando se cambia, información sobre la anchura y la altura o por qué se ha utilizado una velocidad de bits diferente.
seo-title: Obtener información sobre el conmutador de perfil
title: Obtener información sobre el conmutador de perfil
uuid: e26ad9fb-6c54-450e-ab62-784d9033d214
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Obtener información sobre el conmutador de perfil{#get-information-about-profile-switch}

Cuando el reproductor de medios cambia su perfil actual a un nuevo perfil, puede recuperar información sobre el conmutador, incluso cuando se cambia, información sobre la anchura y la altura o por qué se ha utilizado una velocidad de bits diferente.

1. Escucha el `ProfileEvent.PROFILE_CHANGED` evento.

   El reproductor de medios TVSDK distribuye este evento cuando su algoritmo de conmutación de velocidad de bits adaptable cambia a otro perfil debido a las condiciones de red o de equipo. (Cuando cambia la velocidad de bits o el período).
1. Cuando se produce el evento, compruebe las siguientes propiedades para obtener información sobre el conmutador:

   * `profile`:: Identificador del nuevo perfil que se está utilizando.
   * `time`:: La hora de flujo en la que se produjo el cambio.
   * `description`:: Descripción textual del motivo de un cambio en la velocidad de bits, como una cadena de pares de clave/valor separados por punto y coma. Incluye un máximo de uno `Reason` y uno `Bitrate`. Si la información no está disponible o la velocidad de bits no ha cambiado, esta cadena está vacía.
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
       <li id="li_695AB4A89C9D4833AF6D8B6424FC912B">Conmutación por error </li> 
       </ul> </td> 
      </tr> 
      <tr> 
      <td colname="col1"> <span class="codeph"> Velocidad de bits </span> </td> 
      <td colname="col2"> 
       <ul id="ul_1B49BD90A91147359712E1AFD8877E23"> 
       <li id="li_1C8E593C65D34742B14A8D0EAD43E0A9"> <span class="codeph"> up </span>: Se incrementó la velocidad de bits </li> 
       <li id="li_B1A00E3985A849B6855E15CF70D79BB8"> <span class="codeph"> abajo </span>: Se ha reducido la velocidad de bits </li> 
       </ul> </td> 
      </tr> 
    </tbody>
</table>

    A continuación se muestran algunos ejemplos de cadenas `description` devueltas:
    
    &quot;
    &quot;Velocidad de bits::=up;Motivo::=Adaptación de red;&quot;
    
    &quot;Velocidad de bits::=down;Motivo::=Failover;&quot;
    &quot;
    
    * `width&#39;: Entero que indica la anchura en píxeles.
    * &quot;altura&quot;: Entero que indica la altura en píxeles.
    
    >[!NOTE]
    >
    >Los datos de anchura y altura solo están disponibles cuando se incluyen en la etiqueta &quot;RESOLUCIÓN&quot; en el manifiesto M3U8. Si la información no está incluida en la M3U8, las propiedades de anchura y altura se establecen en 0, ya que no forman parte de la información del perfil.

<!--<a id="example_A713D420AE2E4E3CB7B78C6BC732BE90"></a>-->

Por ejemplo:

```
_player.addEventListener(ProfileEvent.PROFILE_CHANGED, onProfileChange); 
private function onProfileChange(event:ProfileEvent):void { 
    _logger.info("#onProfileChange Current profile/bitrate has changed.  
      {0} for reason {1} of resolution [ {2} , {3} ]",  
      event.profile, event.description, event.width, event.height); 
}
```
