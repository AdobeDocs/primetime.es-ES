---
description: La clase MediaResource representa el contenido que debe cargar la instancia de MediaPlayer.
seo-description: La clase MediaResource representa el contenido que debe cargar la instancia de MediaPlayer.
seo-title: Crear un recurso de medios
title: Crear un recurso de medios
uuid: 9ae86c04-7bbe-43fb-9f57-1d9fa2fa73d0
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# Crear un recurso de medios {#create-a-media-resource}

Para cada nuevo contenido de vídeo, inicialice una instancia de MediaResource con información sobre el contenido del vídeo y cargue el recurso multimedia.

La clase MediaResource representa el contenido que debe cargar la instancia de MediaPlayer.

1. Cree un `MediaResource` elemento pasando información sobre el medio al `MediaResource` constructor.

   El constructor `MediaResource` requiere los parámetros siguientes:

   <table id="table_22886D6770FB45E99D35D0B90E6CC302"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> Parámetro de constructor </th> 
      <th colname="col2" class="entry"> Descripción </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> <span class="codeph"> url </span> </td> 
      <td colname="col2"> Una cadena que representa la URL del manifiesto/lista de reproducción del medio. </td> 
   </tr> 
   <tr> 
      <td colname="col1"> <span class="codeph"> type </span> </td> 
      <td colname="col2"> Uno de los siguientes miembros de la enumeración <span class="codeph"> MediaResource.Type </span> , correspondiente al tipo de archivo indicado: 
      <ul id="ul_C286ED3C31364B858A1C9AF3356E9282"> 
      <li id="li_25B24EF76D8849DE8764539F25E435FA"> <span class="codeph"> HLS </span> - M3U8 </li> 
      <li id="li_1344A41B434D49229E392F1AAF9ECA81"> <span class="codeph"> ISOBMFF </span> : formato de archivo de medios base ISO (MP4) </li> 
      <li id="li_92392073B7334916B06B16570C51AC91"> <span class="codeph"> DASH </span> - Descripción de la presentación de medios MPEG-DASH (MPD) </li> 
      </ul> </td> 
   </tr> 
   <tr> 
      <td colname="col1"> <span class="codeph"> metadatos </span> </td> 
      <td colname="col2"> Una instancia de la <span class="codeph"> clase Metadata </span> (una estructura parecida a un diccionario), que puede contener información adicional sobre el contenido que se va a cargar, como contenido alternativo o de anuncio para colocar dentro del contenido principal. Si utiliza publicidad, configure <span class="codeph"> AuditudeSettings </span> antes de utilizar este constructor (consulte href=Ad insert metadata](.../../android-3.5-publicidad/ad-insert/ad-insert-metadata/android-3.5-ad-insert-metadata.md). </td> 
   </tr> 
   </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >TVSDK admite la reproducción solo para tipos de contenido específicos. Si intenta cargar cualquier otro tipo de contenido, TVSDK distribuye un evento de error.
   >
   >Para el contenido de vídeo a petición MP4 (VOD), TVSDK no admite reproducción mediante trucos, flujo de velocidad de bits adaptable (ABR), inserción de anuncios, subtítulos cerrados o DRM.

   El código siguiente crea una `MediaResource` instancia:        >

   ```java
   // To do: Create metadata here 
   MediaResource res = new MediaResource( 
     "https://www.example.com/video/some-video.m3u8",  
   MediaResource.Type.HLS, 
     metadata); 
   ```

   En cualquier momento después de este paso, puede utilizar `MediaResource` descriptores de acceso (captadores) para examinar el tipo, la dirección URL y los metadatos del recurso.

1. Cargue el recurso de medios con una de las siguientes opciones:

   * La instancia de MediaPlayer.
   * `MediaPlayerItemLoader` Para obtener más información, consulte [Carga de un recurso multimedia mediante MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).
   >[!IMPORTANT]
   >
   >No cargue el recurso de medios en un subproceso en segundo plano. La mayoría de las operaciones de TVSDK deben ejecutarse en el subproceso principal y ejecutarlas en un subproceso en segundo plano puede provocar que la operación arroje un error y salga.
