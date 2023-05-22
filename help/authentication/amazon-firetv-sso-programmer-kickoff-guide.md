---
title: Amazon fireTV SSO - Guía de inicio del programador
description: Amazon fireTV SSO - Guía de inicio del programador
exl-id: cf9ba614-57ad-46c3-b154-34204b38742d
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---

# Amazon fireTV SSO - Guía de inicio del programador {#amazon-firetv-sso---programmer-kick-off-guide}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.

</br>

## Introducción {#intro}

Este documento describe la información necesaria para integrar el nuevo **SDK de fireTV de autenticación de Adobe Primetime** en su aplicación fireTV. Este nuevo SDK aprovecha la integración a nivel del sistema operativo en la plataforma fireTV de Amazon y ofrece lo siguiente **Inicio de sesión único** soporte. Para beneficiarse del inicio de sesión único se requiere un pequeño esfuerzo por su parte para migrar la aplicación de la API sin cliente al nuevo SDK de fireTV. A continuación se detallan algunos cambios en los flujos de autenticación.

## Arquitectura de alto nivel e integración a nivel del sistema operativo {#high}

Con el fin de lograr el inicio de sesión único entre las aplicaciones de TV Everywhere en Amazon fireTV platform y para mejorar la experiencia general en esta plataforma, decidimos integrar nuestro SDK principal a nivel del sistema operativo fireTV. Los programadores deberán compilar con una biblioteca de código auxiliar proporcionada por Adobe. La funcionalidad real la proporcionará la biblioteca de Adobe presente en el sistema operativo fireTV de Amazon.

Hasta que Amazon proporcione un simulador fireTV que incorpore nuestra biblioteca a nivel del sistema operativo, el desarrollo solo sería posible usando dispositivos fireTV reales.

## Ventajas {#bene}

* Inicio de sesión único entre todas las aplicaciones de TV por Adobe en todas partes en Amazon fireTV platform con todas las MVPD integradas.
* Posibilidad de beneficiarse de HBA (con MVPD compatibles).
* Capacidad para utilizar el SDK de fireTV más reciente sin necesidad de actualizar las aplicaciones cada vez que se lanza una nueva versión del SDK.
* Todas las aplicaciones de TVE se benefician del uso de la biblioteca del sistema compartido al eliminar la necesidad de tener una copia local de la biblioteca AccessEnabler. Esto también garantiza que todas las aplicaciones utilicen la misma versión del SDK.
* Autenticación de pantalla única: sin necesidad de código de registro y flujos de trabajo de segunda pantalla.

## Migración de una aplicación basada en API sin cliente a una aplicación basada en SDK de fireTV {#migra1}

Para migrar de la API sin cliente al SDK de fireTV, debe eliminar el código base relacionado con la API sin cliente e integrar el nuevo SDK de fireTV.

En comparación con la aplicación basada en la API sin cliente, con el nuevo SDK de fireTV la autenticación se mueve a la primera pantalla, ya no hay necesidad de una segunda autenticación de pantalla.

Esto requiere que los programadores agreguen un selector de MVPD en sus aplicaciones para que los usuarios puedan elegir su proveedor de TV directamente en el dispositivo fireTV. Al seleccionar MVPD, se mostrará al usuario la página de inicio de sesión de MVPD en el dispositivo fireTV.

Puede encontrar modelos de los flujos de usuario que describen los escenarios normales, HBA y SSO en fireTV en [Flujo de usuario de inicio de sesión de Amazon Fire TV - MVVPD](https://xd.adobe.com/view/9058288e-4b67-43a1-9d5b-5f76ede6c51e/).

## Migración de una aplicación basada en SDK de Android a una aplicación basada en SDK de FireTV {#migra2}

Este nuevo SDK de FireTV es muy similar al SDK de Android existente y a la documentación actual que tenemos para **integración del SDK para Android** <!--http://tve.helpdocsonline.com/android-technical-overview-->se puede usar hasta que tengamos listos los documentos del SDK de fireTV. Si ya tiene aplicaciones de Android que usan nuestro SDK de Android, la integración del SDK de fireTV en su aplicación fireTV debería ser sencilla.

En comparación con el SDK de Android existente, en el SDK de fireTV el proceso de autenticación será más sencillo de desarrollar, ya que las tareas de gestión/presentación de la página de inicio de sesión de MVPD y la recuperación del token de AuthN se realizarán internamente por la biblioteca de AccessEnabler.

## Preguntas frecuentes {#faq}

1. ¿Cómo se **SSO** ¿trabajar?

   * SSO funcionará en todas las aplicaciones de Programador con autenticación de Adobe Primetime que estén usando el nuevo SDK de fireTV en el mismo dispositivo Amazon fireTV
   * SSO entre aplicaciones de programador implementadas en la API de REST sin cliente y aplicaciones implementadas en el SDK de fireTV **NO será compatible**

1. ¿Cuál es la cobertura de MVPD de FireTV SSO?

   * **Todas las MVPD** integrado por la autenticación de Adobe Primetime será técnicamente compatible con SSO en el SDK de fireTV.

1. Además de utilizar el nuevo SDK, ¿qué más **cambios de flujo de trabajo** ¿Deben tener en cuenta los programadores?

   * Los programadores necesitan implementar un selector de MVPD para la plataforma fireTV.

1. ¿Se producirá algún cambio en la autenticación? **TTL**?

   * No hay cambios en el comportamiento con respecto a los TTL de autenticación.
   * El primer token de autenticación válido se utilizará para realizar el SSO y, en este caso, todas las demás aplicaciones que se autenticarán mediante SSO utilizarán el mismo TTL hasta que caduque. Por lo tanto, al navegar de una aplicación a otra, la segunda aplicación compartirá el TTL de la primera aplicación que se autentica.

1. ¿Cómo? **API de degradación** ¿trabajar?

   * No se necesitan cambios para la API de degradación; la experiencia del usuario será la misma que en los dispositivos Android.

1. Cómo **TempPass** ¿se ven afectados los flujos?

   * Los flujos TempPass son de una sola pantalla y se comportan como en cualquier otro dispositivo nativo.

1. ¿Funcionarán otras funciones de Adobe como antes?

   * Toda la funcionalidad de autenticación de Primetime funcionará en fireTV como en dispositivos Android.
