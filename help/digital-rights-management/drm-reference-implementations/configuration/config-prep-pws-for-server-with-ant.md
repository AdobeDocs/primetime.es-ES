---
title: Preparación de contraseñas con Ant
description: Preparación de contraseñas con Ant
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---

# Preparación de contraseñas con Ant{#prepare-passwords-using-ant}

Utilice Ant para cifrar la contraseña:

1. Vaya a `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`
1. Configure las variables `sdkdir` propiedad en [!DNL build-refimpl.xml] para que apunte al directorio que incluye el SDK de Java de DRM de Primetime.
1. Ejecute el siguiente comando:

   ```
   ant -f build-refimpl.xml
   ```
