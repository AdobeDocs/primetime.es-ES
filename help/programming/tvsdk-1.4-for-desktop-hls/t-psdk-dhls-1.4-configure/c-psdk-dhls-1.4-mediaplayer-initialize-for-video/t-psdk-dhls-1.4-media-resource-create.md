---
description: La clase MediaResource representa el contenido que carga la instancia de MediaPlayer.
title: Creación de un recurso multimedia
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# Creación de un recurso multimedia {#create-a-media-resource}

Para cada nuevo contenido de vídeo, inicialice una instancia de MediaResource con información sobre el contenido de vídeo y cargue el recurso de medios.

La clase MediaResource representa el contenido que carga la instancia de MediaPlayer.

1. Crear un `MediaResource` al pasar información sobre los medios a `MediaResource` constructor.

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> Parámetro de constructor </th> 
      <th colname="col2" class="entry"> Descripción </th> 
      </tr>
    </thead>
    =<tbody> 
      <tr> 
      <td colname="col1"><span class="codeph"> url</span> </td> 
      <td colname="col2"> <p>Cadena que representa la dirección URL del manifiesto/lista de reproducción del contenido. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> type</span> </td> 
      <td colname="col2"> <p>Uno de los siguientes valores de cadena que corresponde al tipo de archivo indicado: 
        <ul id="ul_7512E90B7B294EF9BFBA2D68DE678CBB"> 
        <li id="li_AA84434E84184A3D909552794B425ABD"><span class="codeph"> MP4</span> - Formato de archivo de medios base ISO (MP4) </li> 
        <li id="li_8A2F3752569344B59EE30303A8393488"><span class="codeph"> HLS</span> - M3U8 </li> 
        </ul> </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> metadatos</span> </td> 
      <td colname="col2"> <p>Una instancia de <span class="codeph"> Metadatos</span> , que puede contener información personalizada sobre el contenido que se va a cargar. </p> <p>Algunos ejemplos de contenido son contenido alternativo o publicitario para colocar dentro del contenido principal. Si utiliza publicidad, configure <span class="codeph"> AuditudeSettings</span> antes de utilizar este constructor. Para obtener más información, consulte <a href="../../../tvsdk-1.4-for-desktop-hls/ad-insertion/ad-insertion-metadata/c-psdk-dhls-1.4-ad-insertion-metadata.md" format="dita" scope="local"> Metadatos del Ad Insertion</a>. </p> </td> 
      </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >TVSDK solo admite la reproducción de tipos de contenido específicos. Si intenta cargar cualquier otro tipo de contenido, TVSDK envía un evento de error.
   >
   >Para el contenido de MP4 vídeo bajo demanda (VOD), TVSDK no admite trucos, flujo de velocidad de bits adaptable (ABR), inserción de publicidad, subtítulos opcionales o DRM.

   El siguiente código crea un `MediaResource` instancia:

   ```
   // To do: Create metadata here
   MyResource = new MediaResource(
            "https://www.example.com/video/some-video.m3u8", 
            "HLS",
            MyMetadata)
   ```

   >[!TIP]
   >
   >En este punto, puede utilizar `MediaResource` descriptores de acceso (getters) para examinar el tipo, la dirección URL y los metadatos del recurso.

1. Cargue el recurso de medios mediante una de las siguientes opciones:

   * Su instancia de MediaPlayer.

     Para obtener más información, consulte [Carga de un recurso de medios en el reproductor de medios](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).
   * A `MediaPlayerItemLoader` Para obtener más información, consulte [Carga de un recurso de medios en el reproductor de medios](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).
