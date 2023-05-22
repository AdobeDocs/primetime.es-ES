---
title: Versión mínima del cliente
description: Versión mínima del cliente
copied-description: true
exl-id: ba311d33-f3dd-42c5-ac66-7ad665d1bd20
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Versión mínima del cliente {#minimum-client-version}

Adobe Access 2.0.2 y versiones posteriores incluyen algunas reglas de uso nuevas, que los clientes de Adobe Access 2.0 no entienden. Estableciendo la versión de cliente mínima admitida ( `HandlerConfiguration.setMinSupportedClientVersion()`), el servidor de licencias puede controlar cómo se comportarán los clientes más antiguos cuando se encuentren con licencias con estas reglas de uso. En función de esta configuración, el servidor puede indicar si los clientes más antiguos pueden ignorar las reglas de uso que no entienden o si no podrán consumir licencias con esas reglas de uso.

Por ejemplo,

* Si la licencia especifica los requisitos de capacidades del dispositivo ( [Funciones del dispositivo necesarias para reproducir contenido protegido](../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-device-capabilities.md)), los clientes de Adobe Access 2.0.2 y posteriores pueden aplicar estos requisitos.
* Si el servidor de licencias no desea que el contenido se reproduzca en clientes que no comprendan los requisitos de capacidades del dispositivo, establezca la versión de cliente mínima admitida en 2 (para 2.0.2). Esto evitará que el servidor emita licencias para clientes de acceso a Adobe anteriores a la versión 2.0.2. La versión de cliente mínima también se aplicará si la licencia se transfiere de un cliente a otro.
* Si el servidor de licencias desea permitir que los clientes más antiguos ignoren los requisitos de capacidades del dispositivo, establezca la versión de cliente mínima admitida en 1 (para Acceso de Adobe 2.0). El servidor emitirá una licencia a cualquier cliente versión 2.0 o posterior. Si el cliente actualiza o transfiere la licencia a otro cliente con la versión 2.0.2 o superior, se aplicarán los requisitos de capacidades del dispositivo en la licencia, ya que el cliente ahora admitiría esa regla de uso.
