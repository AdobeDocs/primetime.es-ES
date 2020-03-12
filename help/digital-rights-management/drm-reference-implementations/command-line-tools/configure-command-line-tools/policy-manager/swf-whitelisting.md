---
seo-title: Lista blanca de aplicaciones SWF
title: Lista blanca de aplicaciones SWF
uuid: e3021ae9-54f4-4bcf-a274-515ae765f74b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Lista blanca de aplicaciones SWF{#swf-application-whitelisting}

Para incluir una aplicación SWF en la lista blanca, puede seguir una de estas dos estrategias:

* Puede especificar una URL para un SWF. Se trata de un enfoque muy flexible, especialmente en un entorno de desarrollo en el que se está reconstruyendo el SWF con regularidad.
* Puede especificar un HASH SWF. Es un valor de compendio criptográfico del SWF. Este enfoque es menos flexible (pero mucho más estricto), ya que el HASH SWF cambiará cuando la aplicación cambie y se vuelva a crear. En esta situación, todo el contenido enlazado al HASH anterior no se reproducirá en el nuevo reproductor y tendrá que ser reempaquetado. La [!DNL PolicyManager.jar] herramienta calculará automáticamente el hash si especifica un [!DNL .swf] archivo.

   Por otro lado, si utiliza Primetime DRM a través de Flash/Adobe Media Server (FMS/AMS), puede proporcionar la ruta a sus archivos SWF concretos y FMS/AMS realizará un hash automático de los archivos SWF para que los inserte en la directiva DRM que se utiliza para empaquetar el contenido transmitido por FMS/AMS.

Consulte `policy.allowedSWFApplication.n` en Propiedades ** de configuración para obtener más información.
