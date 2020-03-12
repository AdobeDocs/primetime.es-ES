---
seo-title: Versión mínima del cliente
title: Versión mínima del cliente
uuid: 9f39e4e7-64eb-43ea-b194-b744838a411e
translation-type: tm+mt
source-git-commit: 53654b740b03c6a79394d30704a41186d4655237

---


# Versión mínima del cliente {#minimum-client-version}

Adobe Access 2.0.2 y versiones posteriores introducen algunas reglas de uso nuevas que los clientes de Adobe Access 2.0 no entienden. Al establecer la versión mínima de cliente admitida ( `HandlerConfiguration.setMinSupportedClientVersion()`), el servidor de licencias puede controlar el comportamiento de los clientes más antiguos cuando encuentran licencias con estas reglas de uso. En función de esta configuración, el servidor puede indicar si los clientes más antiguos pueden ignorar las reglas de uso que no entienden o si los clientes más antiguos no podrán consumir licencias con esas reglas de uso.

Por ejemplo,

* Si la licencia especifica los requisitos de las capacidades del dispositivo (capacidades [del dispositivo necesarias para reproducir contenido](../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-device-capabilities.md)protegido), los clientes de Adobe Access 2.0.2 y versiones posteriores pueden aplicar dichos requisitos.
* Si el servidor de licencias no desea que el contenido se reproduzca en clientes que no entienden los requisitos de capacidades del dispositivo, establezca la versión mínima del cliente compatible en 2 (para 2.0.2). Esto impedirá que el servidor emita licencias a los clientes de Adobe Access antes de la versión 2.0.2. La versión mínima del cliente también se aplicará si la licencia se transfiere de un cliente a otro.
* Si el servidor de licencias desea permitir que los clientes más antiguos omitan los requisitos de capacidades del dispositivo, establezca la versión mínima del cliente compatible en 1 (para Adobe Access 2.0). El servidor emitirá una licencia para cualquier cliente versión 2.0 o posterior. Si el cliente actualiza o transfiere la licencia a otro cliente con la versión 2.0.2 o superior, se aplicarán los requisitos de capacidades del dispositivo de la licencia, ya que el cliente ahora admitiría esa regla de uso.

