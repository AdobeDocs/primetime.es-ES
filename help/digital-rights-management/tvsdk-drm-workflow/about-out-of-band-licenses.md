---
title: Información general sobre las licencias fuera de banda
description: Información general sobre las licencias fuera de banda
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---


# Licencias fuera de banda {#out-of-band-licenses}

Las licencias también se pueden obtener fuera de banda (sin ponerse en contacto con un servidor de licencias DRM de Primetime) almacenando la licencia en disco y en memoria utilizando el método `storeVoucher()`.

Para reproducir vídeos cifrados en Primetime, el tiempo de ejecución respectivo debe obtener la licencia para ese vídeo. La licencia contiene la clave de descifrado del vídeo y la genera el servidor de licencias DRM de Primetime que el cliente ha implementado.

El motor de ejecución generalmente obtiene esta licencia enviando una solicitud de licencia al servidor de licencias DRM de Primetime indicado en los metadatos DRM del vídeo (clase `DRMContentData`). La aplicación puede almacenar en déclencheur esta solicitud de licencia llamando al método `DRMManager.loadVoucher()` .

`DRMManager.storeVoucher()` permite que la solicitud envíe licencias que haya obtenido fuera de banda. El motor de ejecución puede omitir el proceso de solicitud de licencia y utilizar las licencias reenviadas para reproducir vídeos cifrados. El servidor de licencias de Primetime DRM aún debe generar la licencia para poder obtenerla fuera de banda. Sin embargo, tiene la opción de alojar las licencias en cualquier servidor HTTP, en lugar de en un servidor de licencias DRM de Primetime.

`DRMManager.storeVoucher()` también se utiliza para admitir el uso compartido de licencias entre varios dispositivos. Después de Primetime DRM 3.0, esta función se denomina &quot;Compatibilidad con dominios del dispositivo&quot;. Si la implementación admite este caso de uso, puede registrar varios equipos en un grupo de dispositivos mediante el método `DRMManager.addToDeviceGroup()`. Si hay un equipo con una licencia válida enlazada al dominio para un contenido determinado, la aplicación puede extraer la licencia serializada mediante el método `DRMVoucher.toByteArray()` y en el resto de equipos puede importar las licencias mediante el método `DRMManager.storeVoucher()`.

## Acerca del registro de dispositivos {#about-device-registration}

Todas las licencias de DRM de Primetime, en el momento de la creación, deben enlazarse a una entidad final. El enlace es el proceso criptográfico que permite que una entidad específica pueda consumir la licencia. Esto es necesario para evitar &quot;licencias flotantes&quot; que pueden ser utilizadas por cualquier dispositivo arbitrario. Para que Primetime DRM &quot;pregenere&quot; licencias, esto significa que el &quot;objetivo&quot; de estas licencias pregeneradas debe ser conocido con antelación. Primetime DRM se refiere a esto como &quot;Registro de dispositivos&quot;.

## Registrar un dispositivo {#register-a-device}

Supongamos que ha realizado las siguientes tareas:

* Ha configurado el SDK de servidor de DRM de Primetime.
* Ha configurado un servidor HTTP para emitir licencias pregeneradas.
* Ha creado una aplicación Primetime para ver el contenido protegido.

 La fase de registro del dispositivo incluye las siguientes acciones:

1. La aplicación crea un ID generado aleatoriamente.
1. La aplicación invoca el método `DRMManager.authenticate()`. La aplicación debe incluir el ID generado aleatoriamente en la solicitud de autenticación. Por ejemplo, incluya el ID en el campo de nombre de usuario.
1. La acción mencionada en el paso 2 dará como resultado que el DRM de Primetime envíe una solicitud de autenticación al servidor del cliente. Esta solicitud incluye el certificado del dispositivo:
   1. El servidor extrae el certificado del dispositivo y el ID generado de la solicitud y almacena.
   1. El subsistema de cliente genera previamente licencias para este certificado de dispositivo, las almacena y concede acceso a ellas de forma que se asocian con el ID generado. .
1. El servidor responde a la solicitud con un mensaje de &quot;éxito&quot;.
1. La aplicación almacena el ID generado.

Después del registro del dispositivo, la aplicación utiliza el ID generado del mismo modo que habría utilizado el ID del dispositivo en el esquema anterior:
1. La aplicación intentará localizar el ID generado.
1. Si se encuentra el ID generado, la aplicación utilizará el ID generado al descargar las licencias pregeneradas. La aplicación enviará las licencias al cliente de DRM de Primetime para su consumo mediante el método `DRMManager.storeVoucher()`. .
1. Si no se encuentra el ID generado, la aplicación pasará por el procedimiento de registro del dispositivo.

## Restablecimiento de fábrica de DRM {#drm-factory-reset}

Cuando el usuario del dispositivo invoque la opción de restablecimiento de fábrica de DRM, el certificado del dispositivo se depurará. Para continuar reproduciendo el contenido protegido, la aplicación debe volver a pasar por el procedimiento de registro del dispositivo. Si la aplicación envía una licencia pregenerada obsoleta, el cliente de DRM de Primetime la rechazará, ya que la licencia se cifró para un ID de dispositivo antiguo.

* API de Flash: [DRMManager.resetDRMVouchers()](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html#resetDRMVouchers()) - (solo se puede llamar en respuesta a ciertos códigos de error DRM no recuperables).
* API de iOS: [DRMManager resetDRM](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a0dd6c9662428583196e0419d3ea69446)
* API de Android: [DRMManager.resetDRM()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#resetDRM(com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))