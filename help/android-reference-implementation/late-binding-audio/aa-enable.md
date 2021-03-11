---
description: Puede integrar el enlace tardío o las transmisiones de audio alternativas en el reproductor mediante la creación de un gestor de funciones de audio alternativo.
title: Integración del audio de enlace tardío
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# Integración del audio de enlace tardío {#integrate-late-binding-audio}

Puede integrar el enlace tardío o las transmisiones de audio alternativas en el reproductor mediante la creación de un gestor de funciones de audio alternativo.

* Para crear un gestor de audio alternativo:

   ```java
   AAManager aaManager = new AAManagerOn(); 
   ```

* Para utilizar ManagerFactory para habilitar audio alternativo, asegúrese de que la siguiente línea de código esté en el archivo `PlayerFragment.java`:

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>true</b>,config, mediaPlayer);
   ```

   Para desactivar el audio alternativo:

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>false</b>,config, mediaPlayer);
   ```

