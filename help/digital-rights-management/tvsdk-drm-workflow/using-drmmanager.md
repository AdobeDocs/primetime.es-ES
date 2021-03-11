---
title: Información general sobre el uso de la clase DRMManager
description: Información general sobre el uso de la clase DRMManager
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# Uso de la clase DRMManager {#using-the-drmmanager-class}

Utilice la clase `DRMManager` para administrar las licencias y las sesiones del servidor de licencias DRM de Primetime en las aplicaciones.

**Administración de licencias**

Cada vez que un dispositivo reproduce contenido protegido, el motor de ejecución obtiene y almacena en caché la licencia necesaria para ver el contenido. Si la aplicación guarda el contenido localmente y la licencia permite la reproducción sin conexión, el usuario puede ver el contenido de la aplicación sin conexión de red. Con `DRMManager`, puede almacenar la licencia en caché previamente. La aplicación no necesita obtener la licencia necesaria para ver el contenido. Por ejemplo, la aplicación podría descargar el archivo multimedia y luego obtener la licencia mientras el usuario sigue en línea.

Para cargar previamente una licencia, utilice un objeto `DRMContentData`. El objeto `DRMContentData` contiene la dirección URL del servidor de licencias DRM de Primetime que puede proporcionar la licencia y describe si se requiere autenticación de usuario. Con esta información, puede llamar al método `DRMManager` `loadVoucher()` para obtener y almacenar en caché la licencia. El flujo de trabajo de las licencias de precarga se describe con más detalle en *Licencias de precarga para reproducción sin conexión*.

**Administración de sesiones**

También puede utilizar `DRMManager` para autenticar al usuario en un servidor de licencias de DRM de Primetime y para administrar sesiones persistentes. Llame al método `DRMManager` `authenticate()` para establecer una sesión con el servidor de licencias DRM de Primetime. Cuando la autenticación se completa correctamente, el `DRMManager` envía un objeto `DRMAuthenticationCompleteEvent`. Este objeto contiene un token de sesión. Puede guardar este token para establecer sesiones futuras, de modo que el usuario no tenga que proporcionar sus credenciales de cuenta. Pase el token al método `setAuthenticationToken()` para establecer una nueva sesión autenticada. (La configuración del servidor que generó el token determina la caducidad del token y otros atributos).

## Gestión de eventos DRMStatus {#handling-drmstatus-events}

El `DRMManager` envía un objeto `DRMStatusEvent` después de que una llamada al método `loadVoucher()` se complete correctamente. Si se obtiene una licencia, la propiedad detail del objeto event tiene el valor: `DRM.voucherObtained` y la propiedad voucher contiene el objeto `DRMVoucher`. Si no se obtiene una licencia, la propiedad detail sigue teniendo el valor: `DRM.voucherObtained`; sin embargo, la propiedad voucher es nula. No se puede obtener una licencia si, por ejemplo, se utiliza el `LoadVoucherSetting` de `localOnly` y no hay una licencia en caché local. Si la llamada `loadVoucher()` no se completa correctamente, tal vez debido a un error de autenticación o comunicación, el `DRMManager` envía un objeto `DRMErrorEvent` o `DRMAuthenticationErrorEvent` en su lugar.

## Gestión de eventos DRMAuthauthenticationComplete{#handling-drmauthenticationcomplete-events}

El `DRMManager` envía un objeto `DRMAuthenticationCompleteEvent` cuando un usuario se autentica correctamente mediante una llamada al método `authenticate()`. El objeto `DRMAuthenticationCompleteEvent` contiene un token reutilizable que se puede utilizar para mantener la autenticación de usuarios entre sesiones de aplicación. Pase este token al método `DRMManager` `setAuthenticationToken()` para restablecer la sesión. (El creador de tokens establece atributos de token como la caducidad. Adobe no proporciona una API para examinar los atributos de token).

## Gestión de eventos DRMAuthauthenticationError{#handling-drmauthenticationerror-events}

El `DRMManager` envía un objeto `DRMAuthenticationErrorEvent` cuando un usuario no puede autenticarse correctamente mediante una llamada a los métodos `authenticate()` o `setAuthenticationToken()`.