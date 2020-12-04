---
description: 'null'
seo-description: 'null'
seo-title: Preparación de contraseñas con Ant
title: Preparación de contraseñas con Ant
uuid: 9419ab0d-b448-4881-9d26-35c00f0b13bc
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '42'
ht-degree: 0%

---


# Preparar contraseñas con Ant{#prepare-passwords-using-ant}

Use Ant para cifrar su contraseña:

1. Vaya a `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`
1. Establezca la propiedad `sdkdir` en [!DNL build-refimpl.xml] para que señale al directorio que incluye el SDK de Java de DRM Primetime.
1. Ejecute el siguiente comando:

   ```
   ant -f build-refimpl.xml
   ```

