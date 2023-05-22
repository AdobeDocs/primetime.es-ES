---
description: Los administradores de funciones sirven como contenedores para la biblioteca de TVSDK.
title: Estructura de implementación de referencia
exl-id: cf102ccc-2e31-4197-a321-e485f77ba754
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# Estructura de implementación de referencia {#reference-implementation-structure}

Los administradores de funciones sirven como contenedores para la biblioteca de TVSDK.

En Java, las clases están estructuradas en una jerarquía. Por ejemplo, todo el código relacionado con la interfaz de usuario en `com.adobe.primetime.reference.ui` y todos los administradores de funciones se encuentran en `com.adobe.primetime.reference.manager`.

La implementación de referencia de Primetime contiene los siguientes paquetes:

| Paquete | Descripción |
|--- |--- |
| [com.adobe.primetime.reference](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/PrimetimeReference.html) | Esta clase amplía android.app.Application. |
| [com.adobe.primetime.reference.advertising](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/advertising/package-summary.html) | Contiene código para anuncios personalizados. |
| [com.adobe.primetime.reference.config](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html) | Contiene el código de interfaz necesario para configurar los administradores de características. |
| [com.adobe.primetime.reference.drm](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/drm/package-summary.html) | Contiene clases auxiliares para DRM. |
| [com.adobe.primetime.reference.feeds](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/feeds/package-summary.html) | Adaptadores y adaptadores de elementos para información de interfaz, plataforma y referencia. También incluye el código FeedAdapterFactory, ContentRenditionInfo y XMLParserHelper. |
| [com.adobe.primetime.reference.logging](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/logging/package-summary.html) | Proporciona clases para registrar de forma local y remota. |
| [com.adobe.primetime.reference.manager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/package-summary.html) | Aquí es donde puede encontrar los administradores de funciones, así como ManagerFactory. Para las funciones opcionales que puede habilitar o deshabilitar, hay dos administradores de funciones: <ul><li>Un administrador de funciones es el nombre de la función, por ejemplo, CCManager. Este administrador de funciones está desactivado y proporciona el comportamiento de desactivación predeterminado.</li><li>Un administrador de funciones con el valor Activado anexado al nombre del administrador de funciones, por ejemplo, CCManagerOn. Este administrador de funciones proporciona código de ejemplo para la función habilitada.</li></ul> |
| [com.adobe.primetime.reference.ui.cadialog](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/catalog/package-summary.html) | Contiene el código de la interfaz de usuario del catálogo. |
| [com.adobe.primetime.reference.ui.log](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/log/package-summary.html) | Contiene el código de la interfaz de usuario del registro. |
| [com.adobe.primetime.reference.ui.player](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/package-summary.html) | Contiene el código de la interfaz de usuario del reproductor. |
| [com.adobe.primetime.reference.ui.settings](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/settings/package-summary.html) | Contiene el código de la IU para la configuración. |
| [com.adobe.primetime.reference.utils](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/package-summary.html) | Contiene clases de utilidad generales. |
| [com.adobe.primetime.reference.utils.http](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/http/package-summary.html) | Contains `HTTP-specific` clases de utilidades. |
