---
seo-title: Revocación de credenciales de cliente y tiempo de ejecución de DRM
title: Revocación de credenciales de cliente y tiempo de ejecución de DRM
uuid: 8e36536a-8eed-4d27-8a5f-8d3219817e57
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Revocación de credenciales de cliente y tiempo de ejecución de DRM {#revoking-drm-client-and-runtime-credentials}

Las versiones de DRM/Runtime se identifican por nivel de seguridad, número de versión y otros atributos, incluidos el sistema operativo y el tiempo de ejecución. Para restringir las versiones de DRM/Runtime permitidas, establezca las restricciones de módulo en una directiva DRM o en una `HandlerConfiguration`. Las restricciones de módulos pueden incluir un nivel mínimo de seguridad y una lista de versiones de módulos que no están permitidas para que se les expida una licencia.

Consulte [Lista negra de clientes de DRM que no tienen acceso a contenido](../../protecting-content/introduction/usage-rules/runtime-application-restrictions/blacklist-drm-clients.md) protegido para obtener detalles sobre los atributos utilizados para identificar un módulo de DRM/Runtime.

Si se establece el nivel de seguridad mínimo, la versión del cliente (especificada en el token del equipo) debe ser buena o igual al valor especificado.

Si se especifica una lista de versiones excluidas y la versión del cliente coincide con cualquiera de los identificadores de versión de la lista, el cliente no podrá utilizar un derecho que contenga esta instancia ModuleRequirements. Para que un módulo coincida con la información de la versión, todos los parámetros especificados en la información de la versión, excepto la versión de lanzamiento, deben coincidir exactamente con los valores de los módulos. La versión de lanzamiento coincide si el valor del módulo cliente es menor o igual que el valor de la información de la versión.

En caso de que se informe de una infracción con un cliente DRM o una versión de tiempo de ejecución concretos, el propietario del contenido y el distribuidor de contenido (que ejecuta el servidor de licencias) pueden configurar el servidor para que rechace la expedición de licencias durante un período en el que Adobe no disponga de una corrección disponible. Esto se puede configurar a través de las directivas `HandlerConfiguration` descritas anteriormente o realizando cambios en todas las directivas de DRM. En este último caso, puede mantener una lista de actualización de directivas DRM y utilizarla para comprobar si se ha actualizado o revocado una directiva DRM.

Si necesita una versión más reciente de Adobe Flash Player/Adobe AIR Runtime o de la biblioteca de protección de contenido de Adobe (módulo DRM), debe actualizar sus directivas DRM.

Consulte [Actualización de una directiva mediante la API](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md)de Java.

A continuación, debe crear una lista de actualización de directivas de DRM o establecer restricciones en `HandlerConfiguration` invocando `HandlerConfiguration.setRuntimeModuleRequirements()` o `HandlerConfiguration.setDRMModuleRequirements()`. Cuando un usuario solicita una nueva licencia con las listas negras especificadas activadas, debe instalar los últimos tiempos de ejecución y bibliotecas antes de que se pueda emitir una licencia.

Consulte el código de muestra en [Actualización de una directiva mediante la API de Java. Para ver un ejemplo de la lista negra de DRM y versiones](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md) en tiempo de ejecución, por ejemplo, en la lista negra de versiones de DRM y de tiempo de ejecución.
