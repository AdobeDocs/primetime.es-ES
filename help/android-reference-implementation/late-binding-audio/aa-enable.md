---
description: Puede integrar flujos de audio alternativos o de enlace en tiempo de ejecución en el reproductor creando un administrador de funciones de audio alternativo.
title: Integración de audio de enlace en tiempo real
exl-id: 43be9042-d547-4646-a920-cdd2a5dbb1fb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
