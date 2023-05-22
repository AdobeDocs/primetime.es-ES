---
title: Información general sobre las licencias fuera de banda
description: Información general sobre las licencias fuera de banda
copied-description: true
exl-id: 31a9f097-74e8-41d0-9b9a-1c2a08d3e63a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# Licencias fuera de banda {#out-of-band-licenses}

Las licencias también se pueden obtener fuera de banda (sin ponerse en contacto con un servidor de licencias DRM de Primetime) almacenando la licencia en disco y en memoria utilizando `storeVoucher()` método.

Para reproducir vídeos cifrados en Primetime, el tiempo de ejecución correspondiente debe obtener la licencia de ese vídeo. La licencia contiene la clave de descifrado del vídeo y la genera el servidor de licencias DRM de Primetime que ha implementado el cliente.

Por lo general, el motor en tiempo de ejecución de obtiene esta licencia enviando una solicitud de licencia al servidor de licencias DRM de Primetime indicado en los metadatos DRM del vídeo ( `DRMContentData` class). La aplicación puede almacenar en déclencheur esta solicitud de licencia llamando a `DRMManager.loadVoucher()` método.

`DRMManager.storeVoucher()` permite que la aplicación envíe licencias que haya obtenido fuera de banda. El tiempo de ejecución puede omitir el proceso de solicitud de licencia y utilizar las licencias reenviadas para reproducir vídeos cifrados. El servidor de licencias DRM de Primetime aún debe generar la licencia para poder obtenerla fuera de banda. Sin embargo, tiene la opción de alojar las licencias en cualquier servidor HTTP, en lugar de en un servidor de licencias DRM de Primetime.

`DRMManager.storeVoucher()` también se utiliza para admitir el uso compartido de licencias entre varios dispositivos. Después de Primetime DRM 3.0, esta función se denomina &quot;Compatibilidad con dominio de dispositivo&quot;. Si su implementación admite este caso de uso, puede registrar varios equipos en un grupo de dispositivos mediante el `DRMManager.addToDeviceGroup()` método. Si hay un equipo con una licencia enlazada al dominio válida para un contenido determinado, la aplicación puede extraer la licencia serializada mediante `DRMVoucher.toByteArray()` y en sus otros equipos puede importar las licencias utilizando el `DRMManager.storeVoucher()` método.

## Acerca del registro de dispositivos {#about-device-registration}

Todas las licencias DRM de Primetime, en el momento de la creación, deben estar enlazadas a una entidad final. El enlace es el proceso criptográfico de permitir solo a una entidad específica la capacidad de consumir la licencia. Esto es necesario para evitar &quot;licencias flotantes&quot; que pueden ser utilizadas por cualquier dispositivo arbitrario. Para que Primetime DRM &quot;genere previamente&quot; licencias, esto significa que el &quot;objetivo&quot; de estas licencias generadas previamente debe conocerse con antelación. Primetime DRM se refiere a esto como &quot;Registro de dispositivos&quot;.

## Registrar un dispositivo {#register-a-device}

Supongamos que ha realizado las siguientes tareas:

* Ha configurado el SDK del servidor DRM de Primetime.
* Ha configurado un servidor HTTP para emitir licencias generadas previamente.
* Ha creado una aplicación de Primetime para ver el contenido protegido.

 La fase de registro del dispositivo incluye las siguientes acciones:

1. La aplicación crea un ID generado aleatoriamente.
1. La aplicación invoca el `DRMManager.authenticate()` método. La aplicación debe incluir el ID generado aleatoriamente en la solicitud de autenticación. Por ejemplo, incluya el ID en el campo de nombre de usuario.
1. La acción mencionada en el paso 2 hará que Primetime DRM envíe una solicitud de autenticación al servidor del cliente. Esta solicitud incluye el certificado del dispositivo:
   1. El servidor extrae el certificado del dispositivo y el ID generado de la solicitud y almacena.
   1. El subsistema de cliente genera previamente licencias para este certificado de dispositivo, las almacena y concede acceso a ellas de forma que se asocien al ID generado. .
1. El servidor responde a la solicitud con un mensaje de éxito.
1. La aplicación almacena el ID generado.

Después del registro del dispositivo, la aplicación utiliza el ID generado del mismo modo que habría utilizado el ID del dispositivo en el esquema anterior:
1. La aplicación intentará localizar el ID generado.
1. Si se encuentra el ID generado, la aplicación utilizará el ID generado al descargar las licencias generadas previamente. La aplicación enviará las licencias al cliente DRM de Primetime para su consumo mediante el `DRMManager.storeVoucher()` método. .
1. Si no se encuentra el ID generado, la aplicación pasará por el procedimiento de registro del dispositivo.

## Restablecimiento de fábrica de DRM {#drm-factory-reset}

Cuando el usuario del dispositivo invoca la opción de restablecimiento de fábrica de DRM, el certificado del dispositivo se depura. Para seguir reproduciendo el contenido protegido, la aplicación debe volver a pasar por el procedimiento de registro del dispositivo. Si la aplicación envía una licencia pregenerada obsoleta, el cliente de DRM de Primetime la rechazará, ya que la licencia se cifró para un ID de dispositivo anterior.

* API DE Flash: [DRManager.resetDRMVouchers()](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html#resetDRMVouchers()) : (solo se puede llamar en respuesta a ciertos códigos de error DRM no recuperables).
* API de iOS: [DRManager resetDRM](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a0dd6c9662428583196e0419d3ea69446)
* API de Android: [DRManager.resetDRM()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#resetDRM(com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))
