---
title: Preparación de contraseñas mediante Java
description: Preparación de contraseñas mediante Java
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
