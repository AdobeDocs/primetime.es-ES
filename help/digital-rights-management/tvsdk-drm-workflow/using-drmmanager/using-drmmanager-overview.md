---
title: Información general sobre el uso de la clase DRManager
description: Información general sobre el uso de la clase DRManager
copied-description: true
exl-id: 941a69fb-3085-45d6-9176-08ebb93cada4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# Uso de la clase DRManager {#using-the-drmmanager-class}

Utilice el `DRMManager` para administrar licencias y sesiones del servidor de licencias DRM de Primetime en aplicaciones.

**Administración de licencias**

Siempre que un dispositivo reproduce contenido protegido, el motor en tiempo de ejecución obtiene y almacena en caché la licencia necesaria para ver el contenido. Si la aplicación guarda el contenido localmente y la licencia permite la reproducción sin conexión, el usuario puede ver el contenido en la aplicación sin una conexión de red. Uso del `DRMManager`, puede prealmacenar en caché la licencia. La aplicación no tiene que obtener la licencia necesaria para ver el contenido. Por ejemplo, la aplicación podría descargar el archivo multimedia y, a continuación, obtener la licencia mientras el usuario sigue en línea.

Para cargar previamente una licencia, utilice un `DRMContentData` objeto. El `DRMContentData` contiene la URL del servidor de licencias DRM de Primetime que puede proporcionar la licencia y describe si se requiere la autenticación del usuario. Con esta información, puede llamar a la función `DRMManager` `loadVoucher()` para obtener y almacenar en caché la licencia. El flujo de trabajo para la precarga de licencias se describe con más detalle en *Precarga de licencias para la reproducción sin conexión*.

**Administración de sesiones**

También puede utilizar la variable `DRMManager` para autenticar al usuario en un servidor de licencias DRM de Primetime y para administrar sesiones persistentes. Llame a `DRMManager` `authenticate()` para establecer una sesión con el servidor de licencias DRM de Primetime. Cuando la autenticación se completa correctamente, la variable `DRMManager` envía un `DRMAuthenticationCompleteEvent` objeto. Este objeto contiene un token de sesión. Puede guardar este token para establecer sesiones futuras, de modo que el usuario no tenga que proporcionar sus credenciales de cuenta. Pase el token a `setAuthenticationToken()` para establecer una nueva sesión autenticada. (La configuración del servidor que generó el token determina la caducidad del token y otros atributos).

## Gestión de eventos DRMStatus {#handling-drmstatus-events}

El `DRMManager` envía un `DRMStatusEvent` después de una llamada a `loadVoucher()` El método se completa correctamente. Si se obtiene una licencia, la propiedad detail del objeto de evento tiene el valor: `DRM.voucherObtained`y la propiedad de cupones contiene el `DRMVoucher` objeto. Si no se obtiene una licencia, la propiedad detail sigue teniendo el valor: `DRM.voucherObtained`; sin embargo, la propiedad de cupones es nula. No se puede obtener una licencia si, por ejemplo, se utiliza el `LoadVoucherSetting` de `localOnly` y no hay ninguna licencia almacenada en caché local. Si la variable `loadVoucher()` La llamada de no se completa correctamente, tal vez debido a un error de autenticación o comunicación, y el `DRMManager` envía un `DRMErrorEvent` o `DRMAuthenticationErrorEvent` objeto en su lugar.

## Administrar eventos DRMAuthenticationComplete{#handling-drmauthenticationcomplete-events}

El `DRMManager` envía un `DRMAuthenticationCompleteEvent` objeto cuando un usuario se autentica correctamente mediante una llamada a `authenticate()` método. El `DRMAuthenticationCompleteEvent` contiene un token reutilizable que se puede utilizar para mantener la autenticación del usuario en todas las sesiones de la aplicación. Pasar este token a `DRMManager` `setAuthenticationToken()` para restablecer la sesión. (El creador de tokens establece atributos de tokens como la caducidad. El Adobe no proporciona una API para examinar atributos de token).

## Controlar eventos DRMAuthenticationError{#handling-drmauthenticationerror-events}

El `DRMManager` envía un `DRMAuthenticationErrorEvent` objeto cuando un usuario no puede autenticarse correctamente mediante una llamada a `authenticate()` o `setAuthenticationToken()` métodos.
