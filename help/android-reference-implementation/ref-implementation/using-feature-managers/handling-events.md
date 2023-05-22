---
description: Si la aplicación necesita gestionar eventos distribuidos desde el administrador de funciones, debe registrar el administrador en el archivo PlayerFragment.java.
title: Gestión de eventos
exl-id: 4c9a76bb-071e-4408-819c-a7611fe615cd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
