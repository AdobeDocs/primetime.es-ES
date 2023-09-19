---
title: Autenticación Notas de la versión de Android 3.7.3
description: Autenticación Notas de la versión de Android 3.7.3
source-git-commit: fbc0e710d205532d268213ca0bdc81449e9c9835
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Autenticación Notas de la versión de Android 3.7.3 {#android-sdk-370-release-notes}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.

En esta página se describen las nuevas funciones, los cambios y los problemas conocidos de esta versión:

## Número de compilación {#build-no-android-sdk-373}

Autenticación de Adobe Primetime: Android 3.7.3

Fecha de versión: 19/09/2023



## Información general de versión {#overview-android-sdk-370}

* Cambios para admitir Android 14 y aplicaciones dirigidas al nivel de API 34
   * Añadir indicador requerido por [Receptores de emisiones registradas en tiempo de ejecución de Android 14](https://developer.android.com/about/versions/14/behavior-changes-14#runtime-receivers-exported).
* Se ha corregido que ChromeCustomTabs no se abriera para el inicio de sesión de MVPD en la API del emulador 32+
   * Nota: Una solución para este problema en el SDK &lt;3.7.3 es abrir la aplicación Chrome en el emulador y terminar de configurarla antes de intentar iniciar sesión en MVPD


## Liberar paquete {#rel=pkg-android373}

Puede descargar el SDK v3.7.3 de Android desde [aquí](https://tve.zendesk.com/hc/en-us/articles/204963219-Android-Native-AccessEnabler-Library).

Antes de actualizar a esta versión, compruebe esta nota técnica.