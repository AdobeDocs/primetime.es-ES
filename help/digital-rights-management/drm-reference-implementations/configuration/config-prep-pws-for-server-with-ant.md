---
title: Preparación de contraseñas con Ant
description: Preparación de contraseñas con Ant
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---


# Preparación de contraseñas con Ant{#prepare-passwords-using-ant}

Utilice Ant para cifrar la contraseña:

1. Vaya a `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`
1. Establezca la propiedad `sdkdir` en [!DNL build-refimpl.xml] para que apunte al directorio que incluye el SDK de Java de DRM de Primetime.
1. Ejecute el siguiente comando:

   ```
   ant -f build-refimpl.xml
   ```

