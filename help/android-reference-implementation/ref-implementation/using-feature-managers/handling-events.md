---
description: Si la aplicación necesita gestionar eventos distribuidos desde el administrador de funciones, debe registrar al administrador en el archivo PlayerFragment.java .
title: Gestión de eventos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 4%

---


# Gestión de eventos {#handling-events}

Si la aplicación necesita gestionar eventos distribuidos desde el administrador de funciones, debe registrar al administrador en el archivo PlayerFragment.java .

Por ejemplo:

```
private final AdsManager.AdsManagerEventListener adsManagerEventListener =  
  new AdsManager.AdsManagerEventListener() { 
 
    // add the ads functionality... 
 
} 
 
//Register the listener 
adsManager.addEventListener(adsManagerEventListener);
```
