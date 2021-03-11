---
description: Al empaquetar contenido, debe especificar la URL del servidor de licencias.
title: Contenido del paquete
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# Contenido del paquete{#packaging-content}

Al empaquetar contenido, debe especificar la URL del servidor de licencias.

La URL del servidor Adobe Primetime DRM utiliza el siguiente formato:

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

Por ejemplo, para el nombre de host del servidor de licencias `mylicenseserver.com` que escucha en el puerto 8080 y un inquilino llamado *`tenant1`*, debe utilizar la siguiente sintaxis para la URL del servidor de licencias que especifique en el momento en que empaqueta el contenido:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Si cada inquilino utiliza un servidor de licencias y una credencial de transporte diferentes, asegúrese de especificar el certificado del inquilino correcto en el empaquetador.

Si desea asegurarse de que el servidor emite licencias solo para contenido de paquetes conocidos, debe incluir el certificado del empaquetador en la lista de permitidos del empaquetador del archivo de configuración del inquilino.
