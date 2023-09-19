---
title: Empaquetando contenido
description: Empaquetando contenido
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Empaquetando contenido{#packaging-content}

Al empaquetar contenido, se debe especificar la URL del servidor de licencias. La dirección URL de Adobe Access Server tiene el formato:

```
http(s):// license-server-host:port/flashaccessserver/tenant-name
```

Por ejemplo, para el nombre de host del servidor de licencias &quot;mylicensesServer.com&quot; que escucha en el puerto 8080 y un inquilino denominado &quot;tenant1&quot;, la URL del servidor de licencias que se debe especificar en el momento del empaquetado es:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Si cada inquilino utiliza un servidor de licencias y una credencial de transporte diferentes, asegúrese de especificar el certificado del inquilino correcto en el empaquetado.

Para garantizar que el servidor emita licencias únicamente para contenido empaquetado por empaquetadores conocidos, incluya el certificado del empaquetador en la lista de permitidos del empaquetador del archivo de configuración del inquilino.
