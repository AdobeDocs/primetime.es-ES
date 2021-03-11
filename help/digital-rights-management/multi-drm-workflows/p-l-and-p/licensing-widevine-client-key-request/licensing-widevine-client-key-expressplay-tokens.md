---
description: Puede generar tokens de Expressplay para su contenido cifrado enviando solicitudes de token al servidor de token de Expressplay adecuado.
title: Expresiones de tokens
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---


# Expresiones de tokens {#expressplay-tokens}

Puede generar tokens de Expressplay para su contenido cifrado enviando solicitudes de token al servidor de token de Expressplay adecuado.

Por ejemplo, la siguiente URL:

```
https://wv-gen.service.expressplay.com/hms/wv/
token?customerAuthenticator=<your expressplay customer authenticator>
&kid=fd1a706ac2b36002888f6d4a414333c3
&contentKey=5438b719bf47a2f5678237477db2f9e6
&securityLevel=1
&hdcpOutputControl=0
```

El ID de almacenamiento de la clave de cifrado de contenido o CEKSID proporcionado al parámetro `kid` y la clave de cifrado de contenido o CEK proporcionada al parámetro `contentKey` deben coincidir con el ID de almacenamiento de la clave de cifrado de contenido y la clave de cifrado de contenido utilizada para el empaquetado. El siguiente texto es un ejemplo de la respuesta del servidor token:

```
https://wv.service.expressplay.com/hms/wv/rights/
?ExpressPlayToken=AQAAABIDKbgAAABQbt68jktab0YRY-r9mo6VP
 VqDDvkHq78x4V9_AyBUTtcNFHw5JtNKlKrMt-4HBdJ3Fopr7fqFSBp
 SJ4o-d8teAkUZUtW3Od5V-SHsCLnAlbFW84K71h2xNUiMAvRcUFBG3bjxMQ
```

Entonces puede:

* utilice la URL y la consulta devueltas como URL del servidor de licencias, o
* extraer la consulta de la dirección URL y pasar el ExpressPlayToken por separado como encabezado de POST HTTP