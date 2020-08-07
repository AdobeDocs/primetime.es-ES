---
description: La utilidad Password Scrambler cifra una contraseña para el servidor Adobe Primetime DRM para los archivos de configuración de flujo protegido.
seo-description: La utilidad Password Scrambler cifra una contraseña para el servidor Adobe Primetime DRM para los archivos de configuración de flujo protegido.
seo-title: Rótulo de contraseña
title: Rótulo de contraseña
uuid: 56df0f49-f3fd-464d-b4ba-25e1b497158a
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---


# Rótulo de contraseña {#password-scrambler}

La utilidad Password Scrambler cifra una contraseña para el servidor Adobe Primetime DRM para los archivos de configuración de flujo protegido.

Para ejecutar el codificador, escriba:

```
Scrambler.bat  
<i class="+ topic ph hi-d="" i "="">
  password 
</i class="+ topic>
```

o

```
java -jar libs/flashaccess-scrambler.jar  
<i class="+ topic ph hi-d="" i "="">
  password  
</i class="+ topic>
```

La utilidad muestra el siguiente mensaje:

```
Encrypted password:  
<i class="+ topic ph hi-d="" i "="">
  scrambled-password 
</i class="+ topic>
```

Todas las contraseñas especificadas en los archivos [!DNL flashaccess-global.xml] y [!DNL flashaccess-tenant.xml] deben cifrarse.

>[!NOTE]
>
>La utilidad Password Scrambler de Primetime DRM Server for Protected Streaming no es intercambiable con el codificador que se proporciona con el servidor de licencias de implementación de referencia.