---
title: Información general sobre MVPD
description: Información general sobre MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2736'
ht-degree: 0%

---


# Información general sobre MVPD {#mvpd-overview}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Introducción {#intro}

Esta descripción general está dirigida a los distribuidores de programación de vídeo multicanal (MVPD). Para obtener documentación adicional, incluidas las guías de inicio e integración, consulte la sección Información relacionada al final de este documento.



TV Everywhere (TVE) es el ya conocido movimiento de la industria que permite a los suscriptores de televisión de pago acceder al contenido que ya pagan, en múltiples dispositivos, tanto dentro como fuera de sus hogares.  Para los proveedores de televisión de pago, TVE crea nuevas oportunidades, tanto para preservar las relaciones con los clientes existentes como para habilitar otras nuevas. Sin embargo, junto con estas oportunidades surgen desafíos. En el entorno TVE, los programadores proporcionan el contenido, pero los MVPD contienen la información del cliente para verificar que los posibles visualizadores son suscriptores válidos.



Coordinar la autenticación y autorización de los espectadores con un programador puede ser sencillo, pero coordinar con docenas o cientos de programadores diferentes se vuelve cada vez más complejo. Sin embargo, con Adobe® Pass, los MVPD solo necesitan implementar una integración simple para obtener acceso a todo el ecosistema de TVE, incluyendo programadores como NBCUniversal Media, Turner Broadcasting (TBS, TNT, CNN), Fox Broadcast Networks, Hulu, etc.  La autenticación de Adobe Primetime proporciona un marco de integración que hace que la determinación de la asignación de derechos de usuario sea simple y segura.



Línea inferior: La autenticación de Adobe Primetime medita de forma segura las transacciones de derechos entre programadores y MVPD, lo que facilita el acceso del visor al contenido de suscripción. En otras palabras, la autenticación de Adobe Primetime facilita y agiliza el acceso de los clientes adecuados al contenido adecuado.


Con la autenticación de Adobe Primetime, los MVPD reciben:

Fácil integración con programadores.  Ofrezca conectividad instantánea desde múltiples propietarios de contenido con una sola integración.

Participación del cliente mejorada.  Admita una experiencia fluida y con marca, ya que sus clientes ven el contenido en varias plataformas y dispositivos.

Autenticación segura.  Asegúrese de que solo los usuarios y dispositivos autorizados tengan acceso al contenido premium y (opcionalmente) limite la cantidad de dispositivos y flujos simultáneos que pueden conectarse por cuenta familiar.

## Preguntas frecuentes {#faq}

¿Qué nivel de seguridad tiene la autenticación de Adobe Primetime? La prioridad número uno de la arquitectura de autenticación de Adobe Primetime es garantizar que solo los visores autorizados estén autenticados y que se les conceda acceso al contenido premium. La autenticación de Adobe Primetime enlaza estrechamente el acceso a los dispositivos de visualización y puede ayudar a limitar los flujos, sesiones y/o dispositivos de un hogar determinado.


¿Se requiere Flash Player? La autenticación de Adobe Primetime para TV en todas partes no depende del reproductor ni de la plataforma, ya que se integra con cualquier aplicación de reproducción, incluidos Silverlight y HTML5. Además, la autenticación de Adobe Primetime proporciona compatibilidad nativa para dispositivos como teléfonos y tabletas que ejecutan iOS y Android.


¿Qué dispositivos admite la autenticación de Adobe Primetime? La autenticación de Adobe Primetime es compatible con prácticamente cualquier dispositivo que tenga el kit web HTML5 para experiencias de visualización dentro del navegador. Además, la autenticación de Adobe Primetime continúa implementando kits de desarrollo de software nativos (SDK) para varias plataformas específicas del dispositivo, incluidas iOS, Android™, Xbox360 (obsoleto) y aplicaciones de Adobe Air® (obsoleto). Más recientemente, la autenticación de Adobe Primetime estableció una solución sin cliente para dispositivos que no pueden procesar páginas de navegador (por ejemplo, televisores &quot;inteligentes&quot;, decodificadores y consolas de juegos).  La capacidad de procesar páginas de navegador es un requisito para autenticar usuarios con MVPD.


