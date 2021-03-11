---
title: Contenido del paquete
description: Contenido del paquete
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Contenido del paquete{#packaging-content}

Al empaquetar contenido, se debe especificar la URL del servidor de licencias. La URL de Adobe Access Server tiene el formato:

```
http(s):// license-server-host:port/flashaccessserver/tenant-name
```

Por ejemplo, para el nombre de host del servidor de licencias &quot;mylicenciseserver.com&quot; que está escuchando en el puerto 8080 y un inquilino llamado &quot;tenant1&quot;, la URL del servidor de licencias que se debe especificar en el momento del empaquetado es:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Si cada inquilino utiliza un servidor de licencias y una credencial de transporte diferentes, asegúrese de especificar el certificado del inquilino correcto en el empaquetador.

Para garantizar que el servidor envíe licencias solo a contenido empaquetado por paquetes conocidos, incluya el certificado del empaquetador en la lista de permitidos del empaquetador del archivo de configuración del inquilino.
