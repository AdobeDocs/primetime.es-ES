---
description: Si la aplicación necesita gestionar eventos distribuidos desde el administrador de funciones, debe registrar el administrador en el archivo PlayerFragment.java.
title: Gestión de eventos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# Gestión de eventos {#handling-events}

Si la aplicación necesita gestionar eventos distribuidos desde el administrador de funciones, debe registrar el administrador en el archivo PlayerFragment.java.

Por ejemplo:

```
private final AdsManager.AdsManagerEventListener adsManagerEventListener =  
  new AdsManager.AdsManagerEventListener() { 
 
    // add the ads functionality... 
 
} 
 
//Register the listener 
adsManager.addEventListener(adsManagerEventListener);
```
