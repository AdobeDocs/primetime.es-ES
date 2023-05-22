---
title: Preparación de contraseñas con Ant
description: Preparación de contraseñas con Ant
copied-description: true
exl-id: 78f00fd7-ca9c-49a9-9e4b-6d1e2daf9241
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
