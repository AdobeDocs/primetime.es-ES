---
title: Revocación de las credenciales de tiempo de ejecución y cliente de DRM
description: Revocación de las credenciales de tiempo de ejecución y cliente de DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# Revocación de las credenciales de cliente y de tiempo de ejecución de DRM {#revoking-drm-client-and-runtime-credentials}

Las versiones de DRM/Runtime se identifican por nivel de seguridad, número de versión y otros atributos, incluidos el sistema operativo y el tiempo de ejecución. Para restringir las versiones de DRM/Runtime permitidas, establezca las restricciones de módulo en una directiva de DRM o en un `HandlerConfiguration`. Las restricciones de módulos pueden incluir un nivel mínimo de seguridad y una lista de versiones de módulos a las que no se permite expedir una licencia.

Consulte [Lista de bloqueados de clientes DRM restringidos para acceder a contenido protegido](../../protecting-content/introduction/usage-rules/runtime-application-restrictions/blocklist-drm-clients.md) para obtener más información sobre los atributos utilizados para identificar un módulo DRM/Runtime.

Si se establece el nivel de seguridad mínimo, la versión del cliente (especificada en el token del equipo) debe ser buena o igual al valor especificado.

Si se especifica una lista de versiones excluidas y la versión del cliente coincide con cualquiera de los identificadores de versión de la lista, no se permitirá al cliente utilizar un derecho que contenga esta instancia ModuleRequirements. Para que un módulo coincida con la información de la versión, todos los parámetros especificados en la información de la versión, excepto la versión de la versión, deben coincidir exactamente con los valores de los módulos. La versión de la versión coincide si el valor del módulo del cliente es menor o igual que el valor de la información de la versión.

En caso de que se informe de una infracción con un cliente DRM o una versión de tiempo de ejecución en particular, el propietario del contenido y el distribuidor de contenido (que ejecuta el servidor de licencias) pueden configurar el servidor para que rechace la emisión de licencias durante un periodo en el que el Adobe no tenga una corrección disponible. Esto se puede configurar a través de `HandlerConfiguration` como se ha descrito anteriormente, o realizando cambios en todas las políticas de DRM. En este último caso, puede mantener una lista de actualización de directivas de DRM y utilizarla para comprobar si una directiva de DRM se ha actualizado o revocado.

Si necesita una versión más reciente del Flash Player de Adobe/Adobe AIR Runtime o de la biblioteca de protección de contenido de Adobe (módulo DRM), debe actualizar sus políticas de DRM.

Consulte [Actualización de una directiva mediante la API de Java](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md).

A continuación, debe crear una lista de actualización de directivas de DRM o establecer restricciones en `HandlerConfiguration` invocando `HandlerConfiguration.setRuntimeModuleRequirements()` o `HandlerConfiguration.setDRMModuleRequirements()`. Cuando un usuario solicita una licencia nueva con las listas de bloqueados especificadas activadas, debe instalar los últimos tiempos de ejecución y bibliotecas antes de que se pueda emitir una licencia.

Consulte el código de ejemplo en [Actualización de una directiva mediante la API de Java Para ver un ejemplo sobre la lista de bloqueados de versiones de DRM y tiempo de ejecución](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md) para ver un ejemplo sobre la lista de bloqueados de versiones de DRM y de tiempo de ejecución.
