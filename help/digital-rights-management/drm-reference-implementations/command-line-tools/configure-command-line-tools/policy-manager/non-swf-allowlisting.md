---
title: Lista de aplicaciones no SWF permitidas
description: Lista de aplicaciones no SWF permitidas
copied-description: true
exl-id: f33fb0e9-144f-49f8-8da2-8a50aea09456
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Lista de aplicaciones no SWF permitidas {#non-swf-application-isting}

AIR fue la primera plataforma en incluir aplicaciones en la lista de permitidos y el nombre de la propiedad que usa para listas de permitidos aplicaciones que no son de SWF (Adobe AIR, iOS, Android, etc.) conserva su nombre original: `policy.allowedAIRApplication.n`. Esto permite que el contenido se reproduzca en todas las aplicaciones que no sean de Flash y que estén firmadas con un certificado de firma antes de la publicación. Esto se conoce como *ID de aplicación*. Puede extraer el ID de aplicación mediante el complemento [!DNL AdobePublisherIDUtility.jar] herramienta. Esta lista de permitidos se aplicará a cualquier cliente que admita DRM de Primetime.

El identificador de aplicación se deriva de la clave pública del certificado de firma utilizado para firmar una aplicación determinada. Si la clave pública del certificado caduca alguna vez, todos los contenidos anteriores permitidos para reproducir solo en aplicaciones firmadas con el certificado antiguo no se reproducirán en la aplicación nueva (firmada con el certificado nuevo).

Si se encuentra en una situación en la que tiene una biblioteca de contenido permitida para aplicaciones firmadas con un certificado de firma en particular y ese certificado caduca y se le emite un nuevo certificado (con un par de claves pública y privada diferente), el contenido antiguo no se reproducirá en la nueva aplicación *a menos* realice cualquiera de las siguientes acciones:

* Utilice un `PolicyUpdateList` en el servidor de licencias para anular la directiva entrante e insertar una nueva entrada de Lista de permitidos de aplicación con el resumen del nuevo certificado de firma
* Actualice la lógica del servidor de licencias para anular la directiva entrante e insertar una nueva entrada de Lista de permitidos de aplicación.
* Solicite que el emisor del certificado de firma le emita un nuevo certificado que utilice el mismo par de claves pública y privada que utilizó el certificado anterior.
* Si entrega contenido HDS/HLS que hace referencia a un punto final de URL para recuperar la `DRMMetadata`, puede regenerar el `DRMMetadata` (con el SDK de Java de DRM de Primetime) para insertar una nueva directiva DRM que contenga una entrada de Lista de permitidos de aplicación actualizada.

* Vuelva a empaquetar todo el contenido antiguo con una nueva directiva DRM que tenga el resumen del nuevo certificado de firma.

Consulte `policy.allowedAIRApplication.n` in *Propiedades de configuración* para obtener más información.

>[!NOTE]
>
>Permitir la inclusión en la lista de una aplicación de iOS requiere un enfoque especial. Consulte [Lista de permitidos de la aplicación de iOS](../../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) en el *Guía del programador de TVSDK para iOS*.
