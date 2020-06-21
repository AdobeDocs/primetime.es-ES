---
seo-title: Revocación de credenciales de cliente y tiempo de ejecución de DRM
title: Revocación de credenciales de cliente y tiempo de ejecución de DRM
uuid: 774b8ac7-51bb-42fc-a05d-cfa718e24a81
translation-type: tm+mt
source-git-commit: fbc175f383c850a7286b1e6e89daa027e00b29ef
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# Revocación de credenciales de cliente y tiempo de ejecución de DRM{#revoking-drm-client-and-runtime-credentials}

Las versiones de DRM/Runtime se identifican por nivel de seguridad, número de versión y otros atributos, incluidos el sistema operativo y el tiempo de ejecución. Para restringir las versiones de DRM/Runtime permitidas, establezca las restricciones de módulo en una directiva o en una `HandlerConfiguration`. Las restricciones de módulos pueden incluir un nivel mínimo de seguridad y la lista de versiones de módulos que no pueden ser expedidas con una licencia. Consulte Lista [de bloques de clientes de DRM con acceso restringido al contenido](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-blocklist-drm-clients.md) protegido para obtener detalles sobre los atributos utilizados para identificar un módulo de DRM/tiempo de ejecución.

Si se establece el nivel de seguridad mínimo, la versión del cliente (especificada en el token del equipo) debe ser buena o igual al valor especificado.

Si se especifica una lista de versiones excluidas y la versión del cliente coincide con cualquiera de los identificadores de versión de la lista, el cliente no podrá utilizar un derecho que contenga esta instancia ModuleRequirements. Para que un módulo coincida con la información de la versión, todos los parámetros especificados en la información de la versión, excepto la versión de lanzamiento, deben coincidir exactamente con los valores de los módulos. La versión de lanzamiento coincide si el valor del módulo cliente es menor o igual que el valor de la información de la versión.

En el evento se informa de una infracción con un cliente DRM o una versión de tiempo de ejecución concretos, el propietario del contenido y el distribuidor de contenido (que ejecuta el servidor de licencias) pueden configurar el servidor para que rechace la expedición de licencias durante un período en el que Adobe no tenga una corrección disponible. Esto se puede configurar a través de la `HandlerConfiguration` descripción anterior o realizando cambios en todas las directivas. En este último caso, puede mantener una lista de actualización de directiva y utilizarla para comprobar si se ha actualizado o revocado una directiva.

Si necesita una versión más reciente de Adobe® Flash® Player/Adobe® AIR® Runtime o de la biblioteca de protección de contenido de Adobe (módulo DRM), actualice las políticas como se muestra en [Actualización de una política con la API](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md) de Java y cree una Lista de actualización de directiva, o establezca restricciones en `HandlerConfiguration` invocando `HandlerConfiguration.setRuntimeModuleRequirements()` o `HandlerConfiguration.setDRMModuleRequirements()`. Cuando un usuario solicita una nueva licencia con estas listas de bloques habilitadas, los tiempos de ejecución y las bibliotecas más recientes deben instalarse antes de que se pueda emitir una licencia. Para ver un ejemplo de la lista de bloques de versiones de DRM y tiempo de ejecución, consulte el código de muestra en [Actualización de una directiva mediante la API](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md)de Java.
