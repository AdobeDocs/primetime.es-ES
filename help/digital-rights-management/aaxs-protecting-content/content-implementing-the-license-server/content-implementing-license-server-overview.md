---
title: Información general
description: Información general
copied-description: true
exl-id: 7327386b-e796-4fa5-bda4-cacc612a9d1f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# Información general{#overview}

Para emitir licencias a clientes, debe implementar un servidor de licencias de acceso a Adobe. El servidor de licencias utiliza el Adobe ® Access™ SDK para realizar estas tareas:

* Procesar solicitudes de autenticación si se admite la autenticación de nombre de usuario y contraseña.
* Procesar solicitudes de licencia
* Procesar solicitudes de obtención de versión del servidor: todos los servidores deben implementar la compatibilidad con este tipo de solicitud.
* Procesar solicitudes de registro de dominios: solo es necesario si se implementa un servidor de dominios.
* Procesar solicitudes de anulación de registro de dominios: solo es necesario si se implementa un servidor de dominios.
* Sincronización de procesos: sólo es necesario si las licencias especifican requisitos de sincronización.

Además, el servidor debe proporcionar lógica empresarial para autenticar a los usuarios, determinar si están autorizados a ver contenido y, opcionalmente, rastrear el uso de licencias.

Para obtener más información sobre la API de Java que se analiza en este capítulo, consulte *Referencia de API de acceso de Adobe*.
