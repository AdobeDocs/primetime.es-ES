---
title: Listado de aplicaciones permitidas para SWF
description: Listado de aplicaciones permitidas para SWF
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Listado de aplicaciones permitidas para SWF {#swf-application-allowlisting}

Para realizar la lista de permitidos de una aplicación de SWF, puede seguir una de estas dos estrategias:

* Puede especificar una dirección URL para un SWF. Se trata de un enfoque muy flexible, especialmente en un entorno de desarrollo en el que reconstruye a su SWF regularmente.
* Puede especificar un HASH de SWF. Es un valor de resumen criptográfico del SWF. Este enfoque es menos flexible (pero mucho más estricto), ya que el HASH del SWF cambiará cuando la aplicación cambie y se reconstruya. En esta situación, todo el contenido enlazado al HASH anterior no se reproducirá en el nuevo reproductor y deberá volver a empaquetarse. El [!DNL PolicyManager.jar] La herramienta calculará automáticamente el hash si especifica un [!DNL .swf] archivo.

  Por otro lado, si está utilizando Primetime DRM mediante Flash/Adobe Media Server (FMS/AMS), puede proporcionar la ruta a sus SWF particulares, y FMS/AMS hará un hash automático de los SWF para que los inserte en la política de DRM que se utiliza para empaquetar el contenido transmitido por FMS/AMS.

Consulte `policy.allowedSWFApplication.n` in *Propiedades de configuración* para obtener más información.
