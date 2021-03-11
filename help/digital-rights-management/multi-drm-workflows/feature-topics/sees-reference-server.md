---
description: Una forma de coordinar la concesión de licencias y la aplicación de políticas es crear estas funciones en un servidor de autorizaciones. Adobe proporciona el servidor de autorizaciones de referencia SEES con el que puede trabajar para crear su propio servidor.
title: Servidor de referencia Muestra ExpressPlay Servidor de Derechos (SEES)
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Servidor de referencia: Servidor de derechos ExpressPlay de muestra (SEES) {#reference-server-sample-expressplay-entitlement-server-sees}

Una forma de coordinar la concesión de licencias y la aplicación de políticas es crear estas funciones en un servidor de autorizaciones. Adobe proporciona el servidor de autorizaciones de referencia SEES con el que puede trabajar para crear su propio servidor.

El servidor de referencia SEES muestra el servicio de derechos de ExpressPlay, mostrando dos servicios: derecho básico basado en el tiempo y derecho de enlace del dispositivo.

El SEES está construido sobre dos servicios ExpressPlay Fairplay:

1. Servicio de solicitud de tokens de Expression
1. Servicio de recuperación de registros de expresión

El formato URL de la solicitud de token ExpressPlay adopta dos formas, una para la producción y otra para el entorno de prueba:

**Producción**: <span></span>https://fp-gen.{prod_domain}/hms/fp/token

**Prueba**: <span></span>https://fp-gen.test.expressplay.com/hms/fp/token

El formato de URL para la recuperación de registros ExpressPlay toma dos formularios, uno para la producción y otro para el entorno de prueba:

**Producción**: <span></span>https://api.{prod_domain}/cmiapi/getrecord/

**Prueba**: <span></span>https://api.test.expressplay.com/cmiapi/getrecord/
