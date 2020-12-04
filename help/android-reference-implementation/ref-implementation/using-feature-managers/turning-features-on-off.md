---
description: Puede activar o desactivar las funciones sin tener que pasar por el código mediante la fábrica del administrador.
seo-description: Puede activar o desactivar las funciones sin tener que pasar por el código mediante la fábrica del administrador.
seo-title: Activación o desactivación de funciones mediante ManagerFactory
title: Activación o desactivación de funciones mediante ManagerFactory
uuid: 385c2707-95f7-4628-8d25-67731151cb6a
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# Activación o desactivación de funciones mediante ManagerFactory{#turning-features-on-or-off-using-managerfactory}

Puede activar o desactivar las funciones sin tener que pasar por el código mediante la fábrica del administrador.

El argumento de habilitación del ejemplo siguiente determina si la función se utiliza o no. Si es false, se crea el administrador de funciones, pero proporciona únicamente la funcionalidad predeterminada para el reproductor, como si no se hubiera creado el administrador de funciones. Si es true, se crea el administrador de funciones, la función se activa y el reproductor de medios acepta entradas del archivo de configuración.

Por ejemplo, en el archivo `com.adobe.primetime.reference.ui.player.PlayerFragment.java`:

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**Documentación** de API:  [ManagerFactory](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)