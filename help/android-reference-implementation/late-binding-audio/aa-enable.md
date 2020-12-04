---
description: Puede integrar flujos de audio alternativos o de enlace tardío en el reproductor creando un administrador de funciones de audio alternativo.
seo-description: Puede integrar flujos de audio alternativos o de enlace tardío en el reproductor creando un administrador de funciones de audio alternativo.
seo-title: Integrar audio de enlace tardío
title: Integrar audio de enlace tardío
uuid: cd2e259a-2af4-4d7b-a856-79bd087e8ca6
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Integrar audio de enlace tardío {#integrate-late-binding-audio}

Puede integrar flujos de audio alternativos o de enlace tardío en el reproductor creando un administrador de funciones de audio alternativo.

* Para crear un administrador de audio alternativo:

   ```java
   AAManager aaManager = new AAManagerOn(); 
   ```

* Para utilizar ManagerFactory para habilitar el audio alternativo, asegúrese de que la siguiente línea de código esté en el archivo `PlayerFragment.java`:

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>true</b>,config, mediaPlayer);
   ```

   Para desactivar el audio alternativo:

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>false</b>,config, mediaPlayer);
   ```

