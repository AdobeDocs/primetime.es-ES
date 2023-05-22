---
title: Preparación de contraseñas mediante Java
description: Preparación de contraseñas mediante Java
copied-description: true
exl-id: 69d551c4-e13b-473a-86ed-36b5ba24f6b8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '22'
ht-degree: 0%

---

# Preparación de contraseñas mediante Java{#prepare-passwords-using-java}

Ejecute el `ScrambleUtil.class` con Java:

1. Vaya a `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/scrambler/ refimpl/scrambler/`
1. Desde la línea de comandos, escriba:

   ```
   java -classpath [DRM SDK DVD]/SDK/adobe-flashaccess-sdk.jar;  
       com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
   ```
