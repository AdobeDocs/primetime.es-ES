---
seo-title: Información general sobre el uso de la clase DRMManager
title: Información general sobre el uso de la clase DRMManager
uuid: 71ce061b-75b6-4ab5-8bbd-cafe7c3e4592
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Uso de la clase DRMManager {#using-the-drmmanager-class}

Utilice la `DRMManager` clase para administrar licencias y sesiones del servidor de licencias DRM Primetime en las aplicaciones.

**Gestión de licencias**

Cada vez que un dispositivo reproduce contenido protegido, el motor de ejecución obtiene y almacena en caché la licencia necesaria para ver el contenido. Si la aplicación guarda el contenido localmente y la licencia permite la reproducción sin conexión, el usuario puede ver el contenido en la aplicación sin una conexión de red. Con el `DRMManager`, puede prealmacenar la licencia. La aplicación no necesita obtener la licencia necesaria para ver el contenido. Por ejemplo, la aplicación podría descargar el archivo multimedia y obtener la licencia mientras el usuario sigue en línea.

Para precargar una licencia, utilice un `DRMContentData` objeto. El `DRMContentData` objeto contiene la dirección URL del servidor de licencias DRM Primetime que puede proporcionar la licencia y describe si se requiere la autenticación del usuario. Con esta información, puede llamar al `DRMManager` método `loadVoucher()` para obtener y almacenar en caché la licencia. El flujo de trabajo de las licencias de precarga se describe con más detalle en Licencias de *precarga para reproducción* sin conexión.

**Administración de sesiones**

También puede utilizar `DRMManager` para autenticar al usuario en un servidor de licencias DRM de Primetime y para administrar sesiones persistentes. Llame al `DRMManager` `authenticate()` método para establecer una sesión con el servidor de licencias DRM Primetime. Cuando la autenticación se completa correctamente, el `DRMManager` distribuye un `DRMAuthenticationCompleteEvent` objeto. Este objeto contiene un token de sesión. Puede guardar este token para establecer sesiones futuras de modo que el usuario no tenga que proporcionar sus credenciales de cuenta. Pase el token al `setAuthenticationToken()` método para establecer una nueva sesión autenticada. (La configuración del servidor que generó el token determina la caducidad del token y otros atributos).

## Gestión de eventos DRMStatus {#handling-drmstatus-events}

El `DRMManager` distribuye un `DRMStatusEvent` objeto después de que se complete correctamente una llamada al `loadVoucher()` método. Si se obtiene una licencia, la propiedad detail del objeto event tiene el valor: `DRM.voucherObtained`y la propiedad voucher contiene el `DRMVoucher` objeto. Si no se obtiene una licencia, la propiedad detail aún tiene el valor: `DRM.voucherObtained`; sin embargo, la propiedad voucher es null. No se puede obtener una licencia si, por ejemplo, se usa el `LoadVoucherSetting` `localOnly` de y no hay una licencia en caché local. Si la `loadVoucher()` llamada no se completa correctamente, tal vez debido a un error de autenticación o comunicación, entonces `DRMManager` distribuye un `DRMErrorEvent` u `DRMAuthenticationErrorEvent` objeto.

## Gestión de eventos DRMAuthauthenticationComplete{#handling-drmauthenticationcomplete-events}

El `DRMManager` distribuye un `DRMAuthenticationCompleteEvent` objeto cuando un usuario se autentica correctamente mediante una llamada al `authenticate()` método. El `DRMAuthenticationCompleteEvent` objeto contiene un token reutilizable que se puede utilizar para mantener la autenticación de usuarios en las sesiones de la aplicación. Pase este token al `DRMManager` método `setAuthenticationToken()` para restablecer la sesión. (El creador de tokens establece atributos de token como la caducidad. Adobe no proporciona una API para examinar los atributos del token).

## Gestión de eventos DRMAuthauthenticationError{#handling-drmauthenticationerror-events}

El `DRMManager` distribuye un `DRMAuthenticationErrorEvent` objeto cuando un usuario no puede autenticarse correctamente mediante una llamada a los `authenticate()` métodos o `setAuthenticationToken()` .