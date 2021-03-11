---
title: Lista de permitidos de la aplicación SWF
description: Lista de permitidos de la aplicación SWF
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Lista de permitidos de la aplicación SWF {#swf-application-allowlisting}

Para la lista de permitidos de una aplicación SWF, puede seguir una de estas dos estrategias:

* Puede especificar una URL para un SWF. Se trata de un enfoque muy flexible, especialmente en un entorno de desarrollo en el que se está reconstruyendo el SWF con regularidad.
* Puede especificar un HASH SWF. Este es un valor de compendio criptográfico de su SWF. Este enfoque es menos flexible (pero mucho más estricto), ya que el SWF HASH cambiará cuando la aplicación cambie y se vuelva a crear. En esta situación, todo el contenido enlazado al HASH anterior no se reproducirá en el nuevo reproductor y tendrá que ser reempaquetado. La herramienta [!DNL PolicyManager.jar] calculará automáticamente el hash si especifica un archivo [!DNL .swf].

   Por otro lado, si utiliza Primetime DRM a través de Flash/Adobe Medium Server (FMS/AMS), puede proporcionar la ruta a sus SWF concretos y FMS/AMS realizará un hash automático de los SWF para que los inserte en la directiva DRM que se utiliza para empaquetar el contenido transmitido por FMS/AMS.

Consulte `policy.allowedSWFApplication.n` en *Propiedades de configuración* para obtener más información.
