---
title: Autenticación de Adobe Primetime (opcional)
description: Autenticación de Adobe Primetime (opcional)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---


# Autenticación de Adobe Primetime (opcional) {#adobe-primetime-authentication-optional}

Si la política de DRM que se utiliza para empaquetar el contenido es una política anónima, se emitirá una licencia para todas las solicitudes de licencia. De forma opcional, el DRM de Primetime Cloud también admite la autenticación mediante la autenticación de Adobe Primetime. Si esta función está habilitada, no se emitirá una licencia a menos que el dispositivo cliente haya adquirido primero un token de autenticación de Primetime y lo haya establecido localmente a través de la API del cliente adecuada ( `setAuthenticationToken`) para configurar tokens de autenticación personalizados. Para obtener más información sobre la integración de la autenticación de Primetime en el flujo de trabajo de autenticación, consulte: [Autenticación de Adobe Primetime.](https://tve.helpdocsonline.com/home)

Durante la adquisición de licencias, si la directiva DRM indica que se requiere autenticación de tiempo de uso de PRI, el servidor de licencias analizará y validará el token de medios cortos de autenticación de Primetime. Si la directiva DRM especifica `ResourceID` o `RequestorID`, el servidor de licencias también validará el token con estas propiedades. Si no se establecen, el servidor de licencias especificará las propiedades como &quot;null&quot; durante la validación del token. Solo se expedirá una licencia si la validación del token se realiza correctamente; de lo contrario, el cliente enviará un 3328 DRMErrorEvent con un subcódigo de error 305 (usuario no autorizado).

Los parámetros de autenticación de Primetime deben especificarse en la directiva utilizada para empaquetar el contenido que está destinado a requerir autenticación de Primetime.

Las propiedades relevantes son:

```
#policy.customProp.1=adobePass.required=<TRUE or FALSE> 
#policy.customProp.1=adobePass.requestorID=<Requestor ID String> 
#policy.customProp.1=adobePass.resourceID=<Resource ID String>
```

>[!NOTE]
>
>Cuando utilice la autenticación de Primetime junto con la función de rotación de licencias (DRM), tenga en cuenta que el testigo de medios cortos de autenticación de Primetime (SMT) tiene una fecha de validez corta. Si la aplicación planea utilizar la rotación de la licencia (por ejemplo, para admitir el caso de uso *Blackouts*), la aplicación debe tener esto en cuenta y actualizar su token de medios corto de autenticación de Primetime antes de rotar su licencia.