---
title: Acceso al inicio de sesión único (SSO) del SDK para Android de Enabler en aplicaciones Android 10
description: Acceso al inicio de sesión único (SSO) del SDK para Android de Enabler en aplicaciones Android 10
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---



# Acceso al inicio de sesión único (SSO) del SDK para Android de Enabler en aplicaciones Android 10 {#access-enabler-android-sdk-single-sign-on-sso-on-android-10-apps}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Información general

El inicio de sesión único (SSO) entre aplicaciones con autenticación de Adobe Primetime está disponible en dispositivos con Android OS a través del SDK para Android de Access Enabler. Para ofrecer el inicio de sesión único (SSO) en dispositivos Android, el SDK para Android de Access Enabler versión 3.2.1 (última) y las versiones anteriores utilizan un archivo de base de datos compartido guardado en una implementación de almacenamiento Android, accesible en todas las aplicaciones con autenticación Adobe Primetime.

Sin embargo, Google en la última versión de Android 10 produjo algunos cambios &quot;para dar a los usuarios más control sobre sus archivos y para limitar el desorden de archivos, las aplicaciones dirigidas a Android 10 (nivel de API 29) y superiores tienen acceso con ámbitos en un dispositivo de almacenamiento externo, o almacenamiento con ámbitos, de forma predeterminada. Estas aplicaciones solo pueden ver su directorio específico de la aplicación `\[...\]`&quot;. Se presentan más detalles relacionados con estos cambios en el almacenamiento de Android 10 en [Documentación de almacenamiento de datos y archivos para Android](https://developer.android.com/training/data-storage/files/external-scoped).

Como resultado de estos cambios, la versión de Android de Access Enabler ofrece el inicio de sesión único (SSO) **SDK 3.2.1 (última versión)** y las versiones anteriores pueden verse afectadas en dispositivos Android 10, tal como se explica en la siguiente sección.

Consulte [Información general de Roku SSO](/help/authentication/roku-sso-overview.md).

## Comportamiento

Según el **nivel de SDK de target** o el uso de **android:requestLegacyExternalStorage** Atributo de manifiesto El inicio de sesión único (SSO) ofrecido por el SDK de Access Enabler para Android versión 3.2.1 (última) y versiones anteriores se comportará de la siguiente manera:

- Sus destinos de aplicación **Android 9 (nivel de API 28)** o inferior **-\>** Inicio de sesión único (SSO) **funcionará**
- Sus destinos de aplicación **Android 10** **(Nivel de API 29)** y sí **set** el valor de **requestLegacyExternalStorage en true** en el archivo de manifiesto de la aplicación **-\>** Inicio de sesión único (SSO) **funcionará**
- Sus destinos de aplicación **Android 10** **(Nivel de API 29)** y sí **sin configurar** el valor de **requestLegacyExternalStorage en true** en el archivo de manifiesto de la aplicación **-\>** Inicio de sesión único (SSO) **no funcionará**


>[!TIP]
>
> Antes de que el SDK para Android de Access Enabler de autenticación de Adobe Primetime sea totalmente compatible con el almacenamiento de ámbitos, puede desactivar temporalmente la opción en función del nivel de SDK de destino de la aplicación o del atributo requestLegacyExternalStorage manifest tal como se explica en público [Documentación de Android](https://developer.android.com/training/data-storage/files/external-scoped#opt-out-of-scoped-storage).

