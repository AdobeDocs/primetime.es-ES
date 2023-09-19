---
description: Puede integrar flujos de audio alternativos o de enlace en tiempo de ejecución en el reproductor creando un administrador de funciones de audio alternativo.
title: Integración de audio de enlace en tiempo real
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# Integración de audio de enlace en tiempo real {#integrate-late-binding-audio}

Puede integrar flujos de audio alternativos o de enlace en tiempo de ejecución en el reproductor creando un administrador de funciones de audio alternativo.

* Para crear un gestor de audio alternativo:

  ```java
  AAManager aaManager = new AAManagerOn(); 
  ```

* Para utilizar ManagerFactory para activar el audio alternativo, asegúrese de que la siguiente línea de código se encuentra en `PlayerFragment.java` archivo:

  ```java
  aaManager = ManagerFactory.getAAManager( 
  <b>true</b>,config, mediaPlayer);
  ```

  Para desactivar el audio alternativo:

  ```java
  aaManager = ManagerFactory.getAAManager( 
  <b>false</b>,config, mediaPlayer);
  ```
