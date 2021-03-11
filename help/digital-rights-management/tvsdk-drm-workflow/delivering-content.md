---
title: Entrega de contenido
description: Entrega de contenido
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# Entrega de contenido {#delivering-content}

Primetime DRM no tiene en cuenta el mecanismo de entrega del contenido, ya que el tiempo de ejecución abstrae la capa de red y simplemente proporciona el contenido protegido al subsistema Primetime DRM. Por lo tanto, el contenido se puede entregar a través de HTTP, HTTP Dynamic Streaming, RTMP, RTMPE, HLS, etc.

Sin embargo, según el protocolo, puede haber complejidades relacionadas con la recuperación de los metadatos del contenido protegido ( `DRMContentData` - normalmente en forma de archivo [!DNL .metadata] cargado de forma lateral). Estos metadatos DRM son necesarios para llamar a cualquier API `DRMManager`, como la recuperación previa de la licencia, la autenticación DRM o la unión a un dominio del dispositivo. Por ejemplo, con el protocolo RTMP/RTMPE, solo se pueden enviar datos FLV y F4V al cliente a través del Flash Media Server (FMS). Debido a esto, el cliente debe recuperar el blob de metadatos de otras maneras. Una opción para resolver este problema es alojar los metadatos en un servidor web HTTP e implementar el reproductor de vídeo cliente para recuperar los metadatos adecuados, según el contenido que se esté reproduciendo.

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

