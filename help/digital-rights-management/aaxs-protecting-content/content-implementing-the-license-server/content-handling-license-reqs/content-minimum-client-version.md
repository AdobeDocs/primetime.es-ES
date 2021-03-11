---
title: Versión mínima del cliente
description: Versión mínima del cliente
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Versión mínima del cliente {#minimum-client-version}

Adobe Access 2.0.2 y versiones posteriores introducen algunas reglas de uso nuevas que los clientes de Adobe Access 2.0 no entienden. Al establecer la versión de cliente mínima admitida ( `HandlerConfiguration.setMinSupportedClientVersion()`), el servidor de licencias puede controlar cómo se comportarán los clientes más antiguos cuando encuentren licencias con estas reglas de uso. En función de esta configuración, el servidor puede indicar si los clientes más antiguos pueden ignorar las reglas de uso que no comprenden o si los clientes más antiguos no podrán consumir licencias con esas reglas de uso.

Por ejemplo,

* Si la licencia especifica los requisitos de las capacidades del dispositivo ( [Capacidades del dispositivo necesarias para reproducir contenido protegido](../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-device-capabilities.md)), los clientes de acceso al Adobe 2.0.2 y superiores pueden hacer cumplir dichos requisitos.
* Si el servidor de licencias no desea que el contenido se reproduzca en clientes que no comprenden los requisitos de capacidades del dispositivo , establezca la versión mínima del cliente compatible en 2 (para 2.0.2). Esto impedirá que el servidor emita licencias a clientes de Adobe Access antes de la versión 2.0.2. La versión mínima del cliente también se aplicará si la licencia se transfiere de un cliente a otro.
* Si el servidor de licencias desea permitir que los clientes más antiguos ignoren los requisitos de las capacidades del dispositivo, establezca la versión mínima del cliente compatible en 1 (para Acceso a Adobe 2.0). El servidor emitirá una licencia para cualquier cliente de la versión 2.0 o superior. Si el cliente actualiza o transfiere la licencia a otro cliente con la versión 2.0.2 o superior, se aplicarán los requisitos de capacidades del dispositivo de la licencia, ya que el cliente ahora admitiría esa regla de uso.

