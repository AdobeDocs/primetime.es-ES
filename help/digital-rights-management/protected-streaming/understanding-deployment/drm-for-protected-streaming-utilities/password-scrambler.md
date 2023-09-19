---
description: La utilidad Password Scrambler cifra una contraseña para los archivos de configuración de Adobe Primetime DRM Server for Protected Streaming.
title: Password Scrambler
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Password Scrambler {#password-scrambler}

La utilidad Password Scrambler cifra una contraseña para los archivos de configuración de Adobe Primetime DRM Server for Protected Streaming.

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

Todas las contraseñas especificadas en la variable [!DNL flashaccess-global.xml] y [!DNL flashaccess-tenant.xml] los archivos deben estar cifrados.

>[!NOTE]
>
>La utilidad Password Scrambler del servidor DRM de Primetime para flujo protegido no se puede intercambiar con el codificador que se proporciona con el servidor de licencias de implementación de referencia.
