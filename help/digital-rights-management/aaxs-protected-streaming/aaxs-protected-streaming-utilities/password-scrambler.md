---
title: Descodificador de contraseñas
description: Descodificador de contraseñas
copied-description: true
exl-id: ceedd61e-918b-453f-8d21-628b2d8713ff
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
