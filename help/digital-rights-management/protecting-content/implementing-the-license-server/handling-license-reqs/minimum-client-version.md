---
title: Versión mínima del cliente
description: Versión mínima del cliente
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---


# Versión mínima del cliente {#minimum-client-version}

Adobe Primetime DRM 2.0.2 y versiones posteriores introducen algunas reglas de uso nuevas que los clientes de Primetime DRM 2.0 no entienden. Al establecer la versión de cliente mínima admitida ( `HandlerConfiguration.setMinSupportedClientVersion()`), el servidor de licencias puede controlar el comportamiento de los clientes más antiguos cuando encuentran licencias con estas reglas de uso. En función de esta configuración, el servidor puede indicar si los clientes más antiguos pueden ignorar las reglas de uso que no comprenden o si los clientes más antiguos no podrán consumir licencias con esas reglas de uso.

Por ejemplo,

* Si la licencia especifica los requisitos de capacidades del dispositivo ( [Capacidades del dispositivo necesarias para reproducir contenido protegido](../../../protecting-content/introduction/usage-rules/runtime-application-restrictions/device-capabilities.md)), los clientes de Primetime DRM 2.0.2 y posteriores pueden hacer cumplir dichos requisitos.
* Si el servidor de licencias no desea que el contenido se reproduzca en clientes que no comprenden los requisitos de capacidades del dispositivo , establezca la versión mínima del cliente compatible en 2 (para 2.0.2). Esto impedirá que el servidor emita licencias a clientes de Primetime DRM antes de la versión 2.0.2. La versión mínima del cliente también se aplica si la licencia se transfiere de un cliente a otro.
* Si el servidor de licencias desea permitir que los clientes más antiguos ignoren los requisitos de capacidades del dispositivo, establezca la versión mínima del cliente compatible en 1 (para Primetime DRM 2.0). A continuación, el servidor emite una licencia a cualquier cliente de la versión 2.0 o posterior. Si el cliente actualiza o transfiere la licencia a otro cliente con la versión 2.0.2 o posterior, los requisitos de capacidades del dispositivo en la licencia se aplican porque el cliente puede admitir esa regla de uso.

