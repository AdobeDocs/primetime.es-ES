---
title: Amazon fireTV SSO - Guía de inicio del programador
description: Amazon fireTV SSO - Guía de inicio del programador
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---


# Amazon fireTV SSO - Guía de inicio del programador {#amazon-firetv-sso---programmer-kick-off-guide}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>

## Introducción {#intro}

Este documento describe la información necesaria para integrar el nuevo **SDK de fireTV de la autenticación de Adobe Primetime** en su aplicación fireTV. Este nuevo SDK aprovecha la integración de nivel de sistema operativo en la plataforma fireTV de Amazon, ofreciendo así **Inicio de sesión único** asistencia técnica. Para beneficiarse del inicio de sesión único, es necesario realizar un pequeño esfuerzo de su parte para migrar su aplicación de la API sin cliente al nuevo SDK de fireTV. A continuación se detallan algunos cambios en los flujos de autenticación.

## Integración de alto nivel de arquitectura y de nivel de sistema operativo {#high}

Con el fin de lograr el inicio de sesión único entre las aplicaciones de TV en todas partes en la plataforma FireTV de Amazon y mejorar la experiencia general en esta plataforma, decidimos integrar nuestro SDK principal a nivel de sistema operativo FireTV. Los programadores deberán compilar con una biblioteca de stub proporcionada por Adobe. La funcionalidad real la proporcionará la biblioteca de Adobes presente en FireTV OS de Amazon.

Hasta que Amazon proporcione un simulador fireTV que incorpore nuestra biblioteca a nivel del sistema operativo, el desarrollo solo sería posible mediante dispositivos FireTV reales.

## Ventajas {#bene}

* Inicio de sesión único entre todas las aplicaciones de TV por Adobe en todas partes en la plataforma FireTV de Amazon con todos los MVPD integrados.
* Capacidad para beneficiarse de HBA (con MVPDs soportados).
* Posibilidad de utilizar el SDK de fireTV más reciente sin necesidad de actualizar las aplicaciones cada vez que se lanza una nueva versión del SDK.
* Todas las aplicaciones TVE se benefician del uso de la biblioteca del sistema compartido, ya que eliminan la necesidad de tener una copia local de la biblioteca AccessEnabler. Esto también garantiza que todas las aplicaciones utilicen la misma versión del SDK.
* Autenticación de una sola pantalla: sin necesidad de código de registro y flujos de trabajo de la segunda pantalla.

## Migración de la aplicación basada en API sin cliente a la aplicación basada en el SDK de fireTV {#migra1}

Para migrar de la API sin cliente al SDK de fireTV, debe eliminar el código base relacionado con la API sin cliente e integrar el nuevo SDK de fireTV.

En comparación con la aplicación basada en API sin cliente, con el nuevo SDK de fireTV que la autenticación pasa a la primera pantalla, ya no es necesario realizar una segunda autenticación de pantalla.

Esto requiere que los programadores agreguen un selector de MVPD a sus aplicaciones para que los usuarios puedan elegir su proveedor de TV directamente en el dispositivo fireTV. Una vez seleccionada la MVPD, se mostrará al usuario la página de inicio de sesión de MVPD en el dispositivo fireTV.

Los modelos de alambres de los flujos de usuario que describen los escenarios normales, HBA y SSO en fireTV se encuentran en [Amazon Fire TV: Flujo de usuario de inicio de sesión en MVVPD](https://xd.adobe.com/view/9058288e-4b67-43a1-9d5b-5f76ede6c51e/).

## Migración de la aplicación basada en el SDK para Android a la aplicación basada en el SDK de fireTV {#migra2}

Este nuevo SDK de fireTV es muy similar al SDK de Android existente y a la documentación actual que tenemos para **integración de nuestro SDK para Android** <!--http://tve.helpdocsonline.com/android-technical-overview-->se puede utilizar hasta que tengamos listos los documentos del SDK de fireTV. Si ya tiene aplicaciones Android que utilizan nuestro SDK para Android, la integración del SDK de fireTV en su aplicación fireTV debería ser sencilla.

En comparación con el SDK de Android existente, en fireTV SDK el proceso de autenticación será más sencillo de desarrollar, ya que las tareas de administrar/presentar la página de inicio de sesión de MVPD y recuperar el token AuthN se realizarán internamente mediante la biblioteca AccessEnabler.

## Preguntas frecuentes {#faq}

1. ¿Cómo va a **SSO** ¿trabajo?

   * SSO funcionará en todas las aplicaciones de programadores con autenticación de Adobe Primetime que utilicen el nuevo SDK de fireTV en el mismo dispositivo FireTV de Amazon
   * SSO entre aplicaciones de programación implementadas en la API de REST sin cliente y aplicaciones implementadas en el SDK de FireTV **NO será compatible**

1. ¿Cuál es la cobertura de MVPD de fireTV SSO?

   * **Todos los MVPD** integrado por la autenticación de Adobe Primetime será técnicamente compatible con SSO en el SDK de fireTV.

1. Además de usar el nuevo SDK, ¿qué otros? **cambios en el flujo de trabajo** ¿Los programadores deberían estar al tanto?

   * Los programadores necesitan implementar un selector MVPD para la plataforma fireTV.

1. ¿Habrá algún cambio en la autenticación? **TTL**?

   * No hay cambios en el comportamiento con respecto a los TTL de autenticación.
   * El primer token de autenticación válido se utilizará para realizar el SSO y, en este caso, todas las demás aplicaciones que se autenticarán mediante SSO utilizarán el mismo TTL hasta que caduque. Por lo tanto, al navegar de una aplicación a otra, la segunda aplicación compartirá el TTL de la primera aplicación que se autentique.

1. Cómo **API de degradación** ¿trabajo?

   * No se necesitan cambios para la API de degradación, la experiencia del usuario será la misma que en los dispositivos Android.

1. Cómo **TempPass** ¿se ven afectados los flujos?

   * Los flujos de TempPass son de una sola pantalla y se comportan como en cualquier otro dispositivo nativo.

1. ¿Funcionará otra funcionalidad de Adobe como antes?

   * Toda la funcionalidad de autenticación de Primetime funcionará en fireTV como en dispositivos Android.
