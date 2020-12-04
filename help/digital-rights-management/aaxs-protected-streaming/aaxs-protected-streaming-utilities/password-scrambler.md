---
seo-title: Contraseña Scrambler
title: Contraseña Scrambler
uuid: e488babc-cd50-41b9-acb8-490e8e42e8bc
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---


# Contraseña Scrambler {#password-scrambler}

La utilidad Password Scrambler cifra una contraseña para que pueda utilizarse en los archivos de configuración de Adobe Access Server para el flujo protegido. Para ejecutar el codificador, ejecute el comando:

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

Todas las contraseñas especificadas en flashaccess-global.xml y flashaccess-inquilino.xml deben cifrarse.

>[!NOTE]
>
>La utilidad Password Scrambler de Adobe Access Server for Protected Streaming no es intercambiable con el codificador proporcionado con el servidor de licencias de implementación de referencia.

