---
description: Al empaquetar contenido, se debe especificar la URL del servidor de licencias.
title: Empaquetando contenido
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# Empaquetando contenido{#packaging-content}

Al empaquetar contenido, se debe especificar la URL del servidor de licencias.

La URL del servidor DRM de Adobe Primetime utiliza el siguiente formato:

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

Por ejemplo, para el nombre del servidor de licencias `mylicenseserver.com` que escucha en el puerto 8080 y un inquilino llamado *`tenant1`*, utilizaría la siguiente sintaxis para la URL del servidor de licencias que especifique en el momento de empaquetar el contenido:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Si cada usuario utiliza un servidor de licencias y una credencial de transporte diferentes, asegúrese de especificar el certificado del usuario correcto en el empaquetador.

Si desea asegurarse de que el servidor emite licencias únicamente para contenido de empaquetadores conocidos, debe incluir el certificado del empaquetador en la lista de permitidos del empaquetador del archivo de configuración del inquilino.
