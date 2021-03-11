---
title: Datos de configuración del servidor global
description: Datos de configuración del servidor global
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Datos de configuración del servidor global{#global-server-configuration-data}

Además de la configuración utilizada por el servidor de licencias, `HandlerConfiguration` almacena información de configuración que se puede enviar al cliente para controlar cómo se aplican las licencias. Esto se hace creando una clase `ServerConfigData` y llamando a `HandlerConfiguration.setServerConfigData()`. Esta configuración solo se aplica a las licencias emitidas por este servidor de licencias.

La tolerancia a la ventana del reloj es una propiedad que puede establecer el servidor de licencias para controlar cómo el cliente aplica las licencias. De forma predeterminada, los usuarios pueden retrasar el reloj del equipo 4 horas sin invalidar las licencias. Si un operador de servidor de licencias desea utilizar una configuración diferente, el nuevo valor se puede configurar en la clase `ServerConfigData`. Cuando cambie el valor de cualquiera de estas configuraciones, asegúrese de aumentar el número de versión llamando a `setVersion()`. Los nuevos valores solo se envían al cliente si la versión del cliente es anterior a la versión actual `ServerConfigData`.
