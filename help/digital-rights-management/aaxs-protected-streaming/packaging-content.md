---
seo-title: Empaquetado de contenido
title: Empaquetado de contenido
uuid: 5d1d4b9d-f241-4291-9577-e9de5a8b92be
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9

---


# Empaquetado de contenido{#packaging-content}

Al empaquetar contenido, se debe especificar la dirección URL del servidor de licencias. La URL de Adobe Access Server tiene el formato:

```
http(s):// license-server-host:port/flashaccessserver/tenant-name
```

Por ejemplo, para la escucha del nombre de host del servidor de licencias &quot;mylicenciseserver.com&quot; en el puerto 8080 y un inquilino llamado &quot;inquilino1&quot;, la dirección URL del servidor de licencias que se debe especificar en el momento del empaquetado es:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Si cada inquilino utiliza un servidor de licencias y una credencial de transporte diferentes, asegúrese de especificar el certificado del inquilino correcto en el empaquetador.

Para asegurarse de que el servidor emite licencias solo para contenido empaquetado por los empaquetadores conocidos, incluya el certificado del empaquetador en la lista blanca del empaquetador del archivo de configuración del inquilino.
