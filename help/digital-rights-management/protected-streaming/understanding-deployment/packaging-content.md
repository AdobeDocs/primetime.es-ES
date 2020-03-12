---
description: Al empaquetar contenido, debe especificar la URL del servidor de licencias.
seo-description: Al empaquetar contenido, debe especificar la URL del servidor de licencias.
seo-title: Empaquetado de contenido
title: Empaquetado de contenido
uuid: 2e47a9a2-bbc6-4995-8ce5-6ca6b116349b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Empaquetado de contenido{#packaging-content}

Al empaquetar contenido, debe especificar la URL del servidor de licencias.

La URL del servidor DRM de Adobe Primetime utiliza el siguiente formato:

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

Por ejemplo, para el nombre de host del servidor de licencias `mylicenseserver.com` que escucha en el puerto 8080 y un inquilino llamado *`tenant1`*, debe utilizar la siguiente sintaxis para la URL del servidor de licencias que especifique en el momento en que empaqueta el contenido:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Si cada inquilino utiliza un servidor de licencias y una credencial de transporte diferentes, asegúrese de especificar el certificado del inquilino correcto en el empaquetador.

Si desea asegurarse de que el servidor emite licencias solo para el contenido de los empaquetadores conocidos, debe incluir el certificado del empaquetador en la lista blanca del empaquetador del archivo de configuración del inquilino.
