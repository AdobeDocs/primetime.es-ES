---
description: Al empaquetar contenido, se debe especificar la URL del servidor de licencias.
title: Empaquetando contenido
exl-id: f82385d5-cdb3-4c24-822e-3fc3c3a0793f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
