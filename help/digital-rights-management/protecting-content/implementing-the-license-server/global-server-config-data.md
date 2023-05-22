---
title: Datos de configuración global del servidor
description: Datos de configuración global del servidor
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Datos de configuración global del servidor{#global-server-configuration-data}

Además de la configuración utilizada por el servidor de licencias, `HandlerConfiguration` almacena información de configuración que se puede enviar al cliente para controlar cómo se aplican las licencias. Esto se hace creando un `ServerConfigData` clase y llamada `HandlerConfiguration.setServerConfigData()`. Esta configuración sólo se aplica a las licencias emitidas por este servidor de licencias.

La tolerancia del reloj contra devoluciones es una propiedad que puede establecer el servidor de licencias para controlar cómo el cliente aplica las licencias. De forma predeterminada, los usuarios pueden retrasar el reloj del equipo 4 horas sin invalidar las licencias. Si un operador de servidor de licencias desea utilizar una configuración diferente, el nuevo valor se puede establecer en la variable `ServerConfigData` clase. Cuando cambie el valor de cualquiera de estas configuraciones, asegúrese de incrementar el número de versión llamando a `setVersion()`. Los nuevos valores solo se envían al cliente si la versión del cliente es anterior a la actual `ServerConfigData` versión.
