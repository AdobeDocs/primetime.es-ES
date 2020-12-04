---
seo-title: Datos de configuración del servidor global
title: Datos de configuración del servidor global
uuid: f6d6cb01-2645-4cd2-83ec-0272323a67cd
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# Datos de configuración del servidor global{#global-server-configuration-data}

Además de la configuración utilizada por el servidor de licencias, `HandlerConfiguration` almacena información de configuración que se puede enviar al cliente para controlar cómo se aplican las licencias. Esto se lleva a cabo creando una clase `ServerConfigData` y llamando a `HandlerConfiguration.setServerConfigData()` (esta configuración solo se aplica a las licencias emitidas por este servidor de licencias). La tolerancia a la parabrisas del reloj es una propiedad que puede establecer el servidor de licencias para controlar cómo el cliente aplica las licencias. De forma predeterminada, los usuarios pueden retrasar 4 horas el reloj del equipo sin invalidar las licencias. Si un operador de servidor de licencias desea utilizar una configuración diferente, el nuevo valor se puede establecer en la clase `ServerConfigData`. Cuando cambie el valor de cualquiera de estas opciones de configuración, asegúrese de incrementar el número de versión llamando a `setVersion()`. Los nuevos valores sólo se enviarán al cliente si la versión del cliente es menor que la versión actual `ServerConfigData`.
