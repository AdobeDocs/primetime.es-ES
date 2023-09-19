---
title: Descodificador de contraseñas
description: Descodificador de contraseñas
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---

# Descodificador de contraseñas {#password-scrambler}

La utilidad Password Scrambler cifra una contraseña para que pueda utilizarse en los archivos de configuración de Adobe Access Server for Protected Streaming. Para ejecutar el codificador, ejecute el comando:

```
Scrambler.bat password 
```

o el comando:

```
java -jar libs/flashaccess-scrambler.jar password  
```

La utilidad genera el siguiente mensaje:

```
Encrypted password: scrambled-password 
```

Todas las contraseñas especificadas en flashaccess-global.xml y flashaccess-tenant.xml deben estar cifradas.

>[!NOTE]
>
>La utilidad Password Scrambler de Adobe Access Server para transmisión por secuencias protegida no se puede intercambiar con el codificador que se proporciona con el servidor de licencias de implementación de referencia.
