---
description: Para cada nuevo contenido de vídeo, inicialice una instancia de MediaResource con información sobre el contenido de vídeo y cargue el recurso de medios. La clase MediaResource representa el contenido que carga la instancia de MediaPlayer.
title: Creación de un recurso multimedia
exl-id: cda70f91-7f30-4e37-9dfa-888b707e3d61
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Creación de un recurso multimedia {#create-a-media-resource}

Para cada nuevo contenido de vídeo, inicialice una instancia de MediaResource con información sobre el contenido de vídeo y cargue el recurso de medios. La clase MediaResource representa el contenido que carga la instancia de MediaPlayer.

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
    <td colname="col2"> <p>Uno de los siguientes miembros del <span class="codeph"> MediaResource.Type </span> enumeración que corresponde al tipo de archivo indicado: 
    <ul id="ul_72636C41CA7E4538A3BE11A79E0282FC"> 
    <li id="li_070960200DEB40E992C58FCB8909AEA3"> <span class="codeph"> HLS </span> - M3U8 </li> 
    </ul> </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>metadatos </p> </td> 
    <td colname="col2"> <p>Una instancia de <span class="codeph"> Metadatos </span> , que puede contener información personalizada sobre el contenido que se va a cargar. </p> <p>Algunos ejemplos de contenido son contenido alternativo o publicitario para colocar dentro del contenido principal. Si utiliza publicidad, configure <span class="codeph"> AuditudeSettings </span>. Para obtener más información, consulte <a href="../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-insertion-metadata-set-up.md" format="dita" scope="local"> Metadatos del Ad Insertion </a>. </p> </td> 
    </tr> 
    </tbody> 
    </table>

   >[!IMPORTANT]
   >
   >TVSDK solo admite la reproducción de tipos de contenido específicos. Si intenta cargar cualquier otro tipo de contenido, TVSDK envía un evento de error.
   >
   >Para el contenido de MP4 vídeo bajo demanda (VOD), TVSDK no admite trucos, flujo de velocidad de bits adaptable (ABR), inserción de publicidad, subtítulos opcionales o DRM.

   El siguiente código crea un `MediaResource` instancia:

   ```java
   try { 
       // create a MediaResource instance pointing to some HLS content 
       Metadata metadata = //TODO: create metadata  
       MediaResource mediaResource = MediaResource.createFromUrl( 
         "https://www.example.com/video/some-video.m3u8",  
         MediaResource.Type.HLS,  
         metadata); 
   } catch(IllegalArgumentException ex) { 
       // this exception is thrown if the URL does not point  
       // to a valid url. 
   } 
   ```

   >[!TIP]
   >
   >En este punto, puede utilizar `MediaResource` descriptores de acceso (getters) para examinar el tipo, la dirección URL y los metadatos del recurso.

1. Cargue el recurso de medios mediante lo siguiente:

   * Su instancia de MediaPlayer.

      Para obtener más información, consulte [Cargar un recurso multimedia en MediaPlayer](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-resource-load.md).
   * A `MediaPlayerItemLoader` Para obtener más información, consulte [Cargar un recurso multimedia mediante MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).
   >[!IMPORTANT]
   >
   >No cargue el recurso multimedia en un subproceso en segundo plano. La mayoría de las operaciones de TVSDK deben ejecutarse en el subproceso principal, y ejecutarlas en un subproceso en segundo plano puede provocar que la operación genere un error y salga.
