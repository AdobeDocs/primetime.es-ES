---
seo-title: Datos de configuración del servidor global
title: Datos de configuración del servidor global
uuid: a1557b3e-9a08-4623-a62d-8ebc308eae15
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Datos de configuración del servidor global{#global-server-configuration-data}

Además de la configuración utilizada por el servidor de licencias, `HandlerConfiguration` almacena información de configuración que se puede enviar al cliente para controlar cómo se aplican las licencias. Esto se realiza creando una `ServerConfigData` clase y llamando `HandlerConfiguration.setServerConfigData()`. Esta configuración solo se aplica a las licencias emitidas por este servidor de licencias.

La tolerancia a la parabrisas del reloj es una propiedad que puede establecer el servidor de licencias para controlar cómo el cliente aplica las licencias. De forma predeterminada, los usuarios pueden retrasar 4 horas el reloj del equipo sin invalidar las licencias. Si un operador de servidor de licencias desea utilizar una configuración diferente, el nuevo valor se puede establecer en la `ServerConfigData` clase. Cuando cambie el valor de cualquiera de estas opciones de configuración, asegúrese de incrementar el número de versión llamando a `setVersion()`. Los nuevos valores solo se envían al cliente si la versión del cliente es anterior a la `ServerConfigData` versión actual.
