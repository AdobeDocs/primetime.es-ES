---
description: La clase MediaResource representa el contenido que carga la instancia de MediaPlayer.
title: Creación de un recurso multimedia
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Creación de un recurso multimedia {#create-a-media-resource}

Para cada nuevo contenido de vídeo, inicialice una instancia de MediaResource con información sobre el contenido de vídeo y cargue el recurso de medios.

La clase MediaResource representa el contenido que carga la instancia de MediaPlayer.

1. Crear un `MediaResource` al pasar información sobre los medios a `MediaResource` constructor.

   El `MediaResource` El constructor requiere los siguientes parámetros:

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
      <td colname="col2"> Cadena que representa la dirección URL del manifiesto/lista de reproducción del contenido. </td> 
   </tr> 
   <tr> 
      <td colname="col1"> <span class="codeph"> type </span> </td> 
      <td colname="col2"> Uno de los siguientes miembros del <span class="codeph"> MediaResource.Type </span> enum, correspondiente al tipo de archivo indicado: 
      <ul id="ul_C286ED3C31364B858A1C9AF3356E9282"> 
      <li id="li_25B24EF76D8849DE8764539F25E435FA"> <span class="codeph"> HLS </span> - M3U8 </li> 
      <li id="li_1344A41B434D49229E392F1AAF9ECA81"> <span class="codeph"> ISOBMFF </span> - Formato de archivo de medios base ISO (MP4) </li> 
      <li id="li_92392073B7334916B06B16570C51AC91"> <span class="codeph"> GUIÓN </span> - Descripción de la presentación en medios MPEG-DASH (MPD) </li> 
      </ul> </td> 
   </tr> 
   <tr> 
      <td colname="col1"> <span class="codeph"> metadatos </span> </td> 
      <td colname="col2"> Una instancia de <span class="codeph"> Metadatos </span> (una estructura similar a un diccionario), que puede contener información adicional sobre el contenido que se va a cargar, como contenido alternativo o publicitario que se va a colocar dentro del contenido principal. Si utiliza publicidad, configure <span class="codeph"> AuditudeSettings </span> antes de usar este constructor <a href="/help/programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-insertion-metadata/android-3x-ad-insertion-metadata.md"> Metadatos de inserción de publicidad </a>. </td> 
   </tr> 
   </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >TVSDK solo admite la reproducción de tipos de contenido específicos. Si intenta cargar cualquier otro tipo de contenido, TVSDK envía un evento de error.
   >
   >Para el contenido de MP4 vídeo bajo demanda (VOD), TVSDK no admite trucos, flujo de velocidad de bits adaptable (ABR), inserción de publicidad, subtítulos opcionales o DRM.

   El siguiente código crea un `MediaResource` instancia: >

   ```java
   // To do: Create metadata here 
   MediaResource res = new MediaResource( 
     "https://www.example.com/video/some-video.m3u8",  
   MediaResource.Type.HLS, 
     metadata); 
   ```

   En cualquier momento después de este paso, puede utilizar `MediaResource` descriptores de acceso (getters) para examinar el tipo, la dirección URL y los metadatos del recurso.

1. Cargue el recurso de medios mediante una de las siguientes opciones:

   * La instancia de MediaPlayer.
   * `MediaPlayerItemLoader` Para obtener más información, consulte [Cargar un recurso multimedia mediante MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

   >[!IMPORTANT]
   >
   >No cargue el recurso multimedia en un subproceso en segundo plano. La mayoría de las operaciones de TVSDK deben ejecutarse en el subproceso principal, y ejecutarlas en un subproceso en segundo plano puede provocar que la operación genere un error y salga.
