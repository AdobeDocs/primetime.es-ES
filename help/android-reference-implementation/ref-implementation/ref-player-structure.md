---
description: Los administradores de funciones sirven como contenedores en la biblioteca TVSDK.
title: Estructura de implementación de referencia
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---


# Estructura de implementación de referencia {#reference-implementation-structure}

Los administradores de funciones sirven como contenedores en la biblioteca TVSDK.

En Java, las clases están estructuradas en una jerarquía. Por ejemplo, todo el código relacionado con la interfaz de usuario en `com.adobe.primetime.reference.ui` y todos los administradores de funciones están en `com.adobe.primetime.reference.manager`.

La implementación de referencia de Primetime contiene los siguientes paquetes:

| Paquete | Descripción |
|--- |--- |
| [com.adobe.primetime.reference](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/PrimetimeReference.html) | Esta clase amplía android.app.Application. |
| [com.adobe.primetime.reference.advertising](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/advertising/package-summary.html) | Contiene código para los anuncios personalizados. |
| [com.adobe.primetime.reference.config](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html) | Contiene el código de interfaz necesario para configurar los administradores de funciones. |
| [com.adobe.primetime.reference.drm](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/drm/package-summary.html) | Contiene clases de ayuda para DRM. |
| [com.adobe.primetime.reference.feeds](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/feeds/package-summary.html) | Los adaptadores y adaptadores de elementos para la interfaz, la plataforma y la información de referencia. También incluye el código FeedAdapterFactory, ContentRenditionInfo y XMLParserHelper. |
| [com.adobe.primetime.reference.logging](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/logging/package-summary.html) | Proporciona clases para registrar de forma local y remota. |
| [com.adobe.primetime.reference.manager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/package-summary.html) | Aquí es donde puede encontrar los administradores de funciones, así como el administrador de fábrica. Para las funciones opcionales que puede habilitar o deshabilitar, existen dos administradores de funciones: <ul><li>Un administrador de funciones que es el nombre de la función, por ejemplo, CCManager. Este administrador de funciones está desactivado y proporciona el comportamiento predeterminado desactivado.</li><li>Un administrador de funciones que tiene activado anexado al nombre del administrador de funciones, por ejemplo, CCManagerOn. Este administrador de funciones proporciona código de muestra para la función habilitada.</li></ul> |
| [com.adobe.primetime.reference.ui.catalog](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/catalog/package-summary.html) | Contiene código de IU para el catálogo. |
| [com.adobe.primetime.reference.ui.log](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/log/package-summary.html) | Contiene el código de la IU para el registro. |
| [com.adobe.primetime.reference.ui.player](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/package-summary.html) | Contiene el código de IU del reproductor. |
| [com.adobe.primetime.reference.ui.settings](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/settings/package-summary.html) | Contiene código de IU para la configuración. |
| [com.adobe.primetime.reference.utils](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/package-summary.html) | Contiene clases generales de utilidades. |
| [com.adobe.primetime.reference.utils.http](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/http/package-summary.html) | Contiene `HTTP-specific` clases de utilidades. |
