---
description: Una forma de coordinar las licencias y la aplicación de políticas es crear estas funciones en un servidor de derechos. Adobe proporciona el servidor de derechos de referencia SEES con el que puede trabajar para crear su propio servidor.
title: Servidor de referencia Servidor de derechos de muestra de ExpressPlay (SEES)
exl-id: aa5b63f4-dffc-4808-8aa6-6b8f63df592c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Servidor de referencia: Servidor de derechos de ExpressPlay de muestra (SEES) {#reference-server-sample-expressplay-entitlement-server-sees}

Una forma de coordinar las licencias y la aplicación de políticas es crear estas funciones en un servidor de derechos. Adobe proporciona el servidor de derechos de referencia SEES con el que puede trabajar para crear su propio servidor.

El servidor de referencia SEES muestra el servicio de derechos de ExpressPlay, que muestra dos servicios: derechos básicos basados en el tiempo y derechos de enlace de dispositivo.

El SEES se basa en dos servicios ExpressPlay Fairplay:

1. Servicio de solicitud de token de ExpressPlay
1. Servicio de recuperación de registros de ExpressDisplay

El formato URL de la solicitud de token de ExpressPlay tiene dos formatos, uno para la producción y otro para el entorno de prueba:

**Producción**: ht<span></span>tps://fp-gen.{prod_domain}/hms/fp/token

**Prueba**: ht<span></span>tps://fp-gen.test.expressplay.com/hms/fp/token

El formato URL para la recuperación de registros ExpressPlay toma dos formas, una para la producción y otra para el entorno de prueba:

**Producción**: ht<span></span>tps://api.{prod_domain}/cmiapi/getrecord/

**Prueba**: ht<span></span>tps://api.test.expressplay.com/cmiapi/getrecord/
