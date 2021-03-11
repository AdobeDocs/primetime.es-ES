---
title: Información general
description: Información general
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# Información general{#overview}

Para emitir licencias a los clientes, debe implementar un servidor de licencias de acceso a Adobe. El servidor de licencias utiliza el SDK de Adobe® Access™ para realizar estas tareas:

* Procese las solicitudes de autenticación si se admite la autenticación de nombre de usuario y contraseña.
* Procesar solicitudes de licencia
* Procesar Obtener solicitudes de versión del servidor: todos los servidores deben implementar la compatibilidad para este tipo de solicitud.
* Procesar solicitudes de registro de dominio: solo es necesario si se implementa un servidor de dominio.
* Procesar solicitudes de anulación de registro de dominio: solo necesario si se implementa un servidor de dominio.
* Sincronización de procesos: solo es necesaria si las licencias especifican requisitos de sincronización.

Además, el servidor debe proporcionar lógica empresarial para autenticar usuarios, determinar si los usuarios están autorizados a ver contenido y opcionalmente rastrear el uso de licencias.

Para obtener más información sobre la API de Java que se describe en este capítulo, consulte *Referencia de la API de acceso a Adobe*.
