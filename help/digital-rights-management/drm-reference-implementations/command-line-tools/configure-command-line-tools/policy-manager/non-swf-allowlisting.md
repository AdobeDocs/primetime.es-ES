---
seo-title: Lista de permitidos para aplicaciones que no son SWF
title: Lista de permitidos para aplicaciones que no son SWF
uuid: d4f93b15-e556-4749-95ab-f7f58b1061d7
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# Lista de permitidos para aplicaciones que no son SWF {#non-swf-application-isting}

AIR fue la primera plataforma en la que la aplicación destacada permite la inclusión en la lista y el nombre de la propiedad que se utiliza para la lista de permitidos de aplicaciones que no son SWF (Adobe AIR, iOS, Android, etc.) conserva su nombre original: `policy.allowedAIRApplication.n`. Esto permite que el contenido se reproduzca en todas las aplicaciones que no sean Flash y que estén firmadas con un certificado de firma antes de la publicación. Esto se denomina *ID de aplicación*. Puede extraer el ID de aplicación utilizando la [!DNL AdobePublisherIDUtility.jar] herramienta. Este listado permitido se aplicará en cualquier cliente que admita Primetime DRM.

El ID de aplicación se deriva de la clave pública del certificado de firma utilizado para firmar una aplicación concreta. Si la clave pública del certificado caduca alguna vez, el contenido anterior solo se podrá reproducir en las aplicaciones firmadas con el certificado antiguo no se reproducirá en la nueva aplicación (firmada con el nuevo certificado).

Si se encuentra en una situación en la que tiene una biblioteca de contenido que permite la lista de aplicaciones que se firmaron con un certificado de firma determinado, ese certificado caduca y se le emite un nuevo certificado (con un par de claves público/privado diferente), el contenido antiguo no se reproducirá en la nueva aplicación *a menos* que realice una de las siguientes acciones:

* Utilice un `PolicyUpdateList` en el servidor de licencias para anular la directiva entrante e insertar una nueva entrada de Lista de permitidos de aplicación con el compendio del nuevo certificado de firma.
* Actualice la lógica del servidor de licencias para anular la directiva entrante e insertar una nueva entrada de Lista de permitidos de aplicación.
* Solicite que el emisor del certificado de firma le emita un nuevo certificado que utilice el mismo par de claves público/privado que el certificado anterior.
* Si va a entregar contenido HDS/HLS que hace referencia a un extremo de URL para recuperar el `DRMMetadata`, puede volver a generar el `DRMMetadata` (utilizando el SDK de Java de DRM Primetime) para insertar una nueva directiva DRM que contenga una entrada de Lista de permitidos de aplicación actualizada.

* Vuelva a empaquetar todo el contenido antiguo con una nueva directiva DRM que tenga el compendio del nuevo certificado de firma.

Consulte `policy.allowedAIRApplication.n` en Propiedades ** de configuración para obtener más información.

>[!NOTE]
>
>Permitir que la lista de una aplicación de iOS requiere un enfoque especial. Consulte [Lista de permitidos de la aplicación](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) iOS en la Guía *del programador de* TVSDK para iOS.
