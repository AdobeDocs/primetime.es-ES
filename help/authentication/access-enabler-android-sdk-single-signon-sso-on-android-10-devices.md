---
title: Acceso Habilitar el inicio de sesión único (SSO) del SDK de Android en aplicaciones de Android 10
description: Acceso Habilitar el inicio de sesión único (SSO) del SDK de Android en aplicaciones de Android 10
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# Acceso Habilitar el inicio de sesión único (SSO) del SDK de Android en aplicaciones de Android 10 {#access-enabler-android-sdk-single-sign-on-sso-on-android-10-apps}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.

## Información general

El inicio de sesión único (SSO) entre aplicaciones con autenticación de Adobe Primetime está disponible en dispositivos que utilizan el sistema operativo Android a través del SDK de Android con el servicio de habilitación de acceso. Para ofrecer el inicio de sesión único (SSO) en dispositivos Android, el Access Enabler Android SDK versión 3.2.1 (más reciente) y las versiones anteriores utilizan un archivo de base de datos compartido guardado en una implementación de almacenamiento de Android, al que pueden acceder todas las aplicaciones con autenticación de Adobe Primetime.

Sin embargo, en la última versión de Android 10, Google produjo algunos cambios &quot;para dar a los usuarios más control sobre sus archivos y para limitar el desorden de archivos, las aplicaciones dirigidas a Android 10 (nivel de API 29) y superiores reciben acceso con ámbito en un dispositivo de almacenamiento externo, o almacenamiento con ámbito, de forma predeterminada. Estas aplicaciones solo pueden ver su directorio específico de la aplicación `\[...\]`&quot;. Más detalles relacionados con estos cambios de almacenamiento de Android 10 se presentan en [Documentación de almacenamiento de datos y archivos para Android](https://developer.android.com/training/data-storage/files/external-scoped).

Como resultado de estos cambios, el inicio de sesión único (SSO) ofrecido por la versión de Access Enabler de Android **SDK 3.2.1 (última versión)** y versiones anteriores pueden verse afectadas en dispositivos Android 10, como se explica en la siguiente sección.

Consulte [Información general de Roku SSO](/help/authentication/roku-sso-overview.md).

## Comportamiento

Según la aplicación de **nivel de SDK de destino** o el uso de **android:requestLegacyExternalStorage** Atributo de manifiesto de inicio de sesión único (SSO) ofrecido por el SDK de Access Enabler Android versión 3.2.1 (más reciente) y las versiones anteriores se comportarán de la siguiente manera:

- Destinos de su aplicación **Android 9 (nivel de API 28)** o inferior **-\>** Inicio de sesión único (SSO) **funcionará**
- Destinos de su aplicación **Android 10** **(Nivel de API 29)** y lo hace **set** el valor de **requestLegacyExternalStorage a true** en el archivo de manifiesto de su aplicación **-\>** Inicio de sesión único (SSO) **funcionará**
- Destinos de su aplicación **Android 10** **(Nivel de API 29)** y lo hace **sin configurar** el valor de **requestLegacyExternalStorage a true** en el archivo de manifiesto de su aplicación **-\>** Inicio de sesión único (SSO) **no funcionará**


>[!TIP]
>
> Antes de que la autenticación de Adobe Primetime permita el acceso El SDK de Android sea totalmente compatible con el almacenamiento con ámbito, puede optar por excluirse temporalmente en función del nivel de SDK de destino de la aplicación o del atributo de manifiesto requestLegacyExternalStorage, tal como se explica en público [Documentación de Android](https://developer.android.com/training/data-storage/files/external-scoped#opt-out-of-scoped-storage).
