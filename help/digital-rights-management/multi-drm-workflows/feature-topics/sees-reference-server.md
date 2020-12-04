---
description: Una manera de coordinar la aplicación de políticas y licencias es crear estas funciones en un servidor de asignación de derechos. Adobe proporciona el servidor de asignación de derechos de referencia SEES con el que puede trabajar para crear su propio servidor.
seo-description: Una manera de coordinar la aplicación de políticas y licencias es crear estas funciones en un servidor de asignación de derechos. Adobe proporciona el servidor de asignación de derechos de referencia SEES con el que puede trabajar para crear su propio servidor.
seo-title: Servidor de referencia Muestra de ExpressPlay Entitlement Server (SEES)
title: Servidor de referencia Muestra de ExpressPlay Entitlement Server (SEES)
uuid: 99e42f76-7730-42fc-a9a9-f6396ac12c02
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Servidor de referencia: Ejemplo de ExpressPlay Entitlement Server (SEES) {#reference-server-sample-expressplay-entitlement-server-sees}

Una manera de coordinar la aplicación de políticas y licencias es crear estas funciones en un servidor de asignación de derechos. Adobe proporciona el servidor de asignación de derechos de referencia SEES con el que puede trabajar para crear su propio servidor.

El servidor de referencia SEES muestra el servicio de asignación de derechos ExpressPlay, mostrando dos servicios: asignación de derechos básica basada en el tiempo y asignación de derechos de enlace del dispositivo.

El SEES está construido sobre dos servicios ExpressPlay Fairplay:

1. Servicio de solicitud de token de Expressplay
1. Servicio de recuperación de registros de expresión

El formato de URL de la solicitud de token de ExpressPlay consta de dos formularios, uno para producción y otro para el entorno de prueba:

**Producción**: <span></span>https://fp-gen.{prod_domain}/hms/fp/token

**Prueba**: <span></span>https://fp-gen.test.expressplay.com/hms/fp/token

El formato de URL para la recuperación de registros ExpressPlay tiene dos formularios, uno para producción y otro para el entorno de prueba:

**Producción**: <span></span>https://api.{prod_domain}/cmiapi/getrecord/

**Prueba**: <span></span>https://api.test.expressplay.com/cmiapi/getrecord/