¿La autenticación de Adobe Primetime es compatible con los estándares emergentes para TV en todas partes? La autenticación de Adobe Primetime es compatible con la especificación CableLabs OLCA (Acceso a contenido en línea), que proporciona requisitos técnicos y arquitectura para la entrega de vídeo a un cliente de televisión de pago desde fuentes en línea. Adobe participó en el proyecto conjunto de pruebas de interconexión de CableLabs en junio de 2011 y aprobó el proceso de prueba para la implementación de un proveedor de servicios. La autenticación de Adobe Primetime se verifica (completa y prueba) según las especificaciones OLCA para la autenticación. El componente de autorización se ha completado, pero la verificación de prueba espera actualmente el lanzamiento del entorno de prueba de CableLabs. El Adobe también es miembro activo del OATC (Open Authentication Technical Consortium) y participa en varios proyectos de elaboración de especificaciones de los subcomités como parte de ese órgano.



¿Qué es la autenticación? La autenticación es el proceso en el que un MVPD confirma que un usuario determinado es un cliente conocido.



¿Qué es la autorización? La autorización es el proceso en el que un MVPD confirma que un usuario autenticado tiene una suscripción válida a un recurso determinado.



## Arquitectura {#architecture}

La autenticación de Adobe Primetime es un servicio alojado que permite una integración rápida del back-end (servidor a servidor) basada en las reglas comerciales requeridas tanto por los MVPD como por los Programadores. Esto significa un rápido lanzamiento al mercado para todas las partes, un entorno más seguro para prevenir el fraude y una experiencia de cliente superior, con más contenido de TV disponible para más personas en más plataformas.


La autenticación de Adobe Primetime se ofrece a través del modelo Software as a Service (SaaS) y permite una comunicación más segura entre los usuarios finales, los MVPD y los programadores, a fin de validar el derecho al contenido. Los componentes principales del servicio incluyen lo siguiente:

Servidor: el servidor de autenticación de Adobe Primetime alojado. Se trata de un servidor de aplicaciones que interviene en la comunicación de canal de retorno (servidor a servidor) con los sistemas de autenticación de los MVPD.
Lado del cliente: Access Enabler del lado del cliente: Access Enabler es un archivo pequeño que se carga en la página web del programador o en la aplicación del reproductor. Proporciona API de derechos a la aplicación de visualización de contenido del programador y se comunica con el servidor de autenticación de Adobe Primetime.
Servicios web sin cliente (para dispositivos que no admiten la web): servicios web RESTful que proporcionan API de asignación de derechos para dispositivos como televisores inteligentes, consolas de juegos y receptores de Internet.

>[!NOTE]
>
>Como MVPD, sus servicios web deben ser capaces de reconocer las solicitudes de autenticación y autorización de la autenticación de Adobe Primetime y responder con los datos requeridos en el formato esperado.

La autenticación de Adobe Primetime le permite proporcionar a los clientes una administración de identidades federada, también conocida como autenticación y autorización de inicio de sesión único (SSO). Con la autenticación de Adobe Primetime, no es necesario que los suscriptores inicien sesión de nuevo después de su primera autenticación, siempre y cuando la MVPD permita que dicha autenticación persista. (Generalmente, 30 días). Para lograr esto, la autenticación de Adobe Primetime proporciona un dominio común para los tokens de autenticación de nuestros clientes. Esta información de estado de autenticación está disponible para todos los sitios participantes que están integrados con un MVPD determinado.


Actualmente, la mayoría de las integraciones de autenticación de Adobe Primetime con MVPD utilizan el protocolo SAML, uno de los estándares de autenticación principales. La autenticación de Adobe Primetime actúa como proveedor de servicios proxy en la arquitectura SAML y persiste en la respuesta de autenticación SAML como token seguro en el dominio común de Adobe. La autenticación de Adobe Primetime es compatible con SAML 2.0. Sin embargo, aunque la autenticación de Adobe Primetime se utiliza generalmente con soluciones SAML SSO en este punto, la arquitectura de autenticación de Adobe Primetime no está vinculada a ningún protocolo específico. Por lo tanto, la compatibilidad con nuevos protocolos, como uno basado en OAuth 2.0 o protocolos personalizados, se puede agregar con el tiempo.


