---
description: La utilidad Password Scrambler cifra una contraseña para los archivos de configuración de Adobe Primetime DRM Server for Protected Streaming.
title: Password Scrambler
exl-id: 9cedd3e5-01db-4ea9-bf23-8767987fc26c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
