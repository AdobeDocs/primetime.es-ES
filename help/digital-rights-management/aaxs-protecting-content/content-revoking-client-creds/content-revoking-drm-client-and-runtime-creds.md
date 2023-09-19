---
title: Revocar credenciales de tiempo de ejecución y cliente DRM
description: Revocar credenciales de tiempo de ejecución y cliente DRM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Revocar credenciales de tiempo de ejecución y cliente DRM{#revoking-drm-client-and-runtime-credentials}

Las versiones de DRM/Runtime se identifican por nivel de seguridad, número de versión y otros atributos, incluidos el sistema operativo y el tiempo de ejecución. Para restringir las versiones de DRM/Runtime permitidas, establezca las restricciones de módulo en una directiva o en una `HandlerConfiguration`. Las restricciones de módulos pueden incluir un nivel de seguridad mínimo y una lista de versiones de módulos a las que no se permite expedir una licencia. Consulte [Lista de bloqueados de clientes DRM con acceso restringido a contenido protegido](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-blocklist-drm-clients.md) para obtener más información sobre los atributos utilizados para identificar un módulo DRM/Runtime.

Si se establece el nivel de seguridad mínimo, la versión del cliente (especificada en el token del equipo) debe ser mayor o igual que el valor especificado.

Si se especifica una lista de versiones excluidas y la versión del cliente coincide con cualquiera de los identificadores de versión de la lista, no se permitirá al cliente utilizar un derecho que contenga esta instancia ModuleRequirements. Para que un módulo coincida con la información de la versión, todos los parámetros especificados en la información de la versión, excepto la versión de la versión, deben coincidir exactamente con los valores de los módulos. La versión de la versión coincide si el valor del módulo de cliente es menor o igual que el valor de la información de la versión.

En caso de que se informe de una infracción con un cliente DRM o una versión de tiempo de ejecución determinados, el propietario del contenido y el distribuidor de contenido (que ejecuta el servidor de licencias) pueden configurar el servidor para que rechace la emisión de licencias durante un periodo en el que el Adobe no tenga una corrección disponible. Esto se puede configurar mediante las opciones `HandlerConfiguration` como se ha descrito anteriormente, o realizando cambios en todas las directivas. En este último caso, puede mantener una lista de actualización de directivas y utilizarla para comprobar si una directiva se ha actualizado o revocado.

Si necesita una versión más reciente de Adobe® Flash® Player/Adobe® AIR® Runtime o la biblioteca de protección de contenido de Adobe (módulo DRM), actualice las directivas como se muestra en [Actualización de una directiva mediante la API de Java](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md) y cree una Lista de actualización de directivas o establezca restricciones en `HandlerConfiguration` invocando `HandlerConfiguration.setRuntimeModuleRequirements()` o `HandlerConfiguration.setDRMModuleRequirements()`. Cuando un usuario solicita una nueva licencia con estas listas de bloqueados habilitadas, se deben instalar los tiempos de ejecución y las bibliotecas más recientes para poder emitir una licencia. Para ver un ejemplo sobre la lista de bloques de versiones de DRM y de tiempo de ejecución, consulte el código de ejemplo en [Actualización de una directiva mediante la API de Java](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md).
