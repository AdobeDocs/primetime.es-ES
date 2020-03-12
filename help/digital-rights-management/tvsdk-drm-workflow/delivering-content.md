---
seo-title: Distribución de contenido
title: Distribución de contenido
uuid: b277d369-fee3-4a20-9dd8-27b3a8a82a9e
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Distribución de contenido {#delivering-content}

Primetime DRM es independiente del mecanismo de entrega del contenido, ya que el motor de ejecución abstrae la capa de red y simplemente proporciona el contenido protegido al subsistema Primetime DRM. Por lo tanto, el contenido se puede entregar a través de HTTP, HTTP Dynamic Streaming, RTMP, RTMPE, HLS, etc.

Sin embargo, en función del protocolo, puede haber complicaciones en la recuperación de los metadatos del contenido protegido ( `DRMContentData` normalmente en forma de [!DNL .metadata] archivo cargado en paralelo). Estos metadatos DRM son necesarios para llamar a cualquier `DRMManager` API, como recuperar previamente la licencia, la autenticación DRM o unirse a un dominio de dispositivo. Por ejemplo, con el protocolo RTMP/RTMPE, solo se pueden entregar datos FLV y F4V al cliente a través de Flash Media Server (FMS). Debido a esto, el cliente debe recuperar el blob de metadatos de otras formas. Una opción para resolver este problema es alojar los metadatos en un servidor web HTTP e implementar el reproductor de vídeo del cliente para recuperar los metadatos adecuados, en función del contenido que se esté reproduciendo.

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

