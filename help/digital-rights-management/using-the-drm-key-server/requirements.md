---
title: Requisitos para utilizar el servidor de claves DRM de Primetime
description: Requisitos para utilizar el servidor de claves DRM de Primetime
copied-description: true
exl-id: a5c0db05-15a1-45b0-abb9-11f857f5e34c
source-git-commit: 1bc2f6c230c262babf2958c32fee31afcad04c2f
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# Introducción {#introduction}

El servidor de claves DRM de Primetime es un servidor de claves de varios inquilinos para la entrega de claves de Xbox 360 o iOS remoto. Si la entrega de claves remotas está activada en una directiva para iOS, se debe implementar un servidor de claves DRM de Primetime para habilitar la reproducción de contenido en clientes de iOS. El servidor de claves DRM de Primetime siempre es necesario para Xbox 360.

## Requisitos para utilizar el servidor de claves DRM de Primetime {#requirements-for-using-primetime-drm-key-server}

Los requisitos mínimos para utilizar el servidor de claves DRM de Primetime son:

* [Java JRE 1.6](https://www.oracle.com/technetwork/java/javase/downloads/index.html) o más tarde. (Para utilizar HSM en Windows de 64 bits, se requiere JRE 8)

  >[!NOTE]
  >
  >PKCS11 de 64 bits ahora es compatible con OpenJDK 8: [https://openjdk.java.net/jeps/131](https://openjdk.java.net/jeps/131), y ORACLE
* [Apache Tomcat 7](https://tomcat.apache.org)
* Credenciales emitidas por Adobe
* Credenciales emitidas por Microsoft (para clientes Xbox 360)
