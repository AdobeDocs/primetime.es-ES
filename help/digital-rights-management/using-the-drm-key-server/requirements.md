---
seo-title: Requisitos para utilizar Primetime DRM Key Server
title: Requisitos para utilizar Primetime DRM Key Server
uuid: 769f9e10-7a3e-4a38-b30d-18181b666bb4
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# Introducción {#introduction}

Primetime DRM Key Server es un servidor de claves de varios inquilinos para iOS remoto y/o envío de claves Xbox 360. Si el Envío de clave remota está habilitado en una directiva para iOS, se debe implementar un servidor de claves DRM Primetime para habilitar la reproducción de contenido en clientes iOS. Primetime DRM Key Server siempre es necesario para Xbox 360.

## Requisitos para utilizar Primetime DRM Key Server {#requirements-for-using-primetime-drm-key-server}

Los requisitos mínimos para utilizar Primetime DRM Key Server son:

* [Java JRE 1.6](https://www.oracle.com/technetwork/java/javase/downloads/index.html) o posterior. (Para utilizar HSM en Windows de 64 bits, se requiere JRE 8)

   >[!NOTE]
   >
   >Ahora se admite PKCS11 de 64 bits en OpenJDK 8: [https://openjdk.java.net/jeps/131](https://openjdk.java.net/jeps/131) y Oracle JDK: [https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559](https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559).

* [Apache Tomcat 7](https://tomcat.apache.org)
* Credenciales expedidas por el Adobe
* Credenciales emitidas por Microsoft (para clientes de Xbox 360)