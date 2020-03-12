---
description: Si la aplicación necesita gestionar eventos enviados desde el administrador de funciones, debe registrar al administrador en el archivo PlayerFragment.java.
seo-description: Si la aplicación necesita gestionar eventos enviados desde el administrador de funciones, debe registrar al administrador en el archivo PlayerFragment.java.
seo-title: Gestión de eventos
title: Gestión de eventos
uuid: 13639f02-0dcc-4a0a-8524-515da5478006
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Gestión de eventos {#handling-events}

Si la aplicación necesita gestionar eventos enviados desde el administrador de funciones, debe registrar al administrador en el archivo PlayerFragment.java.

Por ejemplo:

```
private final AdsManager.AdsManagerEventListener adsManagerEventListener =  
  new AdsManager.AdsManagerEventListener() { 
 
    // add the ads functionality... 
 
} 
 
//Register the listener 
adsManager.addEventListener(adsManagerEventListener);
```
