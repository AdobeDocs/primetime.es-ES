---
description: Puede activar o desactivar las funciones sin tener que pasar por el código utilizando la fábrica del administrador.
title: Activar o desactivar las funciones mediante ManagerFactory
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# Activar o desactivar las funciones con ManagerFactory{#turning-features-on-or-off-using-managerfactory}

Puede activar o desactivar las funciones sin tener que pasar por el código utilizando la fábrica del administrador.

El argumento de habilitación del ejemplo siguiente determina si la función se utiliza o no. Si tiene el valor false, se crea el administrador de funciones, pero solo proporciona la funcionalidad predeterminada al reproductor, como si no se hubiera creado el administrador de funciones. Si tiene el valor true, se crea el administrador de funciones, la función se activa y el reproductor de medios acepta la entrada del archivo de configuración.

Por ejemplo, en el archivo `com.adobe.primetime.reference.ui.player.PlayerFragment.java`:

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**Documentación** de API:  [ManagerFactory](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)