---
title: Lista de permitidos de aplicaciones que no son SWF
description: Lista de permitidos de aplicaciones que no son SWF
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# Lista de permitidos de aplicaciones que no son SWF {#non-swf-application-isting}

AIR fue la primera plataforma en la que se incluían listas de permitidos de aplicaciones y el nombre de la propiedad que se utiliza para la lista de permitidos de aplicaciones que no son SWF (Adobe AIR, iOS, Android, etc.) conserva su nombre original: `policy.allowedAIRApplication.n`. Esto permite que todas las aplicaciones que no sean de Flash y que estén firmadas con un certificado de firma antes de la publicación puedan reproducir el contenido. Esto se conoce como *ID de aplicación*. Puede extraer el ID de la aplicación utilizando la herramienta [!DNL AdobePublisherIDUtility.jar]. Esta lista de permitidos se aplicará a cualquier cliente que admita Primetime DRM.

El ID de aplicación se deriva de la clave pública del certificado de firma utilizado para firmar una aplicación determinada. Si la clave pública del certificado caduca en algún momento, todo el contenido anterior permitido que aparezca solo en aplicaciones firmadas con el certificado antiguo no se reproducirá en la nueva aplicación (firmada con el nuevo certificado).

Si se encuentra en una situación en la que tiene una biblioteca de contenido permitida en la lista de aplicaciones que fueron firmadas con un certificado de firma determinado, y ese certificado caduca y se le emite un nuevo certificado (con un par de claves pública y privada diferente), el contenido antiguo no se reproducirá en la nueva aplicación *a menos que* realice una de las siguientes acciones:

* Utilice un `PolicyUpdateList` en el servidor de licencias para anular la directiva entrante e insertar una nueva entrada de Lista de permitidos de aplicación con el compendio del nuevo certificado de firma .
* Actualice la lógica del servidor de licencias para anular la directiva entrante e insertar una nueva entrada de Lista de permitidos de aplicación.
* Solicite que el emisor del certificado de firma le emita un nuevo certificado que utilice el mismo par de claves pública y privada que el certificado anterior.
* Si está entregando contenido HDS/HLS que hace referencia a un extremo de URL para recuperar el `DRMMetadata`, puede volver a generar el `DRMMetadata` (utilizando el SDK de Java de DRM de Primetime) para insertar una nueva directiva DRM que contenga una entrada de Lista de permitidos de aplicación actualizada.

* Vuelva a empaquetar todo el contenido antiguo con una nueva directiva DRM que tenga el resumen del nuevo certificado de firma.

Consulte `policy.allowedAIRApplication.n` en *Propiedades de configuración* para obtener más información.

>[!NOTE]
>
>Para permitir que aparezca una aplicación de iOS es necesario un enfoque especial. Consulte [Lista de permitidos de la aplicación de iOS](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) en la *Guía del programador de TVSDK para iOS*.
