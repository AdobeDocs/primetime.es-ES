---
title: ¿Qué NO es compatible con Primetime Cloud DRM?
description: ¿Qué NO es compatible con Primetime Cloud DRM?
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---


# ¿Qué NO es compatible con Primetime Cloud DRM{#what-is-not-supported-by-primetime-cloud-drm}?

Primetime Cloud DRM admite casi todas las funciones disponibles actualmente con Primetime DRM. Sin embargo, debido a algunas de las funciones de DRM que requieren la comunicación con el subsistema de reglas comerciales back-end de un cliente, algunas funciones no están disponibles con Primetime Cloud DRM.

Las funciones actualmente no compatibles con el DRM de Primetime Cloud son:

* Contenido empaquetado con un CEK externo (donde el servidor de licencias solicita el CEK del contenido desde un sistema de administración de claves externas)
* Dominios de dispositivo
* Encadenado de licencias avanzado
* Regreso/revocación de la licencia
* PHLS/PHDS. Estos son esquemas de protección que no utilizan un servidor de licencias
* Autenticación de usuario/contraseña

