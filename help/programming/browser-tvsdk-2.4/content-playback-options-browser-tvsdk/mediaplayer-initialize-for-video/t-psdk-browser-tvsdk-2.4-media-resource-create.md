---
description: La clase MediaResource representa el contenido que carga la instancia de MediaPlayer.
title: Creación de un recurso multimedia
exl-id: ab66255d-7848-479a-a8cd-c6113cdd7749
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Creación de un recurso multimedia {#create-a-media-resource}

La clase MediaResource representa el contenido que carga la instancia de MediaPlayer.

1. Crear un `MediaResource` al pasar información sobre los medios a `MediaResource` constructor.

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
    <tr> 
    <th colname="col1" class="entry"> Parámetro de constructor </th> 
    <th colname="col2" class="entry"> Descripción </th> 
    </tr> 
    </thead>
    <tbody> 
    <tr> 
    <td colname="col1"> <p>url </p> </td> 
    <td colname="col2"> <p>Cadena que representa la dirección URL del manifiesto/lista de reproducción del contenido. </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>type </p> </td> 
    <td colname="col2"> <p>Uno de los siguientes miembros del <span class="codeph"> MediaResource.Type </span> enumeración que corresponde al tipo de archivo indicado: </p> <p> 
    <ul id="ul_E9689FA06DC94BF4848F16E1F2F01A59"> 
    <li id="li_83A14B96CDC648C6AF6F5FA745343E1F"> <span class="codeph"> MP4 </span> - Formato de archivo de medios base ISO (MP4) </li> 
    <li id="li_FCD355151515412D9A78C3815DD09129"> <span class="codeph"> HLS </span> - M3U8 </li> 
    <li id="li_9D3D306D49264830AC6EFB1F49524A3B"> <span class="codeph"> GUIÓN </span> - MPD </li> 
    </ul> </p> <p></p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>metadatos </p> </td> 
    <td colname="col2"> <p>Una instancia de <span class="codeph"> Metadatos </span> , que puede contener información personalizada sobre el contenido que se va a cargar. Algunos ejemplos de contenido son contenido alternativo o publicitario para colocar dentro del contenido principal. Si utiliza publicidad, configure <span class="codeph"> AuditudeSettings </span> antes de utilizar este constructor. Para obtener más información, consulte <a href="../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md">Ad-insertion-metadata</a>. </p> <p>Sugerencia: Puede forzar la reserva de Flash, si es necesario, utilizando la variable <span class="codeph"> forceFlash </span> al crear un recurso de medios. Esto puede resultar útil porque actualmente no todas las funciones (como los flujos de trabajo de publicidad en directo) son compatibles con el TVSDK del explorador. La reserva de Flash se utiliza para reproducir contenido de vídeo. </p> </td> 
    </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >El TVSDK del explorador admite la reproducción solo para tipos de contenido específicos. Si intenta cargar cualquier otro tipo de contenido, el TVSDK del explorador envía un evento de error.

   El siguiente código crea un `MediaResource` instancia:

   ```js
   //create a MediaResource instance pointing to some HLS content 
   Metadata metadata = //TODO: create metadata here 
   mediaResource = new AdobePSDK.MediaResource ( 
         "https://www.example.com/video/some-video.m3u8", 
         AdobePSDK.MediaResourceType.HLS,  
         metadata);
   ```

   >[!TIP]
   >
   >En cualquier momento después de esto, puede utilizar `MediaResource` descriptores de acceso (getters) para examinar el tipo, la dirección URL y los metadatos del recurso.

1. Cargue la instancia de MediaPlayer. Para obtener más información, consulte [Cargar un recurso multimedia en MediaPlayer](../../content-playback-options-browser-tvsdk/mediaplayer-initialize-for-video/t-psdk-browser-tvsdk-2.4-media-resource-load.md).
