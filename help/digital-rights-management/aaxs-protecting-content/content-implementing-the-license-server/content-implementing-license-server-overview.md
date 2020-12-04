---
seo-title: Información general
title: Información general
uuid: f4ae10ca-6e2a-4313-80a0-4c7377dba000
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# Información general{#overview}

Para emitir licencias a los clientes, debe implementar un servidor de licencias de Adobe Access. El servidor de licencias utiliza el SDK de Adobe® Access™ para realizar estas tareas:

* Procesar solicitudes de autenticación, si se admite la autenticación de nombre de usuario y contraseña.
* Procesar solicitudes de licencia
* Procesar solicitudes Get Server Version: todos los servidores deben implementar la compatibilidad con este tipo de solicitud.
* Procesar solicitudes de registro de dominio: solo es necesario si se implementa un servidor de dominio.
* Procesar solicitudes de anulación del registro de dominio: solo es necesario si se implementa un servidor de dominio.
* Sincronización de procesos: solo se necesita si las licencias especifican los requisitos de sincronización.

Además, el servidor debe proporcionar lógica empresarial para autenticar usuarios, determinar si los usuarios están autorizados para vista de contenido y, opcionalmente, rastrear el uso de licencias.

Para obtener más información sobre la API de Java que se analiza en este capítulo, consulte *Referencia de API de acceso a Adobe*.
