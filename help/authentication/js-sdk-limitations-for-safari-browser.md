---
title: Limitaciones del SDK de JS para el explorador Safari
description: Limitaciones del SDK de JS para el explorador Safari
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 0%

---

# Limitaciones del SDK de JS para el explorador Safari {#js-sdk-limitations-for-safari-browser}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

<!--
>[!IMPORTANT] 
>
>We are strongly recommending [migration to AccessEnabler JavaScript SDK versions 4.x](http://tve.helpdocsonline.com/accessenabler-js-v4-migration-guide) in order to have a stable and predictable behavior on Safari browser.-->


## Safari 10 {#safari10}

**Detalles**

* A partir de Safari 10, la configuración predeterminada de privacidad del explorador hará que las funciones de inicio de sesión único (SSO), cierre de sesión único (SLO) y autenticación pasiva dejen de funcionar. El inicio de sesión único (SSO) y la autenticación pasiva no funcionarán ni siquiera en la misma sesión entre varias pestañas o ventanas del explorador.

* Estos cambios afectan a los procesos de autenticación de Adobe Primetime y están teniendo un impacto en ellos para las siguientes versiones del SDK de JavaScript de AccessEnabler: v2 (versiones 2.x), v3 (versiones 3.x), v4 (versiones 4.x).

### Mitigación {#mitigation-safari10}

* Para mitigar estas limitaciones, puede indicar al usuario que cambie la configuración de privacidad del explorador de Safari 10 y usar la variable **Siempre permitir**&quot; para la opción &quot;**Cookies y datos de sitio web**&quot; en la pestaña Privacidad del navegador de Preferencias, como se muestra en la imagen siguiente.

   ![](assets/always-allow-safari10.png)


## Safari 11 {#safari11}

**Detalles**

>[!IMPORTANT]
>
>Todos los detalles anteriores de la sección Safari 10 siguen aplicándose en el caso de Safari 11.

* A partir de Safari 11, el explorador introduce [Prevención inteligente del seguimiento](https://webkit.org/blog/7675/intelligent-tracking-prevention/)(ITP), una tecnología que utiliza heurística para evitar el seguimiento entre sitios. Estas heurísticas afectan a la forma en que se almacenan las cookies de terceros y se reproducen en las llamadas de red, lo que significa que, según la activación del mecanismo ITP, el explorador Safari bloqueará las cookies de terceros en la comunicación del modelo cliente-servidor.

* El servicio de autenticación de Adobe Primetime utiliza y se basa en cookies como parte del proceso de autenticación **para funcionar**. En situaciones en las que el proceso de autenticación se realiza automáticamente (por ejemplo, Temp Pass) o en implementaciones que utilizan iFrames o funcionalidad &quot;sin actualización&quot;, las cookies de Adobe se consideran cookies de terceros y están bloqueadas de forma predeterminada. En cualquier otro caso, Safari utiliza un algoritmo de aprendizaje automático que podría marcar todas las cookies del servicio de autenticación de Primetime de Adobe como cookies de seguimiento, por lo que está sujeto al bloqueo de ITP.  

* En conclusión, es posible que un usuario del explorador Safari 11 no pueda autenticarse en un sitio web habilitado para la autenticación Adobe Primetime después de la activación del mecanismo de prevención inteligente del seguimiento (ITP), especialmente cuando los usuarios utilizan varios sitios web habilitados para la autenticación Adobe Primetime. Por lo tanto, la experiencia de autenticación del usuario puede ser inesperada e indefinida, ya que abarca desde la incapacidad para iniciar sesión hasta una duración de autenticación inferior a la esperada.

* Estos cambios afectan a los procesos de autenticación de Adobe Primetime y están teniendo un impacto en ellos para las siguientes versiones del SDK de JavaScript de AccessEnabler: v2 (versiones 2.x), v3 (versiones 3.x).

### Mitigación {#mitigation-safari11}

* Tanto para el SDK v3 de JavaScript de AccessEnabler (versiones 3.x) como para el SDK v4 de JavaScript de AccessEnabler (versiones 4.x), la biblioteca contiene un mecanismo capaz de identificar las situaciones en las que la autenticación del usuario se bloqueó debido a la falta de cookies requeridas. En estas situaciones, la biblioteca déclencheur una llamada de retorno de error específica [N130](/help/authentication/error-reporting.md#advanced-error-codes-reference), que se devuelve al sitio web habilitado para la autenticación de Adobe Primetime para utilizarse como señal para indicar al usuario que realice acciones que puedan mitigar el problema. Para beneficiarse de este mecanismo, el sitio web debe implementar la variable [Informes de errores](/help/authentication/error-reporting.md) especificación.

* Para el SDK v2 de JavaScript de AccessEnabler (versiones 2.x), la biblioteca no ofrece el mecanismo descrito anteriormente, por lo tanto el sitio web habilitado para la autenticación de Adobe Primetime no puede indicar cuándo se debe indicar al usuario que realice acciones para mitigar el problema.

* Lista de acciones que pueden mitigar los problemas mencionados **se aplica a las tres versiones** del SDK de JavaScript de AccessEnabler.

* When [N130](/help/authentication/error-reporting.md#advanced-error-codes-reference) la llamada de retorno de error la recibe el sitio web del implementador, se debe indicar al usuario que deshabilite Intelligent Tracking Prevention (ITP) y habilite las cookies de terceros mediante:

* En el caso de Mac OS X High Sierra y posterior: Desmarcando el &quot;**Impedir el seguimiento entre sitios**&quot; para &quot;**Seguimiento del sitio web**&quot; en la pestaña Privacidad del navegador de Preferencias, como se muestra en la imagen siguiente.

   ![](assets/uncheck-prvnt-cr-st-tr-safari11.png)

* En el caso de Mac OS X Sierra y anteriores: Comprobando el **Siempre permitir**&quot; para la opción &quot;**Cookies y datos de sitio web**&quot; en la pestaña Privacidad del navegador de Preferencias, como se muestra en la imagen siguiente.

   ![](assets/always-allow-safari11.png)

## Safari 12 {#safari12}

**Detalles**

>[!IMPORTANT]
>
>Todos los detalles anteriores de la sección Safari 10 y la sección Safari 11 siguen siendo aplicables en el caso de Safari 12.

Esta sección detalla los problemas de compatibilidad de **AccessEnabler JavaScript SDK versiones 4.x** en Safari 12.

>[!NOTE]
>
>Tenga en cuenta que, en el caso de las versiones 2.x y 3.x del SDK de JavaScript de AccessEnabler de JavaScript, ambas utilizan cookies de terceros para los procesos de autenticación y, debido a las políticas de cookies ITP y de terceros que comienzan con Safari 11, la experiencia de autenticación del usuario puede ser inesperada e indefinida, ya que puede variar desde la incapacidad para iniciar sesión hasta una duración de autenticación más corta de la esperada.


### Funcionalidad certificada del SDK v4 de JavaScript de AccessEnabler (versiones 4.x) en Safari 12 {#certified-functionality-of-accessenabler-javacscript=sdk-v4}

* **Autenticación** los flujos que utilizan la interacción del usuario siempre funcionarán, incluso si el explorador del usuario tiene deshabilitadas las cookies de terceros, ya que, a partir de la versión 4.0, el SDK para JavaScript de AccessEnabler ya no utiliza cookies de terceros para los procesos de autenticación.

>[!NOTE]
>
>El usuario DEBE interactuar con el sitio para abrir las ventanas emergentes de inicio de sesión o interactuar con la página de inicio de sesión de MVPD.

* **Autorización/comprobación previa/metadatos del usuario** las operaciones son completamente funcionales, siempre que el usuario ya esté autenticado.

### Problemas conocidos del SDK v4 de JavaScript de AccessEnabler (versiones 4.x) en Safari 12 {#known-issues-of-accessenabler-javascript-sdk-4}

* SSO y SLO

   * Debido a cómo se implementa localStorage en Safari a partir de Safari 10, el SDK de JS ya no puede compartir el estado de inicio de sesión a través de un iFrame de dominio común. Esto significa que el usuario debe iniciar sesión en cada sitio que utilice el SDK de JavaScript de AccessEnabler. Al cerrar la sesión también no se eliminan los tokens de autenticación entre sitios, por lo que el usuario debe cerrar la sesión en cada sitio web habilitado para la autenticación de Adobe Primetime.

* Pase temporal

   * Para pasadas temporales, el SDK de JavaScript de AccessEnabler utiliza un mecanismo de personalización para bloquear un token de autenticación en un dispositivo específico (instancia del explorador). Debido a los nuevos mecanismos de Safari 12 diseñados para evitar el seguimiento, la huella digital que estamos computando y utilizando en el mecanismo de individualización **será el mismo para todos los usuarios que tengan la misma dirección IP**. Si tomamos en consideración la IP del cliente con fines de individualización, el impacto es sobre los usuarios que comparten la misma dirección IP pública. Para estos usuarios, calcularemos el mismo id de individualización y el pase temporal estará vinculado a él. Esto significa que una vez que un usuario de este tipo utiliza un pase temporal, nadie más tendrá acceso a él \! Esto afecta especialmente a los usuarios corporativos, instituciones educativas o cualquier otra organización que tenga varios usuarios usando NAT o un proxy común para acceder a Internet.

>[!NOTE]
>
>Este problema afecta a los usuarios solo si el implementador utiliza Temp Pass como resultado de la interacción del usuario; de lo contrario, la autenticación Temp Pass está sujeta a **Flujos automáticos** más abajo.

* Flujos automáticos

   * Los flujos de autenticación intentados en un modo automatizado, sin interacción del usuario, no se producirán correctamente en Safari 12 al utilizar el SDK 4.0 de JS. Tenga en cuenta que el SDK 4.1 de JS para futuro corrige todos los problemas con los flujos automatizados.

Casos de uso afectados por este problema:

* Autenticación automática de TempPass (vista previa gratuita): para estos flujos, el SDK genera un error N130.

* Autenticación pasiva (falla silenciosamente): se solicita al usuario que seleccione este MVPD e introduzca credenciales

### Mitigación {#mitigation-safari12}

**SSO y SLO**

En el momento de escribir este artículo no hay una mitigación conocida o posible. Apple introdujo una &quot;API de acceso al almacenamiento&quot; en Safari 12 (`https://webkit.org/blog/8124/introducing-storage-access-api`), pero la implementación actual no se aplica a localStorage sino solo a las cookies. Además, la API requiere la interacción del usuario para poder utilizarlo y, una vez que lo utilice, también se le solicitará un cuadro de diálogo de permisos similar al que se muestra a continuación.

![](assets/permission-dialog-apple.png)


En este punto, estos requisitos/mensajes de Safari no se alinean con nuestros requisitos de UX y no tenemos un comportamiento coherente como en otros exploradores, donde SSO &quot;solo funciona&quot; una vez que guardamos un token en un dominio común localStorage.

**Pase temporal**

Para mitigar los problemas de personalización y tener una interacción de usuario, le recomendamos que utilice **[Pase temporal promocional ](/help/authentication/promotional-temp-pass.md)** de forma interactiva, y proporcione al menos una información adicional sobre el usuario (por ejemplo, la dirección de correo electrónico).

## Safari 13 {#safari13}

**Detalles**

>[!IMPORTANT]
>
>Todos los detalles anteriores de la sección Safari 10 hasta la sección Safari 12 siguen siendo aplicables en el caso de Safari 13.


A partir de Safari 13, el explorador introduce nuevos cambios en la variable [Prevención inteligente del seguimiento](https://webkit.org/blog/7675/intelligent-tracking-prevention/) (ITP), lo que hace que las heurísticas del mecanismo sean más estrictas en el proceso de marcar las cookies de terceros como cookies de seguimiento, a fin de evitar el seguimiento entre sitios.

Como se describe en secciones anteriores, el servicio de autenticación de Adobe Primetime utiliza y se basa en cookies de terceros como parte de los procesos de autenticación cuando los implementadores utilizan el SDK v2 de JavaScript de AccessEnabler (versiones 2.x) y el SDK v3 de JavaScript de AccessEnabler (versiones 3.x). En comparación con las versiones anteriores del navegador Safari cuando ITP se iniciaba después de pasar un tiempo para &quot;conocer&quot; la interacción entre el usuario y las partes involucradas (sitios web y Adobe del programador), el navegador Safari 13 está bloqueando las cookies de terceros iniciales que se consideran cookies de seguimiento en la comunicación del modelo cliente-servidor.

En conclusión, es muy probable que un usuario del explorador Safari 13 no pueda iniciar nuevas autenticaciones en un sitio web habilitado para la autenticación de Adobe Primetime que esté utilizando una versión anterior del SDK de JavaScript de AccessEnabler, v2 (versiones 2.x) o v3 (versiones 3.x). Esto sucede debido al hecho de que ITP bloquea todas las cookies del servicio de autenticación de Primetime del Adobe requerido, lo que impide que el servicio cumpla la solicitud de autenticación.

La biblioteca AccessEnabler JavaScript SDK v4 (versiones 4.x) no utiliza cookies de terceros para el proceso de autenticación, por lo que sus operaciones no se ven afectadas de ninguna manera por los cambios de Safari 13.

### Mitigación {#mitigation-safari13}

En primer lugar, recomendamos encarecidamente **migración a las versiones 4.x del SDK para JavaScript de AccessEnabler** para tener un comportamiento estable y predecible en el navegador Safari.

En segundo lugar, para el SDK v3 de JavaScript de AccessEnabler (versiones 3.x), la biblioteca contiene un mecanismo capaz de identificar las situaciones en las que la autenticación de los usuarios se bloqueó debido a la falta de cookies requeridas. En estas situaciones, la biblioteca déclencheur una llamada de retorno de error específica ([N130](/help/authentication/error-reporting.md#advanced-error-codes-reference)) que se devuelve al sitio web habilitado para la autenticación de Adobe Primetime para utilizarse como señal para indicar al usuario que realice acciones que puedan mitigar el problema. Para beneficiarse de este mecanismo, el sitio web debe implementar la variable [Informes de errores](/help/authentication/error-reporting.md) especificación.

Para el SDK v2 de JavaScript de AccessEnabler (versiones 2.x), la biblioteca no ofrece el mecanismo descrito anteriormente, por lo tanto el sitio web habilitado para la autenticación de Adobe Primetime no puede indicar cuándo se debe indicar al usuario que realice acciones para mitigar el problema.

When [N130](/help/authentication/error-reporting.md#advanced-error-codes-reference) la llamada de retorno de error la recibe el sitio web del implementador, se debe indicar al usuario que deshabilite Intelligent Tracking Prevention (ITP) y habilite las cookies de terceros mediante:

* En el caso de Mac OS X High Sierra y posterior: Desmarcando el &quot;**Impedir el seguimiento entre sitios**&quot; para &quot;**Seguimiento del sitio web**&quot; en la pestaña Privacidad del navegador de Preferencias, como se muestra en la imagen siguiente.

   ![](assets/prvnt-cross-site-tr-safari13.png)

* En el caso de Mac OS X Sierra y anteriores: Comprobación de</span>El &quot;**Siempre permitir**&quot; para la opción &quot;**Cookies y datos de sitio web**&quot; en la pestaña Privacidad del navegador de Preferencias, como se muestra en la imagen siguiente.

   ![](assets/always-allow-safari13.png)

