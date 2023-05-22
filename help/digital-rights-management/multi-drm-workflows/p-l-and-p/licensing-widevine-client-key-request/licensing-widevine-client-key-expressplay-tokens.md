---
description: Puede generar tokens de Expressplay para su contenido cifrado enviando solicitudes de token al servidor de tokens de Expressplay correspondiente.
title: Mostrar tokens
exl-id: 38faba06-6737-4dec-ac97-27db3124b993
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# Mostrar tokens {#expressplay-tokens}

Puede generar tokens de Expressplay para su contenido cifrado enviando solicitudes de token al servidor de tokens de Expressplay correspondiente.

Un ejemplo es la siguiente URL:

```
https://wv-gen.service.expressplay.com/hms/wv/
token?customerAuthenticator=<your expressplay customer authenticator>
&kid=fd1a706ac2b36002888f6d4a414333c3
&contentKey=5438b719bf47a2f5678237477db2f9e6
&securityLevel=1
&hdcpOutputControl=0
```

El ID de almacenamiento de la clave de cifrado de contenido o CEKSID dado al `kid` y la clave de cifrado de contenido o CEK dada al parámetro `contentKey` El parámetro debe coincidir con el ID de almacenamiento de la clave de cifrado de contenido y la clave de cifrado de contenido utilizada para el empaquetado. El siguiente texto es un ejemplo de la respuesta del servidor de tokens:

```
https://wv.service.expressplay.com/hms/wv/rights/
?ExpressPlayToken=AQAAABIDKbgAAABQbt68jktab0YRY-r9mo6VP
 VqDDvkHq78x4V9_AyBUTtcNFHw5JtNKlKrMt-4HBdJ3Fopr7fqFSBp
 SJ4o-d8teAkUZUtW3Od5V-SHsCLnAlbFW84K71h2xNUiMAvRcUFBG3bjxMQ
```

A continuación, puede hacer lo siguiente

* usar la URL devuelta y la consulta como URL del servidor de licencias, o
* elimine la consulta de la dirección URL y pase el ExpressPlayToken por separado como encabezado de POST HTTP
