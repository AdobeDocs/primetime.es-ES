---
seo-title: Información general sobre el servidor de licencias
title: Información general sobre el servidor de licencias
uuid: 8c62376b-b159-4297-9322-75d62947e84e
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Información general {#license-server-overview}

Para poder emitir licencias a los clientes, debe implementar un servidor de licencias DRM de Adobe Primetime. El servidor de licencias utiliza el SDK de DRM de Primetime para realizar varias tareas.

Para implementar un servidor de licencias:

* Procesar solicitudes de autenticación, si se admite la autenticación de nombre de usuario y contraseña.
* Procesar solicitudes de licencia
* Procesar solicitudes Get Server Version: todos los servidores deben implementar la compatibilidad con este tipo de solicitud.
* Procesar solicitudes de registro de dominio: solo es necesario si se implementa un servidor de dominio.
* Procesar solicitudes de anulación del registro de dominio: solo es necesario si se implementa un servidor de dominio.
* Sincronización de procesos: solo es necesaria si las licencias especifican los requisitos de sincronización.

Además, el servidor debe proporcionar lógica empresarial para autenticar usuarios, determinar si los usuarios están autorizados para ver contenido y, opcionalmente, rastrear el uso de licencias.

Consulte *Adobe Primetime DRM API Reference* para obtener más información sobre la API de Java.
