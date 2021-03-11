---
description: La utilidad Password Scrambler cifra una contraseña para el servidor Adobe Primetime DRM para los archivos de configuración de transmisión protegida.
title: Desencadenador de contraseña
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Descodificador de contraseña {#password-scrambler}

La utilidad Password Scrambler cifra una contraseña para el servidor Adobe Primetime DRM para los archivos de configuración de transmisión protegida.

Para ejecutar el marcador, escriba:

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
>La utilidad Password Scrambler del servidor Primetime DRM para transmisión protegida no es intercambiable con el reproductor que se proporciona con el servidor de licencias de implementación de referencia.