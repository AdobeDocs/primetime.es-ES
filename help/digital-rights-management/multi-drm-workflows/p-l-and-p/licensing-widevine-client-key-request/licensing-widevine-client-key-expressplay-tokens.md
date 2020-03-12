---
description: Puede generar tokens de Expressplay para su contenido cifrado enviando solicitudes de token al servidor de autentificador de Expressplay adecuado.
seo-description: Puede generar tokens de Expressplay para su contenido cifrado enviando solicitudes de token al servidor de autentificador de Expressplay adecuado.
seo-title: Tokens de Expressplay
title: Tokens de Expressplay
uuid: 6103e1b2-127d-4758-a589-15f0f3c73db1
translation-type: tm+mt
source-git-commit: d0ba1f98b16f6350ae842ca2ce1261bf49dd8a66

---


# Tokens de Expressplay {#expressplay-tokens}

Puede generar tokens de Expressplay para su contenido cifrado enviando solicitudes de token al servidor de autentificador de Expressplay adecuado.

Un ejemplo es la siguiente dirección URL:

```
https://wv-gen.service.expressplay.com/hms/wv/
token?customerAuthenticator=<your expressplay customer authenticator>
&kid=fd1a706ac2b36002888f6d4a414333c3
&contentKey=5438b719bf47a2f5678237477db2f9e6
&securityLevel=1
&hdcpOutputControl=0
```

El ID de almacenamiento de la clave de cifrado de contenido o CEKSID otorgado al `kid` parámetro y la clave de cifrado de contenido o CEK otorgada al `contentKey` parámetro deben coincidir con el ID de almacenamiento de la clave de cifrado de contenido y la clave de cifrado de contenido utilizada para el empaquetado. El siguiente texto es un ejemplo de la respuesta del servidor de tokens:

```
https://wv.service.expressplay.com/hms/wv/rights/
?ExpressPlayToken=AQAAABIDKbgAAABQbt68jktab0YRY-r9mo6VP
 VqDDvkHq78x4V9_AyBUTtcNFHw5JtNKlKrMt-4HBdJ3Fopr7fqFSBp
 SJ4o-d8teAkUZUtW3Od5V-SHsCLnAlbFW84K71h2xNUiMAvRcUFBG3bjxMQ
```

A continuación, puede

* utilice la dirección URL y la consulta devueltas como dirección URL del servidor de licencias, o
* saque la consulta de la dirección URL y pase el ExpressPlayToken por separado como encabezado HTTP POST