---
seo-title: Información general sobre el uso de la clase DRMManager
title: Información general sobre el uso de la clase DRMManager
uuid: 71ce061b-75b6-4ab5-8bbd-cafe7c3e4592
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# Uso de la clase DRMManager {#using-the-drmmanager-class}

Utilice la clase `DRMManager` para administrar las licencias y las sesiones del servidor de licencias DRM de Primetime en las aplicaciones.

**Gestión de licencias**

Cada vez que un dispositivo reproduce contenido protegido, el motor de ejecución obtiene y almacena en caché la licencia necesaria para la vista del contenido. Si la aplicación guarda el contenido localmente y la licencia permite la reproducción sin conexión, el usuario puede realizar la vista del contenido en la aplicación sin una conexión de red. Con el `DRMManager`, puede prealmacenar la licencia. La aplicación no necesita obtener la licencia necesaria para la vista del contenido. Por ejemplo, la aplicación podría descargar el archivo multimedia y obtener la licencia mientras el usuario sigue en línea.

Para precargar una licencia, utilice un objeto `DRMContentData`. El objeto `DRMContentData` contiene la dirección URL del servidor de licencias DRM de Primetime que puede proporcionar la licencia y describe si se requiere la autenticación del usuario. Con esta información, puede llamar al método `DRMManager` `loadVoucher()` para obtener y almacenar en caché la licencia. El flujo de trabajo para licencias de precarga se describe con más detalle en *licencias de Precarga para reproducción sin conexión*.

**Administración de sesiones**

También puede utilizar `DRMManager` para autenticar al usuario en un servidor de licencias DRM de Primetime y administrar sesiones persistentes. Llame al método `DRMManager` `authenticate()` para establecer una sesión con el servidor de licencias DRM de Primetime. Cuando la autenticación se completa correctamente, `DRMManager` distribuye un objeto `DRMAuthenticationCompleteEvent`. Este objeto contiene un token de sesión. Puede guardar este token para establecer sesiones futuras de modo que el usuario no tenga que proporcionar sus credenciales de cuenta. Pase el token al método `setAuthenticationToken()` para establecer una nueva sesión autenticada. (La configuración del servidor que generó el token determina la caducidad del token y otros atributos).

## Gestión de Eventos DRMStatus {#handling-drmstatus-events}

El `DRMManager` distribuye un objeto `DRMStatusEvent` después de que se complete correctamente una llamada al método `loadVoucher()`. Si se obtiene una licencia, la propiedad detail del objeto evento tiene el valor: `DRM.voucherObtained` y la propiedad voucher contiene el objeto `DRMVoucher`. Si no se obtiene una licencia, la propiedad detail aún tiene el valor: `DRM.voucherObtained`; sin embargo, la propiedad voucher es null. No se puede obtener una licencia si, por ejemplo, se utiliza el `LoadVoucherSetting` de `localOnly` y no hay una licencia en caché local. Si la llamada `loadVoucher()` no se completa correctamente, tal vez debido a un error de autenticación o comunicación, el `DRMManager` distribuye un objeto `DRMErrorEvent` o `DRMAuthenticationErrorEvent` en su lugar.

## Gestión de Eventos DRMAuthauthenticationComplete{#handling-drmauthenticationcomplete-events}

El `DRMManager` distribuye un objeto `DRMAuthenticationCompleteEvent` cuando un usuario se autentica correctamente mediante una llamada al método `authenticate()`. El objeto `DRMAuthenticationCompleteEvent` contiene un token reutilizable que se puede utilizar para mantener la autenticación del usuario en todas las sesiones de la aplicación. Pase este token al método `DRMManager` `setAuthenticationToken()` para restablecer la sesión. (El creador de tokens establece atributos de token como la caducidad. Adobe no proporciona una API para examinar los atributos del token).

## Gestión de eventos DRMAuthauthenticationError{#handling-drmauthenticationerror-events}

El `DRMManager` distribuye un objeto `DRMAuthenticationErrorEvent` cuando un usuario no puede autenticarse correctamente mediante una llamada a los métodos `authenticate()` o `setAuthenticationToken()`.