Adobe trabaja con el equipo técnico de un MVPD para configurar la autenticación de Adobe Primetime para satisfacer las necesidades de cualquier integración existente. La integración es gratuita para los MVPD, asumiendo una integración &quot;estándar&quot; y requisitos de soporte mínimos (documentación y soporte básico de correo electrónico). Si un MVPD requiere soporte significativo o un plazo escalado, se puede cobrar una tarifa de soporte o el proveedor puede querer trabajar con un tercero familiarizado con nuestra solución como Synacor.


La autenticación de Adobe Primetime también admite la administración eficiente de la lógica empresarial de MVPD, como se indica a continuación:

En el caso de la lógica empresarial independiente que puede aplicar el MVPD cuando se recibe una solicitud de autorización, Adobe proporciona los datos necesarios para respaldar la aplicación lógica empresarial cuando el MVPD recibe una solicitud de autorización. Estos datos pueden incluir, entre otros, el ID de dispositivo único para el usuario que realiza la solicitud y la dirección IP del dispositivo.

Para la lógica empresarial que requiere la intervención del usuario o la gestión específica por parte de la solución de Adobe, Adobe puede mantener algunas propiedades personalizadas para cada MVPD. Estas configuraciones y políticas específicas de MVPD incluyen la habilitación de flujos de trabajo predefinidos que pueden iniciarse en puntos específicos del flujo de trabajo de nivel superior. Para obtener más información sobre la compatibilidad con propiedades personalizadas, póngase en contacto con su representante de Adobe.

El diagrama siguiente ilustra la relación entre MVPD y Programmer con estos componentes de autenticación de Adobe Primetime:

![](assets/high-level-architecture-nflows.png)

*Figura: Arquitectura y flujos de alto nivel*

## Componentes de autenticación de Adobe Primetime {#components}

A continuación se proporciona una descripción general de algunos de los componentes principales del ecosistema de autenticación de Adobe Primetime. Estos incluyen:

