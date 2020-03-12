---
seo-title: Lista blanca de aplicaciones que no son SWF
title: Lista blanca de aplicaciones que no son SWF
uuid: d4f93b15-e556-4749-95ab-f7f58b1061d7
translation-type: tm+mt
source-git-commit: a63768e51c911914a6ba9d884e2587fa34939f9d

---


# Lista blanca de aplicaciones que no son SWF {#non-swf-application-whitelisting}

AIR fue la primera plataforma que presentó la lista de aplicaciones permitidas y el nombre de la propiedad que se utiliza para incluir en la lista blanca aplicaciones que no son SWF (Adobe AIR, iOS, Android, etc.) conserva su nombre original: `policy.allowedAIRApplication.n`. Esto permite que el contenido se reproduzca en todas las aplicaciones que no sean Flash y que estén firmadas con un certificado de firma antes de la publicación. Esto se conoce como ID *de aplicación*. Puede extraer el ID de aplicación mediante la [!DNL AdobePublisherIDUtility.jar] herramienta. Esta lista blanca se aplicará a cualquier cliente que admita Primetime DRM.

El ID de la aplicación se deriva de la clave pública del certificado de firma utilizado para firmar una aplicación concreta. Si la clave pública del certificado caduca alguna vez, todo el contenido anterior en la lista blanca que se reproduzca únicamente en las aplicaciones firmadas con el certificado antiguo no se reproducirá en la nueva aplicación (firmado con el nuevo certificado).

Si se encuentra en una situación en la que tiene una biblioteca de contenido en la lista de elementos permitidos en aplicaciones que se firmaron con un certificado de firma concreto, dicho certificado caduca y se le emite un nuevo certificado (con un par de claves público/privado diferente), el contenido antiguo no se reproducirá en la nueva aplicación *a menos* que realice una de las siguientes acciones:

* Utilice un `PolicyUpdateList` en el servidor de licencias para anular la directiva entrante e insertar una nueva entrada de la lista blanca de aplicaciones con el compendio del nuevo certificado de firma.
* Actualice la lógica del servidor de licencias para anular la directiva entrante e insertar una nueva entrada de lista blanca de aplicaciones.
* Solicite que el emisor del certificado de firma le emita un nuevo certificado que utilice el mismo par de claves público/privado que el certificado anterior.
* Si va a entregar contenido HDS/HLS que hace referencia a un extremo de URL para recuperar el `DRMMetadata`, puede volver a generar el `DRMMetadata` (utilizando el SDK de Java de DRM Primetime) para insertar una nueva directiva DRM que contenga una entrada de lista blanca de aplicaciones actualizada.

* Vuelva a empaquetar todo el contenido antiguo con una nueva directiva DRM que tenga el compendio del nuevo certificado de firma.

Consulte `policy.allowedAIRApplication.n` en Propiedades ** de configuración para obtener más información.

>[!NOTE]
>
>La lista blanca de aplicaciones de iOS requiere un enfoque especial. Consulte [Lista blanca de la aplicación](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-whitelist-your-ios-application.md) iOS en la Guía *del programador de* TVSDK para iOS.