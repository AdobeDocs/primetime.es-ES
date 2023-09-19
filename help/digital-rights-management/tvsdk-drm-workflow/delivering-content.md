---
title: Entrega de contenido
description: Entrega de contenido
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# Entrega de contenido {#delivering-content}

Primetime DRM no es compatible con el mecanismo de entrega de contenido, ya que el tiempo de ejecución abstrae la capa de red y simplemente proporciona el contenido protegido al subsistema Primetime DRM. Por lo tanto, el contenido se puede entregar a través de HTTP, HTTP Dynamic Streaming, RTMP o RTMPE, HLS, etc.

Sin embargo, según el protocolo, puede haber dificultades para recuperar los metadatos del contenido protegido ( `DRMContentData` - normalmente en forma de carga lateral [!DNL .metadata] file). Estos metadatos DRM son necesarios para llamar a cualquier `DRMManager` API, como recuperar previamente la licencia, autenticar DRM o unirse a un dominio de dispositivo. Por ejemplo, con el protocolo RTMP/RTMPE, solo se pueden entregar al cliente datos FLV y F4V a través del Flash Media Server (FMS). Debido a esto, el cliente debe recuperar el blob de metadatos de otras maneras. Una opción para resolver este problema es alojar los metadatos en un servidor web HTTP e implementar el reproductor de vídeo del cliente para recuperar los metadatos adecuados, según el contenido que se esté reproduciendo.

```
private function getMetadata():void { 
    extrapolated-path-to-metadata = "https://metadatas.mywebserver.com/" + videoname; 
     var urlRequest : URLRequest =  
      new URLRequest(extrapolated-path-to-the-metadata + ".metadata");  
    var urlStream : URLStream = new URLStream();  
    urlStream.addEventListener(Event.COMPLETE, handleMetadata);  
    urlStream.addEventListener(IOErrorEvent.NETWORK_ERROR, handleIOError);  
    urlStream.addEventListener(IOErrorEvent.IO_ERROR, handleIOError);  
    urlStream.addEventListener(IOErrorEvent.VERIFY_ERROR, handleIOError);  
 
    try { 
        urlStream.load(urlRequest);  
    } catch(se:SecurityError) { 
        videoLog.text += se.toString() + "\n";  
    } catch(e:Error) { 
        videoLog.text += e.toString() + "\n";  
    } 
} 
```
