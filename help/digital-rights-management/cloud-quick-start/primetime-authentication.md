---
title: Autenticación de Adobe Primetime (opcional)
description: Autenticación de Adobe Primetime (opcional)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Autenticación de Adobe Primetime (opcional) {#adobe-primetime-authentication-optional}

Si la directiva DRM que se utiliza para empaquetar el contenido es una directiva anónima, se emitirá una licencia a todas las solicitudes de licencia. De forma opcional, Primetime Cloud DRM también admite la autenticación mediante autenticación de Adobe Primetime. Si esta función está habilitada, no se emitirá una licencia a menos que el dispositivo cliente haya adquirido primero un token de autenticación de Primetime y lo establezca localmente mediante la API de cliente adecuada ( `setAuthenticationToken`) para configurar tokens de autenticación personalizados. Para obtener más información sobre la integración de la autenticación de Primetime en el flujo de trabajo de autenticación, consulte: [Autenticación de Adobe Primetime.](https://tve.helpdocsonline.com/home)

Durante la adquisición de la licencia, si la política de DRM indica que se requiere autenticación de tiempo de ejecución de Primetime, el servidor de licencias analizará y validará el token de medios corto de autenticación de Primetime. Si la política de DRM especifica un `ResourceID` o `RequestorID`, el servidor de licencias también validará el token con estas propiedades. Si no se establecen, el servidor de licencias especificará las propiedades como &quot;null&quot; durante la validación del token. Solo si la validación del token se realiza correctamente, se emitirá una licencia; de lo contrario, el cliente enviará un DRMErrorEvent 3328 con un código de suberror 305 (usuario no autorizado).

Los parámetros de autenticación de Primetime deben especificarse en la directiva utilizada para empaquetar el contenido que se va a requerir para la autenticación de Primetime.

Las propiedades relevantes son:

```
#policy.customProp.1=adobePass.required=<TRUE or FALSE> 
#policy.customProp.1=adobePass.requestorID=<Requestor ID String> 
#policy.customProp.1=adobePass.resourceID=<Resource ID String>
```

>[!NOTE]
>
>Cuando utilice la autenticación de Primetime junto con la función de rotación de licencias (DRM), tenga en cuenta que el token de medios cortos (SMT) de autenticación de Primetime tiene una fecha de validez corta. Si su aplicación planea utilizar la rotación de licencias (p. ej., para admitir la *Interrupciones* caso de uso), la aplicación debe tener en cuenta esto y actualizar su token de medio corto de autenticación de Primetime antes de rotar su licencia.
