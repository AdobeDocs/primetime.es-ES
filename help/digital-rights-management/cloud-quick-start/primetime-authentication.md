---
seo-title: Autenticación de Adobe Primetime (opcional)
title: Autenticación de Adobe Primetime (opcional)
uuid: fa6225d6-e0e5-4fcc-ac26-4ff54f9f334a
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---


# Autenticación de Adobe Primetime (opcional) {#adobe-primetime-authentication-optional}

Si la política de DRM que se utiliza para empaquetar el contenido es una política anónima, se emitirá una licencia para todas las solicitudes de licencia. Opcionalmente, Primetime Cloud DRM también admite la autenticación mediante la autenticación de Adobe Primetime. Si esta función está habilitada, no se emitirá una licencia a menos que el dispositivo cliente haya adquirido primero un autentificador Primetime y lo haya establecido localmente mediante la API de cliente adecuada ( `setAuthenticationToken`) para configurar los autentificadores de autenticación personalizados. Para obtener más información sobre la integración de la autenticación Primetime en el flujo de trabajo de autenticación, consulte: [Autenticación de Adobe Primetime.](https://tve.helpdocsonline.com/home)

Durante la adquisición de licencias, si la directiva DRM establece que se requiere autenticación de tiempo de impresión, el servidor de licencias analizará y validará el autentificador de medios cortos de autenticación Primetime. Si la directiva DRM especifica `ResourceID` o `RequestorID`, el servidor de licencias también validará el token con estas propiedades. Si no se establecen, el servidor de licencias especificará las propiedades como &quot;null&quot; durante la validación del token. Sólo se expedirá una licencia si la validación del token se realiza correctamente; de lo contrario, el cliente enviará un evento 3328 DRMErrorEvent con un subcódigo de error 305 (Usuario no autorizado).

Los parámetros de autenticación Primetime deben especificarse en la directiva utilizada para empaquetar el contenido destinado a requerir autenticación Primetime.

Las propiedades relevantes son:

```
#policy.customProp.1=adobePass.required=<TRUE or FALSE> 
#policy.customProp.1=adobePass.requestorID=<Requestor ID String> 
#policy.customProp.1=adobePass.resourceID=<Resource ID String>
```

>[!NOTE]
>
>Al utilizar la autenticación Primetime junto con la función de rotación de licencias (DRM), tenga en cuenta que el autentificador de medios cortos de autenticación Primetime (SMT) tiene una fecha de validez corta. Si la aplicación planea utilizar la Rotación de licencia (por ejemplo, para admitir el caso de uso *Apagones*), la aplicación debe tener esto en cuenta y actualizar su autentificación Primetime Short Media Token antes de rotar su licencia.