* [Access Enabler / Clientless Web Services](#ae)
* [Servidor back-end alojado en Adobe](#backend)
* [Tokens](#tokens)

### Access Enabler / Clientless Web Services {#ae}

Access Enabler facilita todas las interacciones de autenticación y autorización con el usuario y se ejecuta localmente en su sistema. Access Enabler gestiona los flujos de trabajo de asignación de derechos reales con el MVPD, mientras que el programador mantiene la responsabilidad de la página web o la aplicación del reproductor de nivel superior.

La autenticación de Adobe Primetime proporciona servicios web sin cliente para dispositivos que no pueden renderizar páginas web.  Para estos dispositivos, el proceso de asignación de derechos se inicia y el contenido se visualiza en el dispositivo inteligente, mientras que la autenticación con un MVPD se realiza en un dispositivo compatible con web (PC, smartphone y tablet).

El habilitador de acceso:

* Inicia los flujos de trabajo de autenticación y autorización específicos de MVPD.
* Almacena en caché las respuestas de autorización correctas por recurso/canal del programador para minimizar el tráfico de solicitud innecesario.
* Se puede configurar para flujos de trabajo predefinidos específicos de cada MVPD, como el registro explícito del dispositivo.
* Está disponible en los siguientes formularios:
   * Archivo SWF que puede ejecutar el motor de ejecución del Flash Player
   * Un archivo JS ejecutado directamente por el explorador
   * Un Access Enabler nativo para varias plataformas, incluidas iOS, Android y Xbox.

### Servidor back-end alojado en Adobe {#backend}

El servidor back-end de autenticación de Adobe Primetime, alojado por el Adobe:

* Proporciona los flujos de trabajo de autenticación y autorización con los MVPD que requieren comunicación servidor a servidor entre la autenticación de Adobe Primetime y el operador.
* Mantiene la configuración para sitios y aplicaciones de Programador.
* Aloja los archivos de componente descargables de Access Enabler.
* Genera tokens de autenticación y autorización.

### Tokens {#tokens}

La solución de autorizaciones de autenticación de Adobe Primetime se centra en la generación de fragmentos de datos específicos que se obtienen tras la correcta finalización de los flujos de trabajo de autenticación/autorización. Estos datos se denominan tokens. Tienen una vida útil limitada y se almacenan de forma segura en ubicaciones dependientes de la plataforma. Una vez caducado, los tokens deben volver a emitirse mediante el reinicio de los flujos de trabajo de autenticación o autorización.

Existen tres tipos de tokens que se emiten durante los flujos de trabajo de autenticación/autorización. Dos son &quot;de larga duración&quot;, lo que proporciona continuidad en la experiencia de visualización del usuario. La tercera, un token de corta duración, proporciona soporte para las prácticas recomendadas del sector para mitigar el fraude mediante la extracción de flujo. Los valores de tiempo de vida (&quot;TTL&quot;) de los tokens se establecen según los acuerdos entre MVPD y los programadores. Usted decide sobre un valor TTL que mejor sirva a su negocio y a sus clientes.

**El token de autenticación de larga duración**. El éxito de la autenticación se produce cuando un cliente utiliza la autenticación de Adobe Primetime para iniciar sesión correctamente en su cuenta MVPD. A continuación, la autenticación de Adobe Primetime genera un token de autenticación de larga duración (&quot;authN&quot;) vinculado al dispositivo solicitante y (en función del MVPD) un identificador único global (&quot;GUID&quot;) que identifica de forma anónima al usuario.

**El token de autorización de larga duración**. Tras una autorización correcta, la autenticación de Adobe Primetime crea un token de autorización de larga duración (&quot;authZ&quot;). Este token no es portátil, ya que está vinculado al dispositivo solicitante y a un recurso protegido específico (por ejemplo, un canal, una serie o un episodio). Access Enabler utiliza el token authZ de larga duración para crear los tokens de medios de corta duración que se utilizan para el acceso de visualización real.

**El testigo breve de los medios de comunicación**. Una vez autorizado el usuario, la autenticación de Adobe Primetime genera un token authZ y lo utiliza para generar un token de medios de corta duración de un solo uso que está firmado por Adobe y cifrado para evitar alteraciones durante el intercambio. Dado que el token de corta duración está expuesto al sitio de incrustación a través de la API de Access Enabler o los servicios web sin cliente, antes de proporcionar acceso al recurso protegido, el servidor de medios del programador debe utilizar un componente de autenticación de Adobe Primetime, el verificador de tokens de medios, para validar el token.

## Ciclo de vida de integración de MVPD {#lifecycle}

La siguiente ilustración muestra el ciclo de vida de la integración entre la autenticación de Adobe Primetime y un MVPD.

![](assets/mvpd-int-lifecycle.png)

*Figura: Ciclo de vida de integración de MVPD*

## Diagrama de flujo de derechos {#chart}

El siguiente diagrama de flujo presenta el proceso general de confirmación de la asignación de derechos mediante la autenticación de Adobe Primetime:

![](assets/authn-authz-entitlmnt-flow.png)

*Figura: Proceso de confirmación de la asignación de derechos mediante la autenticación de Adobe Primetime*

## Pasos de autenticación {#authn-steps}

Los siguientes pasos presentan un ejemplo del flujo de autenticación de Adobe Primetime.  Esta es la parte del proceso de asignación de derechos en la que un programador determina si el usuario es un cliente válido de un MVPD.  En esta situación, el usuario es un suscriptor válido de un MVPD.  El usuario está intentando ver contenido protegido mediante una aplicación de Flash del programador:

1. El usuario navega a la página web del programador, que carga la aplicación de Flash del programador y los componentes de Access Enabler de autenticación de Adobe Primetime en el equipo del usuario. La aplicación de Flash utiliza Access Enabler para establecer la identificación del programador con la autenticación de Adobe Primetime, y la autenticación de Adobe Primetime asigna al activador de acceso con la configuración y los datos de estado para ese programador (el &quot;solicitante&quot;). Access Enabler debe recibir estos datos del servidor antes de realizar cualquier otra llamada API.  Nota técnica: el programador establece su identidad con el activador de acceso `setRequestor()` método; para obtener más información, consulte la [Guía de integración del programador](/help/authentication/programmer-integration-guide-overview.md).
1. Cuando el usuario intenta ver el contenido protegido del programador, la aplicación del programador presenta al usuario una lista de MVPD, desde los cuales el usuario selecciona un proveedor.
1. El usuario se redirige a un servidor de autenticación de Adobe Primetime, donde se crea una solicitud SAML cifrada para el MVPD seleccionado por el usuario. Esta solicitud se envía como una solicitud de autenticación en nombre del programador al MVPD. Según el sistema de MVPD, el navegador del usuario se redirige al sitio de MVPD para iniciar sesión, o se crea un iFrame de inicio de sesión en la aplicación del programador.
1. En cualquier caso (redirección o iFrame), el MVPD acepta la solicitud y muestra su página de inicio de sesión.
1. El usuario inicia sesión con el MVPD, el MVPD valida el estado del usuario como cliente que paga y, a continuación, el MVPD crea su propia sesión HTTP.
1. Cuando se valida el usuario, el MVPD crea una respuesta (SAML y cifrada), que el MVPD devuelve a la autenticación de Adobe Primetime.
1. La autenticación de Adobe Primetime recibe la respuesta MVPD, ve que hay una sesión HTTP de autenticación de Adobe Primetime abierta, valida la variable [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) respuesta de MVPD, y redirige al sitio del programador.
1. El sitio del programador se vuelve a cargar, el activador de acceso se vuelve a cargar y el programador llama a setRequestor() de nuevo.  La segunda llamada a setRequestor() es necesaria porque la configuración actual ha cambiado: ahora hay un indicador presente que informa al Access Enabler de que hay un token AuthN esperando a generarse en el servidor.
1. Access Enabler observa que hay una autenticación pendiente y solicita el token al servidor de autenticación de Adobe Primetime. El token se recupera del servidor invocando las funciones DRM del Flash Player.
1. El token AuthN se almacena en la caché LSO de Flash Player del programador; la autenticación ya ha finalizado y la sesión se ha destruido en el servidor de autenticación de Adobe Primetime.

## Pasos de autorización {#authz-steps}

Los siguientes pasos continúan a partir de la sección anterior ([Pasos de autenticación](#authn-steps)):

1. Cuando el usuario intenta acceder al contenido protegido del programador, la aplicación del programador comprueba primero si hay un token AuthN en el equipo o dispositivo local del usuario.  Si ese token no está ahí, entonces la variable [Pasos de autenticación](#authn-steps) se siguen los anteriores.  Si el token AuthN está allí, el flujo de autorización continúa con la aplicación del programador iniciando una llamada al habilitador de acceso con una solicitud para obtener los derechos de visualización del usuario para un elemento específico de contenido protegido.
1. El elemento específico de contenido protegido se representa mediante un &quot;identificador de recurso&quot;.  Podría ser una cadena simple o una estructura más compleja, pero en cualquier caso la naturaleza del identificador del recurso se acuerda con antelación entre el Programador y el MVPD.  La aplicación del programador pasa el identificador de recurso al activador de acceso.  Access Enabler comprueba si hay un token AuthZ en el equipo o dispositivo local del usuario.  Si el token AuthZ no está allí, Access Enabler pasa la solicitud al servidor de autenticación de Adobe Primetime back-end.
1. El servidor de autenticación de Adobe Primetime se comunica con el extremo de autorización de los MVPD mediante protocolos estandarizados.  Si la respuesta de MVPD indica que el usuario está autorizado a ver el contenido protegido, el servidor de autenticación de Adobe Primetime crea un token AuthZ y lo devuelve al activador de acceso, que almacena el token AuthZ en el equipo del usuario.
1. Con un token AuthZ almacenado en el equipo o dispositivo del usuario, la aplicación del programador llama a Access Enabler para obtener un token multimedia del servidor de autenticación de Adobe Primetime y proporciona ese token a la aplicación del programador.
1. Por último, la aplicación del programador utiliza el componente Verificador de tokens de medios para confirmar que el usuario correcto está viendo el contenido correcto y, con el token de medios en su lugar, el usuario puede ver el contenido protegido.

<!--
>![RELATEDINFORMATION]
>
>*   Kickstart Guides, [MVPD kickstart](/help/authentication/mvpd-kickstart-guide.md) and [programmer kickstart](/help/authentication/programmer-kickstart-guide.md). These guides explain the initial steps to take to begin integrating with Adobe Primetime authentication.
>
>*   [MVPD Integration Guide](/help/authentication/mvpd-kickstart-guide.md). This is a lower level technical guide for MVPDs, directed primarily to the software engineers who code and test the applications and systems involved in the integration.
>
>*   [Overview For Programmers](/help/authentication/programmer-overview.md). The same high level of conceptual information as in this MVPD overview, but directed toward the content providers (Programmers).
-->
