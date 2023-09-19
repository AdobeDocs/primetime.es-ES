---
title: Introducción al servidor de licencias
description: Introducción al servidor de licencias
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Información general {#license-server-overview}

Para poder emitir licencias a clientes de, debe implementar un servidor de licencias DRM de Adobe Primetime. El servidor de licencias utiliza el SDK de DRM de Primetime para realizar diversas tareas.

Para implementar un servidor de licencias:

* Procesar solicitudes de autenticación si se admite la autenticación de nombre de usuario y contraseña.
* Procesar solicitudes de licencia
* Procesar solicitudes de obtención de versión del servidor: todos los servidores deben implementar la compatibilidad con este tipo de solicitud.
* Procesar solicitudes de registro de dominios: solo es necesario si se implementa un servidor de dominios.
* Procesar solicitudes de anulación de registro de dominios: solo es necesario si se implementa un servidor de dominios.
* Sincronización de procesos: solo es necesario si las licencias especifican requisitos de sincronización.

Además, el servidor debe proporcionar lógica empresarial para autenticar a los usuarios, determinar si están autorizados a ver contenido y, opcionalmente, rastrear el uso de licencias.

Consulte *Referencia de API de DRM de Adobe Primetime* para obtener más información sobre la API de Java.
