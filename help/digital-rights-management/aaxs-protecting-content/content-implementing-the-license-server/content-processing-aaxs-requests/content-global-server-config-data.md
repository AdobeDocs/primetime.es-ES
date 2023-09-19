---
title: Datos de configuración global del servidor
description: Datos de configuración global del servidor
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---

# Datos de configuración global del servidor{#global-server-configuration-data}

Además de la configuración utilizada por el servidor de licencias, `HandlerConfiguration` almacena información de configuración que se puede enviar al cliente para controlar cómo se aplican las licencias. Esto se hace creando un `ServerConfigData` clase y llamada `HandlerConfiguration.setServerConfigData()` (esta configuración sólo se aplica a las licencias emitidas por este servidor de licencias). La tolerancia del reloj contra devoluciones es una propiedad que puede establecer el servidor de licencias para controlar cómo el cliente aplica las licencias. De forma predeterminada, los usuarios pueden retrasar el reloj del equipo 4 horas sin invalidar las licencias. Si un operador de servidor de licencias desea utilizar una configuración diferente, el nuevo valor se puede establecer en la variable `ServerConfigData` clase. Cuando cambie el valor de cualquiera de estas configuraciones, asegúrese de incrementar el número de versión llamando a `setVersion()`. Los nuevos valores solo se enviarán al cliente si la versión del cliente es menor que la actual `ServerConfigData` versión.
