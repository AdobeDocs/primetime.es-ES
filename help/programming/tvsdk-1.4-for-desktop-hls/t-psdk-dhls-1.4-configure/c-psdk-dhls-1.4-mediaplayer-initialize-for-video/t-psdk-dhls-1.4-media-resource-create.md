---
description: La clase MediaResource representa el contenido que debe cargar la instancia de MediaPlayer.
seo-description: La clase MediaResource representa el contenido que debe cargar la instancia de MediaPlayer.
seo-title: Crear un recurso de medios
title: Crear un recurso de medios
uuid: 3d03d92f-69b3-4da8-9b16-25a264115ae5
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Crear un recurso de medios {#create-a-media-resource}

Para cada nuevo contenido de vídeo, inicialice una instancia de MediaResource con información sobre el contenido del vídeo y cargue el recurso multimedia.

La clase MediaResource representa el contenido que debe cargar la instancia de MediaPlayer.

1. Cree un `MediaResource` elemento pasando información sobre el medio al `MediaResource` constructor.

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
      <td colname="col2"> <p>Una cadena que representa la URL del manifiesto/lista de reproducción del medio. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> type</span> </td> 
      <td colname="col2"> <p>Uno de los siguientes valores de cadena que corresponde al tipo de archivo indicado: 
        <ul id="ul_7512E90B7B294EF9BFBA2D68DE678CBB"> 
        <li id="li_AA84434E84184A3D909552794B425ABD"><span class="codeph"> MP4</span> : formato de archivo de medios base ISO (MP4) </li> 
        <li id="li_8A2F3752569344B59EE30303A8393488"><span class="codeph"> HLS</span> - M3U8 </li> 
        </ul> </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> metadatos</span> </td> 
      <td colname="col2"> <p>Instancia de la clase <span class="codeph"> Metadata</span> , que puede contener información personalizada sobre el contenido que se va a cargar. </p> <p>Algunos ejemplos de contenido son contenido alternativo o de publicidad para colocarlo dentro del contenido principal. Si utiliza publicidad, configure <span class="codeph"> AuditudeSettings</span> antes de utilizar este constructor. Para obtener más información, consulte <a href="../../../tvsdk-1.4-for-desktop-hls/ad-insertion/ad-insertion-metadata/c-psdk-dhls-1.4-ad-insertion-metadata.md" format="dita" scope="local"> Metadatos</a>de inserción de publicidad. </p> </td> 
      </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >TVSDK admite la reproducción solo para tipos de contenido específicos. Si intenta cargar cualquier otro tipo de contenido, TVSDK distribuye un evento de error.
   >
   >Para el contenido de vídeo a petición MP4 (VOD), TVSDK no admite reproducción mediante trucos, flujo de velocidad de bits adaptable (ABR), inserción de anuncios, subtítulos cerrados o DRM.

   El código siguiente crea una `MediaResource` instancia:

   ```
   // To do: Create metadata here
   MyResource = new MediaResource(
            "https://www.example.com/video/some-video.m3u8", 
            "HLS",
            MyMetadata)
   ```

   >[!TIP]
   >
   >En este punto, puede utilizar `MediaResource` descriptores de acceso (captadores) para examinar el tipo, la dirección URL y los metadatos del recurso.

1. Cargue el recurso de medios mediante una de las siguientes opciones:

   * La instancia de MediaPlayer.

      Para obtener más información, consulte [Carga de un recurso de medios en MediaPlayer](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).
   * R `MediaPlayerItemLoader` Para obtener más información, consulte [Carga de un recurso de medios en MediaPlayer](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).

