---
title: Revocar credenciales de tiempo de ejecución y cliente DRM
description: Revocar credenciales de tiempo de ejecución y cliente DRM
copied-description: true
exl-id: 3a91a256-ab01-48d8-99f3-854195faae6f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Revocar credenciales de tiempo de ejecución y cliente DRM {#revoking-drm-client-and-runtime-credentials}

Las versiones de DRM/Runtime se identifican por nivel de seguridad, número de versión y otros atributos, incluidos el sistema operativo y el tiempo de ejecución. Para restringir las versiones de DRM/Runtime permitidas, defina las restricciones de módulo en una directiva DRM o en un `HandlerConfiguration`. Las restricciones de módulos pueden incluir un nivel de seguridad mínimo y una lista de versiones de módulos a las que no se permite expedir una licencia.

Consulte [Lista de bloqueados de clientes DRM con acceso restringido a contenido protegido](../../protecting-content/introduction/usage-rules/runtime-application-restrictions/blocklist-drm-clients.md) para obtener más información sobre los atributos utilizados para identificar un módulo DRM/Runtime.

Si se establece el nivel de seguridad mínimo, la versión del cliente (especificada en el token del equipo) debe ser buena o igual al valor especificado.

Si se especifica una lista de versiones excluidas y la versión del cliente coincide con cualquiera de los identificadores de versión de la lista, no se permitirá al cliente utilizar un derecho que contenga esta instancia ModuleRequirements. Para que un módulo coincida con la información de la versión, todos los parámetros especificados en la información de la versión, excepto la versión de la versión, deben coincidir exactamente con los valores de los módulos. La versión de la versión coincide si el valor del módulo de cliente es menor o igual que el valor de la información de la versión.

En caso de que se informe de una infracción con un cliente DRM o una versión de tiempo de ejecución determinados, el propietario del contenido y el distribuidor de contenido (que ejecuta el servidor de licencias) pueden configurar el servidor para que rechace la emisión de licencias durante un periodo en el que el Adobe no tenga una corrección disponible. Esto se puede configurar mediante las opciones `HandlerConfiguration` como se ha descrito anteriormente, o realizando cambios en todas las políticas de DRM. En este último caso, se puede mantener una lista de actualización de directivas DRM y utilizarla para comprobar si una directiva DRM se ha actualizado o revocado.

Si necesita una versión más reciente del Flash Player de Adobe/Adobe AIR Runtime o la biblioteca de protección de contenido de Adobe (módulo DRM), debe actualizar las directivas de DRM.

Consulte [Actualización de una directiva mediante la API de Java](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md).

A continuación, debe crear una Lista de actualización de directivas DRM o establecer restricciones en `HandlerConfiguration` invocando `HandlerConfiguration.setRuntimeModuleRequirements()` o `HandlerConfiguration.setDRMModuleRequirements()`. Cuando un usuario solicita una nueva licencia con las listas de bloqueados especificadas habilitadas, debe instalar los tiempos de ejecución y las bibliotecas más recientes para poder emitir una licencia.

Consulte el código de ejemplo en [Actualización de una directiva mediante la API de Java Para ver un ejemplo sobre la lista de bloqueados de versiones de tiempo de ejecución y DRM](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md) para ver un ejemplo sobre la lista de bloqueados de versiones de DRM y de tiempo de ejecución.
