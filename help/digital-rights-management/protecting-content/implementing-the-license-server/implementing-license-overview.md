---
title: Resumen del servidor de licencias
description: Resumen del servidor de licencias
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Información general {#license-server-overview}

Para poder emitir licencias a los clientes, debe implementar un servidor de licencias Adobe Primetime DRM. El servidor de licencias utiliza el SDK de DRM de Primetime para realizar varias tareas.

Para implementar un servidor de licencias:

* Procese las solicitudes de autenticación si se admite la autenticación de nombre de usuario y contraseña.
* Procesar solicitudes de licencia
* Procesar Obtener solicitudes de versión del servidor: todos los servidores deben implementar la compatibilidad para este tipo de solicitud.
* Procesar solicitudes de registro de dominio: solo es necesario si se implementa un servidor de dominio.
* Procesar solicitudes de anulación de registro de dominio: solo necesario si se implementa un servidor de dominio.
* Sincronización de procesos: solo es necesaria si las licencias especifican requisitos de sincronización.

Además, el servidor debe proporcionar lógica empresarial para autenticar usuarios, determinar si los usuarios están autorizados a ver contenido y opcionalmente rastrear el uso de licencias.

Consulte *Referencia de la API de Adobe Primetime DRM* para obtener más información sobre la API de Java.
