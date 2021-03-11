---
title: Requisitos para el uso de Primetime DRM Key Server
description: Requisitos para el uso de Primetime DRM Key Server
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# Introducción {#introduction}

Primetime DRM Key Server es un servidor de claves multiinquilino para iOS remoto y / o entrega de claves Xbox 360. Si la entrega de claves remotas está habilitada en una directiva para iOS, se debe implementar un servidor de claves DRM de Primetime para habilitar la reproducción de contenido en clientes iOS. El servidor de claves DRM de Primetime siempre es necesario para Xbox 360.

## Requisitos para utilizar el servidor de claves DRM de Primetime {#requirements-for-using-primetime-drm-key-server}

Los requisitos mínimos para utilizar el servidor de claves DRM de Primetime son:

* [Java JRE 1.6](https://www.oracle.com/technetwork/java/javase/downloads/index.html) o posterior. (Para utilizar HSM en Windows de 64 bits, se requiere JRE 8)

   >[!NOTE]
   >
   >El PKCS11 de 64 bits ahora es compatible con OpenJDK 8: [https://openjdk.java.net/jeps/131](https://openjdk.java.net/jeps/131) y Oracle JDK: [https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559](https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559).

* [Apache Tomcat 7](https://tomcat.apache.org)
* Credenciales expedidas por el Adobe
* Credenciales emitidas por Microsoft (para clientes de Xbox 360)