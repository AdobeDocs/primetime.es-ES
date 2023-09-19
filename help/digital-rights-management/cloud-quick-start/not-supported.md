---
title: Qué NO es compatible con Primetime Cloud DRM
description: Qué NO es compatible con Primetime Cloud DRM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Qué NO es compatible con Primetime Cloud DRM{#what-is-not-supported-by-primetime-cloud-drm}

Primetime Cloud DRM admite casi todas las funciones disponibles actualmente con Primetime DRM. Sin embargo, debido a algunas de las funciones de DRM que requieren comunicación con el subsistema de reglas empresariales back-end de un cliente, algunas funciones no están disponibles con Primetime Cloud DRM.

Las funciones que actualmente no admite Primetime Cloud DRM son:

* Contenido empaquetado con una CEK externa (donde el servidor de licencias solicita la CEK del contenido desde un sistema de administración de claves externo)
* Dominios de dispositivo
* Encadenamiento de licencias avanzado
* Devolución/revocación de la licencia
* PHLS/PHDS. Son esquemas de protección que no utilizan un servidor de licencias
* Autenticación de usuario/contraseña
