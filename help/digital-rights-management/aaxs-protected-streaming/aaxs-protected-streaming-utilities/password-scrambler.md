---
title: Contraseña Scrambler
description: Contraseña Scrambler
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---


# Contraseña Scrambler {#password-scrambler}

La utilidad Password Scrambler cifra una contraseña para que se pueda utilizar en los archivos de configuración de Adobe Access Server para transmisión protegida. Para ejecutar el reproductor, ejecute el comando:

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

Todas las contraseñas especificadas en flashaccess-global.xml y flashaccess-tenant.xml deben cifrarse.

>[!NOTE]
>
>La utilidad Password Scrambler de Adobe Access Server para transmisión protegida no es intercambiable con el codificador que se proporciona con el servidor de licencias de implementación de referencia.

