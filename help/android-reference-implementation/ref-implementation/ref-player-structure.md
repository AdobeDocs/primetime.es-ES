---
description: Los administradores de funciones sirven de envoltorios en la biblioteca TVSDK.
seo-description: Los administradores de funciones sirven de envoltorios en la biblioteca TVSDK.
seo-title: Estructura de implementación de referencia
title: Estructura de implementación de referencia
uuid: ae347a97-1500-476a-9fc8-c99e6b2ab8de
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Estructura de implementación de referencia {#reference-implementation-structure}

Los administradores de funciones sirven de envoltorios en la biblioteca TVSDK.

En Java, las clases están estructuradas en una jerarquía. Por ejemplo, todos los códigos relacionados con la IU debajo `com.adobe.primetime.reference.ui` y todos los administradores de funciones están en `com.adobe.primetime.reference.manager`.

La implementación de referencia de Primetime contiene los siguientes paquetes:

| Paquete | Descripción |
|--- |--- |
| [com.adobe.primetime.reference](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/PrimetimeReference.html) | Esta clase amplía android.app.Application. |
| [com.adobe.primetime.reference.publicidad](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/advertising/package-summary.html) | Contiene código para las publicidades personalizadas. |
| [com.adobe.primetime.reference.config](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html) | Contiene el código de interfaz necesario para configurar los administradores de funciones. |
| [com.adobe.primetime.reference.drm](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/drm/package-summary.html) | Contiene clases auxiliares para DRM. |
| [com.adobe.primetime.reference.feeds](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/feeds/package-summary.html) | Adaptadores y adaptadores de elementos para interfaz, plataforma e información de referencia. También incluye el código FeedAdapterFactory, ContentRenditionInfo y XMLParserHelper. |
| [com.adobe.primetime.reference.logging](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/logging/package-summary.html) | Proporciona clases para el registro local y remoto. |
| [com.adobe.primetime.reference.manager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/package-summary.html) | Aquí es donde puede encontrar los administradores de funciones, así como también ManagerFactory. Para las funciones opcionales que puede activar o desactivar, hay dos administradores de funciones: <ul><li>Un administrador de funciones que es el nombre de la función, por ejemplo, CCManager. Este administrador de funciones está desactivado y proporciona el comportamiento predeterminado desactivado.</li><li>Un administrador de funciones que tiene activado anexado al nombre del administrador de funciones, por ejemplo, CCManagerOn. Este administrador de funciones proporciona código de muestra para la función habilitada.</li></ul> |
| [com.adobe.primetime.reference.ui.catalog](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/catalog/package-summary.html) | Contiene código de interfaz de usuario para el catálogo. |
| [com.adobe.primetime.reference.ui.log](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/log/package-summary.html) | Contiene código de interfaz de usuario para el registro. |
| [com.adobe.primetime.reference.ui.player](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/package-summary.html) | Contiene código de interfaz de usuario para el reproductor. |
| [com.adobe.primetime.reference.ui.seón](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/settings/package-summary.html) | Contiene código de interfaz de usuario para la configuración. |
| [com.adobe.primetime.reference.utils](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/package-summary.html) | Contiene clases generales de utilidades. |
| [com.adobe.primetime.reference.utils.http](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/http/package-summary.html) | Contiene `HTTP-specific` clases de utilidades. |
