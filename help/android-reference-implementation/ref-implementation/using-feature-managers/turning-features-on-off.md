---
description: Puede activar o desactivar las funciones sin pasar por el código mediante el uso de la fábrica del administrador.
title: Activación o desactivación de funciones con ManagerFactory
exl-id: 4e288a6e-80e5-43c1-aba2-374723dd9957
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# Activación o desactivación de funciones con ManagerFactory{#turning-features-on-or-off-using-managerfactory}

Puede activar o desactivar las funciones sin pasar por el código mediante el uso de la fábrica del administrador.

El argumento de habilitación del ejemplo siguiente determina si la función se utiliza o no. Si es false, se crea el administrador de funciones, pero solo proporciona la funcionalidad predeterminada al reproductor, como si no se hubiera creado. Si el valor es True, se crea el administrador de funciones, la función se activa y el reproductor de medios acepta la entrada del archivo de configuración.

Por ejemplo, en la variable `com.adobe.primetime.reference.ui.player.PlayerFragment.java` archivo:

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**Documentación de API**: [ManagerFactory](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)
