---
title: Versión mínima del cliente
description: Versión mínima del cliente
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# Versión mínima del cliente {#minimum-client-version}

Adobe Primetime DRM 2.0.2 y posteriores introducen algunas reglas de uso nuevas que los clientes de Primetime DRM 2.0 no comprenden. Estableciendo la versión de cliente mínima admitida ( `HandlerConfiguration.setMinSupportedClientVersion()`), el servidor de licencias puede controlar cómo se comportan los clientes más antiguos cuando se encuentran con licencias con estas reglas de uso. En función de esta configuración, el servidor puede indicar si los clientes más antiguos pueden ignorar las reglas de uso que no entienden o si no podrán consumir licencias con esas reglas de uso.

Por ejemplo,

* Si la licencia especifica los requisitos de capacidades del dispositivo ( [Funciones del dispositivo necesarias para reproducir contenido protegido](../../../protecting-content/introduction/usage-rules/runtime-application-restrictions/device-capabilities.md)), los clientes de DRM de Primetime 2.0.2 y posteriores pueden aplicar estos requisitos.
* Si el servidor de licencias no desea que el contenido se reproduzca en clientes que no comprendan los requisitos de capacidades del dispositivo, establezca la versión de cliente mínima admitida en 2 (para 2.0.2). Esto evitará que el servidor emita licencias a clientes de Primetime DRM anteriores a la versión 2.0.2. La versión de cliente mínima también se aplica si la licencia se transfiere de un cliente a otro.
* Si el servidor de licencias desea permitir que clientes más antiguos ignoren los requisitos de capacidades del dispositivo, establezca la versión de cliente mínima admitida en 1 (para Primetime DRM 2.0). A continuación, el servidor emite una licencia para cualquier cliente versión 2.0 o posterior. Si el cliente actualiza o transfiere la licencia a otro cliente con la versión 2.0.2 o posterior, los requisitos de capacidades del dispositivo en la licencia se aplican porque el cliente puede admitir esa regla de uso.
