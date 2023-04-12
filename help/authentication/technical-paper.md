---
title: Acerca de la autenticación de Adobe Primetime y TV en todas partes
description: Acerca de la autenticación de Adobe Primetime y TV en todas partes
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '6288'
ht-degree: 0%

---


# Acerca de la autenticación de Adobe Primetime y TV en todas partes {#about-auth-tve}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Acerca de TV en todas partes {#about-tve}

Los televidentes de hoy pueden conectarse en cualquier momento o lugar, y esperan que su capacidad para acceder a contenido de televisión de pago esté allí con ellos. Además, las audiencias ven el contenido utilizando una gama cada vez mayor de dispositivos compatibles con Internet, entre los que se incluyen:

* Portátiles
* Comprimidos
* Smartphones
* Sitios web
* Aplicaciones federadas
* Consolas de juegos
* Cuadros superiores
* Televisores inteligentes

TV en todas partes es el movimiento de la industria que apoya la capacidad de los suscriptores de Pay TV de acceder al mismo contenido que ya están pagando, a través de múltiples dispositivos, tanto dentro como fuera de sus hogares. Si bien la mayor parte de la visualización de televisión sigue produciéndose en la televisión lineal convencional, el aumento del consumo se debe a un desplazamiento del tiempo en el contenido, el vídeo en línea y las pantallas alternativas. Como resultado, el mercado de distribución de video hoy está en un estado de interrupción, y TV en todas partes ha surgido como la solución que alinea los intereses de programadores, proveedores de televisión de pago y suscriptores de televisión de pago.


El objetivo técnico de TV Everywhere es permitir a los clientes de televisión de pago acceder al contenido al que ya se han suscrito en todos sus dispositivos y plataformas.


Los objetivos comerciales de TV Everywhere son:

* **Mantener relaciones de cliente existentes y habilitar nuevas**
* Permita a los programadores y propietarios de contenido llegar a la audiencia más amplia y obtener más valor del contenido premium
* Ampliar marcas mediante la interacción directa en línea con los espectadores

## Desafíos de TV en todas partes {#tve-challenges}

Junto con las oportunidades de TV en todas partes vienen desafíos. En el centro de todo esto está el derecho. Antes de que un visor acceda al contenido de suscripción, alguien debe determinar si tiene derecho a ese acceso.

¿El usuario tiene una suscripción con un proveedor de televisión de pago? En caso afirmativo, ¿incluye esa suscripción el contenido que se está solicitando? El derecho es especialmente difícil de determinar directamente para los programadores y propietarios de contenido, ya que son los operadores de televisión de pago los que tienen los datos de identificación de sus clientes, así como los privilegios de acceso de sus clientes.


Más allá de la asignación de derechos, hay una serie de desafíos técnicos y de integración relacionados, entre ellos:

* Desarrollo y aplicación de una estrategia integral para varios dispositivos
* Coordinar la infinidad de relaciones entre programadores y proveedores de televisión de pago
* Prevención del acceso fraudulento o del abuso de las condiciones de servicio
* Ofrecer una experiencia de autenticación coherente y sin frustraciones a los usuarios de distintos sitios web y aplicaciones
* Mantener un rápido tiempo de salida al mercado para mantenerse al día con los acuerdos de afiliación
* Administración de los costes asociados con varias integraciones

Estos desafíos hacen que la realización y el mantenimiento de integraciones complejas y directas entre programadores y los sistemas de autenticación de múltiples proveedores de televisión de pago requieran gran cantidad de recursos, tiempo y sofisticación técnica.


¿La solución? **Autenticación Adobe® Primetime**.

## Introducción a la autenticación de Adobe Primetime {#authentication-intro}

Con la autenticación de Adobe Primetime, los programadores y los proveedores de televisión de pago solo necesitan realizar una integración sencilla, utilizando las API de autenticación de Adobe Primetime, para obtener acceso a todo el ecosistema, lo que incluye:

* Programadores como Turner Broadcasting (TBS, TNT, CNN), Fox Broadcast Networks y Hulu

* Todos los principales proveedores de televisión de pago de EE. UU., que comprenden más del 90% de todos los hogares de televisión de pago de EE. UU.

Además, la autenticación de Adobe Primetime proporciona el marco que hace que la autenticación y autorización de usuarios sea simple y segura.

![](assets/programmers-connect-authn.png)

*Figura 1: Sólo algunos de los programadores y proveedores de televisión de pago que se conectan a través de la autenticación de Adobe Primetime...*

Adobe Pass media de forma segura las transacciones de derechos entre programadores y proveedores de televisión de pago, lo que facilita el acceso del visor al contenido de suscripción. O, en otras palabras...

**La autenticación de Adobe Primetime facilita y agiliza el acceso de los clientes adecuados al contenido adecuado.**

**¿Para quién es la autenticación de Adobe Primetime?**

* **Programadores** que desean integrarse fácilmente con proveedores de televisión de pago (también conocidos como &quot;MVPD&quot; o &quot;Distribuidores de Programación de Vídeo Multicanal&quot;), llegando a la audiencia más amplia, para obtener los ingresos óptimos. Mediante la autenticación de Adobe Primetime, los programadores pueden autenticar los visualizadores en todos los proveedores principales, independientemente de la plataforma del cliente.

* **Proveedores de TV de pago/MVPD** que buscan una conectividad sin problemas con varios programadores y una mayor satisfacción del cliente al facilitar el acceso al contenido de suscripción en línea.

* **Clientes de televisión de pago** que desean un acceso fácil al contenido al que ya se suscriben, donde quiera que estén, sin coste adicional. El inicio de sesión único proporciona autenticación segura del visor en la web o en todas las aplicaciones móviles, sin necesidad de descargas de clientes ni de registros repetidos, así como una buena experiencia de usuario.

Para **Programadores**, la autenticación de Adobe Primetime proporciona:

* Fácil integración y conectividad instantánea con los principales proveedores de TV de pago, sin el dolor de múltiples integraciones directas
* Optimización de los ingresos por suscripción (licencia) y publicidad al admitir la mayor cantidad de audiencias posibles para el contenido
* Autenticación segura, con acceso a contenido premium concedido solo a usuarios/dispositivos autorizados
* Un marco abierto y flexible que no sea ni para el reproductor ni para la plataforma DRM; la reproducción puede producirse en una amplia gama de plataformas, incluidas iOS, Android, Windows 8, consolas de juegos, decodificadores, etc.
* Compatibilidad con cualquier tecnología DRM, como el Flash Access de Adobe® o Play Ready®.
* Compatibilidad con autenticación y autorización de inicio de sesión único (SSO), de modo que los suscriptores no tengan que iniciar sesión de nuevo después de su primera autenticación en su propio sistema.


Para **Proveedores de TV de pago/MVPD**, la autenticación de Adobe Primetime proporciona:

* Fácil integración con los propietarios de contenido, que ofrece conectividad instantánea con varios programadores mediante una sola integración
* Se ha mejorado la participación de los clientes al ofrecer compatibilidad con una experiencia fluida y de marca a medida que ven el contenido en varias plataformas y dispositivos
* Autenticación segura que garantiza que solo los usuarios/dispositivos autorizados tengan acceso al contenido premium y (opcionalmente) limita el número de dispositivos y flujos simultáneos que pueden conectarse por cuenta familiar.


Para **Clientes de televisión de pago**, la autenticación de Adobe Primetime proporciona:

* **¡TV en todas partes!**

El resto de este documento proporciona una introducción técnica a la autenticación de Adobe Primetime.  Aunque gran parte de lo siguiente se centra en la integración de programadores, también hay información general y específica que se aplica a los proveedores de televisión de pago. Este documento también destaca la seguridad y la integridad de cómo funciona la autenticación de Adobe Primetime como una solución para TV en todas partes. Para obtener más información además de este documento, póngase en contacto con su representante del Adobe o rellene el formulario de solicitud de información [here](https://www.adobe.com/).

## Componentes arquitectónicos {#arch-building-blocks}

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/import-pc7mz3dfnv/check.gif) A continuación se describen las transacciones centrales de derechos de autenticación y autorización. La autenticación es el proceso de confirmar con un proveedor de televisión de pago que un usuario determinado es un cliente conocido. La autorización es el proceso en el que un proveedor de televisión de pago confirma que un usuario autenticado tiene una suscripción válida a un recurso determinado.
La autenticación de Adobe Primetime consta de los siguientes componentes básicos:

* Componente cliente (uno de los siguientes):

   * Access Enabler: biblioteca específica de la plataforma; proporciona API fáciles de usar y ejemplos de código para implementar los flujos de derechos
   * La API sin cliente - servicios web RESTful; proporciona extremos de flujo de derechos para plataformas sin capacidades de renderización de páginas web (como consolas de juegos, cuadros superiores, etc.)

* Servidores back-end alojados en Adobe
* El verificador de tokens de medios
* Un medio de intercambio seguro y central (tokens)

En un nivel básico, la autenticación de Adobe Primetime consta de tres componentes (Access Enabler, los servidores back-end alojados en Adobe y Media Token Verifier) y un elemento central de intercambio (tokens).

### Componentes del cliente {#client-components}

* Access Enabler
* API sin cliente

#### Access Enabler {#access-enabler}

En plataformas totalmente compatibles (incluidas la web, iOS, Android y Windows 8), los programadores interactúan con la autenticación de Adobe Primetime mediante el componente cliente Access Enabler. Este componente facilita todas las interacciones de autenticación y autorización con el cliente.  Access Enabler se ejecuta localmente en su sistema. Cuando un usuario accede a un sitio o aplicación de Programador y solicita contenido, el componente Access Enabler alojado o mantenido en Adobe se carga silenciosamente en segundo plano.

Access Enabler gestiona los flujos de trabajo de asignación de derechos reales, mientras que el Programador mantiene la responsabilidad de la página web o la aplicación del reproductor de nivel superior que implementa la interfaz de usuario e interactúa con Access Enabler. Estas interacciones se realizan mediante un sistema asincrónico de funciones y retrollamadas, definido por la API de Access Enabler.

Estos son los flujos de asignación de derechos básicos, implementados fácilmente mediante la API de Access Enabler:

* Configuración de la identidad del solicitante (programador)
* Comprobación/obtención de la autenticación de usuario contra un operador de televisión de pago específico (el &quot;proveedor de identidad&quot;)
* Comprobación u obtención de la autorización de un usuario para un recurso determinado
* Cerrar sesión del usuario

Access Enabler también proporciona los siguientes servicios:

* Valida las consultas del programador, incluido el estado de registro de clientes específicos, sus dominios y sus recursos/canales.
* Proporciona los datos que crean la lista de operadores de televisión de pago desde la que el usuario selecciona a su proveedor. Esta lista también se valida y define como corresponde para el programador desde el que se origina la solicitud.
* Inicia los flujos de trabajo de autenticación y autorización específicos del operador de Pay TV.
* Almacena en caché las respuestas de autorización correctas por recurso/canal del programador para minimizar el tráfico de solicitud innecesario.
* Se puede configurar para flujos de trabajo predefinidos específicos de cada operador de televisión de pago, como el registro explícito del dispositivo.

Según el sitio web o la aplicación del reproductor, Access Enabler puede adoptar los siguientes formularios:

* Archivo SWF que puede ejecutar el motor de ejecución del Flash Player
* Un archivo JS ejecutado directamente por el explorador
* Un Access Enabler nativo para plataformas compatibles (incluidas iOS, Android y Windows 8)

#### API sin cliente {#clientless-api}

El método de API sin cliente es para &quot;dispositivos inteligentes&quot; (consolas de juegos, receptores de televisión y televisores inteligentes) que no admiten exploradores web (necesarios para la autenticación con MVPD).  En el enfoque sin clientes, las aplicaciones de dispositivos inteligentes se comunican directamente con la autenticación de Adobe Primetime a través de las API de servicios web RESTful para todo excepto para la autenticación, que se realiza en una aplicación de segunda pantalla (explorador). En otras palabras, no se usa la biblioteca del lado del cliente de Access Enabler. En su lugar, los desarrolladores de aplicaciones de dispositivos inteligentes consumen directamente las API de servicios web de autenticación de Adobe Primetime para implementar los flujos de derechos.

### Servidores back-end alojados en Adobe {#adobe-backend-servers}

Los servidores back-end de autenticación de Adobe Primetime, alojados por Adobe:

* Aprovisionar los flujos de trabajo de autenticación y autorización con los proveedores de televisión de pago que requieren comunicación servidor a servidor entre la autenticación de Adobe Primetime y el operador.
* Mantener la configuración para sitios y aplicaciones programadores.
* Aloje los archivos de componente descargables de Access Enabler.
* Proporcione los extremos del servicio web RESTful para la integración de API sin cliente.
* Genere (y en algunos casos almacene) tokens de autenticación y autorización.

### Tokens y el verificador de tokens de medios {#tokens-media-token-verifier}

La solución de autorizaciones de autenticación de Adobe Primetime se centra en la generación de fragmentos de datos específicos que se obtienen tras la correcta finalización de los flujos de trabajo de autenticación/autorización. Estos datos se denominan tokens. Tienen una vida útil limitada y se almacenan de forma segura, ya sea en ubicaciones dependientes de la plataforma en el cliente o en servidores de Adobe en el caso de la solución API sin cliente. Una vez caducado, los tokens deben volver a emitirse mediante el reinicio de los flujos de trabajo de autenticación o autorización.

Existen tres tipos de tokens que causan problemas de autenticación de Adobe Primetime durante los flujos de trabajo de autenticación/autorización. Dos son &quot;de larga duración&quot;, lo que proporciona continuidad en la experiencia de visualización del usuario. La tercera, un token de corta duración, proporciona soporte para las prácticas recomendadas del sector para mitigar el fraude (donde el fraude incluye, por ejemplo, vulnerabilidades como la extracción de flujo). Los valores de tiempo de vida (&quot;TTL&quot;) se establecen en base a acuerdos entre programadores y proveedores de televisión de pago, que acuerdan un valor que mejor sirva a todos los involucrados.

#### Token de autenticación (de larga duración) {#long-lived-auth-token}

El éxito de la autenticación se produce cuando un cliente utiliza la autenticación de Adobe Primetime para iniciar sesión correctamente en su cuenta de televisión de pago. A continuación, la autenticación de Adobe Primetime genera un token de autenticación (AuthN) de larga duración vinculado al dispositivo solicitante y (en función del proveedor de televisión de pago) un identificador único global (&quot;GUID&quot;) que identifica de forma anónima al usuario.

* La autenticación de Adobe Primetime almacena el token AuthN de forma segura en una ubicación donde está disponible para todas las aplicaciones que utilizan la autenticación de Adobe Primetime. Para integraciones de Access Enabler, los tokens se almacenan de forma segura en el lado del cliente.  La autenticación de Adobe Primetime utiliza el token AuthN para realizar consultas de autorización posteriores en nombre del usuario.
* En un momento dado, solo se almacena un token AuthN. Siempre que se emite un nuevo token AuthN y ya existe uno antiguo, el nuevo token sobrescribe el valor almacenado existente.

#### Token de autorización (de larga duración) {#long-lived-authriz-token}

Tras una autorización correcta, la autenticación de Adobe Primetime crea un token de autorización de larga duración (&quot;AuthZ&quot;). Este token no es portátil, ya que está vinculado al dispositivo solicitante y a un recurso protegido específico (por ejemplo, un canal, una serie o un episodio).

* La autenticación de Adobe Primetime almacena el token AuthZ de forma segura, junto con otros tokens de autorización de otros recursos.  De nuevo, al igual que con los tokens de AuthN, en las plataformas que utilizan Access Enabler el token se almacena localmente en el cliente; en plataformas que utilizan la API sin cliente, los tokens se almacenan en los servidores de autenticación de Adobe Primetime.
* El tiempo de vida (TTL) del token de AuthZ de larga duración se define generalmente en el rango de días a semanas, según el acuerdo específico entre el proveedor de televisión de pago y el programador.
* En un momento dado, solo se almacena un token AuthZ por recurso. Puede haber varios tokens de autorización almacenados, siempre que estén asociados a distintos recursos. Siempre que se emite un nuevo token de autorización y ya existe uno antiguo para el mismo recurso, el nuevo token sobrescribe el valor almacenado en caché existente.
* La autenticación de Adobe Primetime utiliza el autenticador AuthZ de larga duración para crear los tokens de medios de corta duración que se utilizan para el acceso de visualización real.

#### Token de medios de corta duración {#short-lived-media-token}

Una vez que la autenticación de Adobe Primetime genera el token AuthZ, utiliza ese token para generar un token de medios de breve duración de un solo uso que se firma con Adobe y se cifra para evitar alteraciones durante el intercambio:

* El TTL del token de corta duración (predeterminado: 5 minutos) está configurado para permitir problemas de sincronización de reloj entre el servidor que genera el token y el servidor que valida el token.
* El token de corta duración se expone al sitio de incrustación antes de proporcionar acceso al recurso protegido, por lo que el programador debe validar el token, utilizando el verificador de tokens de medios para integraciones de Access Enabler o el servicio de verificador de tokens en el caso de integraciones de API sin cliente.

#### Verificador de tokens de medios {#media-token-verifier}

Los programadores son responsables de integrar la biblioteca del verificador de tokens de medios en su servidor de aplicaciones existente, de modo que el verificador pueda realizar las validaciones finales del usuario antes de que se inicie realmente un flujo de vídeo. La biblioteca del verificador de tokens de medios define:

* Una API de verificación de tokens que recupera información del token, como si es válida, la hora en que se emitió el token y otros datos relevantes
* La clave pública de Adobe utilizada para comprobar que el token viene de Adobe
* Una implementación de referencia que muestra cómo utilizar la API de Verifier y cómo utilizar la clave pública de Adobe contenida en la biblioteca para comprobar su origen

![](assets/high-level-architecture-nflows.png)

*Figura 2: Arquitectura de alto nivel del ecosistema de autenticación de Adobe Primetime en una integración de Access Enabler*

## Integración con la autenticación de Adobe Primetime {#integrate-auth}

Tanto si es un proveedor de televisión de pago como un programador, el proceso de integración con la autenticación de Adobe Primetime requiere una parte de su participación activa. A continuación se describe cada uno de estos procesos.

### El proceso de proveedor de televisión de pago

La responsabilidad principal del proveedor de televisión de pago con la autenticación de Adobe Primetime es validar que el usuario solicitante es, de hecho, un suscriptor conocido que tiene derecho a acceder al contenido del programador. En un nivel superior, el proceso de autenticación de Adobe Primetime para la integración con un nuevo proveedor de televisión de pago requiere los siguientes pasos:

1. El proveedor firma el Acuerdo de no divulgación de la autenticación de Adobe Primetime (NDA).
1. El proveedor proporciona el Adobe de las especificaciones de su sistema de autenticación y autorización. Para la integración más sencilla, se recomienda que los operadores de televisión de pago tengan un proveedor de identidad (IdP) basado en SAML para la autenticación y la capacidad de comunicarse mediante el protocolo de acceso SOAP para la autorización.
1. El proveedor establece la conectividad entre sus servidores y los servidores de autenticación de Adobe Primetime. Esto incluye el suministro de extremos y la lista de IP.
1. Versión de precalificación y FC.
1. Versión de producción y FC.

Aunque la autenticación de Adobe Primetime puede reemplazar las integraciones existentes para programadores, esto generalmente no es necesario para los proveedores de televisión de pago. Adobe trabaja con el equipo técnico del proveedor para configurar la autenticación de Adobe Primetime para satisfacer las necesidades de cualquier integración existente. La integración es gratuita para los proveedores de televisión de pago, asumiendo una integración &quot;estándar&quot; y requisitos mínimos de soporte (documentación y soporte básico de correo electrónico). Si un proveedor requiere soporte significativo o un plazo escalado, se puede cobrar una tarifa de soporte o el proveedor puede querer trabajar con un tercero familiarizado con nuestra solución como Synacor.


La autenticación de Adobe Primetime también admite la gestión eficiente de la lógica empresarial del proveedor de televisión de pago, como se indica a continuación:

* En el caso de la lógica empresarial independiente que el operador puede aplicar cuando recibe una solicitud de autorización, Adobe proporciona los datos necesarios para admitir la aplicación lógica empresarial cuando recibe una solicitud de autorización. Estos datos pueden incluir, entre otros, el ID de dispositivo único para el usuario que realiza la solicitud y la dirección IP del dispositivo.
* Para la lógica empresarial que requiere la intervención del usuario o la gestión específica por parte de la solución de Adobe, el Adobe puede mantener algunas propiedades personalizadas para cada proveedor de televisión de pago. Estas configuraciones y políticas específicas del operador incluyen la habilitación de flujos de trabajo predefinidos que se pueden iniciar en puntos específicos del flujo de trabajo de nivel superior. Para obtener más información sobre la compatibilidad con propiedades personalizadas, póngase en contacto con su representante de Adobe.

El Adobe también ofrece servicios que limitan el fraude. Póngase en contacto con su representante de Adobe para obtener más información.

### El proceso de programación {#programmer-process}

Para integrar correctamente la autenticación de Adobe Primetime, los programadores deben configurar su aplicación o página web del reproductor de contenidos para trabajar con la autenticación de Adobe Primetime en la gestión de los procesos de asignación de derechos principales: autenticación, autorización y cierre de sesión.


Antes de comenzar una integración con la autenticación de Adobe Primetime, los programadores deben tener:

* Una plataforma de vídeo en línea existente, incluido un reproductor de contenidos, ya sea como parte de un sitio web o como aplicación independiente
* Un sistema de gestión de contenido
* Un mecanismo de entrega, que puede incluir o no una red de entrega de contenido (CDN) de terceros

Los programadores deben realizar algunas tareas de integración como parte de la provisión de servicios de TV en todas partes con autenticación de Adobe Primetime. Estas tareas incluyen:

* Integración de la biblioteca Access Enabler de la autenticación de Adobe Primetime en la página web o el reproductor de medios, o implementación de la integración mediante el enfoque sin cliente para &quot;dispositivos inteligentes&quot; que no son compatibles con la web
* Trabajo del lado del servidor para integrar el componente verificador de tokens de autenticación de Adobe Primetime en el flujo de trabajo de flujo de trabajo de vídeo
* La creación de una interfaz de usuario para el flujo de trabajo de acceso en su sitio web o aplicación (algunos elementos de esto, como el proceso de inicio de sesión real, los proporciona el operador de televisión de pago y algunos elementos están disponibles de forma opcional como parte de la autenticación de Adobe Primetime)

En el presente documento se ofrece una visión general del proceso del Programador y el Adobe proporciona orientación adicional al iniciar oficialmente la integración.

#### Configuración del solicitante (programador) {#requester-prog-setup}

##### Registro con Adobe {#registering}

Como primer paso, los programadores deben registrarse con Adobe o un socio autorizado por Adobe y especificar los dominios que desean utilizar con la autenticación de Adobe Primetime. A continuación, los programadores reciben un ID de solicitante único, que se proporciona a la autenticación de Adobe Primetime para cada sesión en la que el programador interactúa con Access Enabler.

##### Configuración De La Integración Inicial De Access Enabler {#access-enabler-int-setup}

Antes de cualquier cliente que solicite acceso al contenido, los programadores deben integrar el componente cliente de autenticación de Adobe Primetime (Access Enabler) en su aplicación o página web del reproductor de contenidos existente. Hay varias opciones para hacerlo:

* Puede incrustar la versión de Flash, AccessEnabler.swf, en un reproductor de vídeo basado en Flash en una página web o directamente en HTML. Puede comunicarse con el SWF en ActionScript o JavaScript. La API base es ActionScript, pero hay disponible una biblioteca de contenedores JavaScript completa.
* Para los dispositivos que no son de Flash, puede:
   * Utilice la versión de HTML5/JavaScript, AccessEnabler.js, y comunique con él a través de la API de JavaScript, o
   * Usar una biblioteca nativa de Access Enabler, como para iOS, Android o Windows 8

##### Configuración de la integración inicial de API sin cliente {#clientless-api-int-setup}

Antes de cualquier cliente que solicite acceso al contenido, los programadores deben implementar las llamadas de servicios web RESTful mediante la API sin cliente en la aplicación del reproductor de medios, así como configurar una aplicación de &quot;segunda pantalla&quot; para gestionar el inicio de sesión del usuario en su proveedor de televisión de pago a través de la web.

#### Administración de autenticación y autorización {#auth-authr-handling}

Cuando un cliente solicita un recurso protegido a un programador por primera vez, el programador presenta al cliente una lista de proveedores de televisión de pago de los que elegir. Cuando se selecciona el proveedor, se redirige al usuario a ese operador para la autenticación inicial del usuario. Una vez que la autenticación se realiza correctamente, la autenticación de Adobe Primetime se comunica con el proveedor de televisión de pago seleccionado para autorizar el acceso al recurso especificado. A continuación se proporcionan detalles sobre estos procesos.

![](assets/providr-selection-ui.png)


*Figura 3: Ejemplo de interfaz de usuario de selección de proveedor*

>[!NOTE]
>
>* La autenticación se produce como un intercambio SAML entre la autenticación de Adobe Primetime como proveedor de servicios (o &quot;SP&quot;) y un proveedor de televisión de pago como proveedor de identidad (o &quot;IdP&quot;).
>* La autorización utiliza un intercambio de servicio web de canal de retorno (servidor a servidor) entre la autenticación de Adobe Primetime (el SP) y un proveedor de televisión de pago (el IdP).



##### Comunicación del programador mediante Access Enabler

El canal de comunicación bidireccional entre Access Enabler y la página web o la aplicación del reproductor del programador sigue un patrón totalmente asíncrono. El programador envía mensajes al habilitador de acceso a través de los métodos expuestos por la API de Access Enabler. Access Enabler responde mediante llamadas de retorno registradas en la biblioteca de Access Enabler.

* Cualquier solicitud de autorización solicita primero la autenticación de forma automática si no se encuentra un token de autenticación en el sistema local. Cuando la autenticación se realiza correctamente, el token del cliente se almacena localmente para que no necesite iniciar sesión de nuevo durante un período de tiempo determinado. Si se han autenticado correctamente a través de la solución de asignación de autenticación de Adobe Primetime en cualquier otro contexto (por ejemplo, a través del sitio web del proveedor de televisión de pago o de un programador diferente), Access Enabler tiene acceso al token local y no requiere que se realice una autenticación adicional.
* Cuando un cliente solicita un recurso específico, el programador solicita la autorización al proveedor de televisión de pago a través de Access Enabler. Después de comprobar (o iniciar) la autenticación, Access Enabler se pone en contacto con el proveedor de televisión de pago (mediante la autenticación de Adobe Primetime) para determinar si el cliente tiene derecho a ver el recurso. La autenticación de Adobe Primetime gestiona la comunicación con el proveedor de televisión de pago para obtener autorización. El programador solo necesita enviar la solicitud al habilitador de acceso y gestionar la respuesta (éxito o error de autorización). Si la autorización se realiza correctamente, se almacena un token de autorización en el sistema cliente y la rellamada recibe un token multimedia de corta duración.

##### Comunicación del programador mediante la API sin cliente {#progr-comm-clientless-api}

La comunicación entre la aplicación del programador y la autenticación de Adobe Primetime se realiza a través de los servicios web RESTful.  Existen protocolos de seguridad para todas las llamadas de API a los extremos de autenticación de Adobe Primetime.  Los requisitos de seguridad se describen en la documentación de la API sin cliente.

##### Flujo de trabajo de muestra con autenticación basada en SSO del explorador web SAML {#sample-wf}

1. El visor navega a un sitio (Dummy1.com) e intenta acceder al contenido asignado.
1. La página o reproductor de vídeo carga Access Enabler de adobe.com y, cuando el usuario lo solicita, solicita la autorización del contenido solicitado.
1. Access Enabler ejecuta y valida el solicitante y la solicitud.
1. Access Enabler comprueba si hay un token de autorización válido en el almacén local. Si se encuentra una autorización válida, Access Enabler produce un token de medios de corta duración (consulte el paso 14).
1. Si no se encuentra ninguna autorización válida para el recurso solicitado pero existe un token de autenticación válido, Access Enabler inicia una solicitud de autorización con el proveedor de televisión de pago con el que el usuario está autenticado. El servidor de Adobe proporciona el intercambio de solicitud/respuesta de autorización con el proveedor de televisión de pago.
1. Si no se encuentra ningún token de autenticación válido, Access Enabler solicita al usuario que especifique su proveedor de televisión de pago. (Al seleccionar un proveedor que admita el explorador web SAML basado en SSO, se déclencheur un flujo de trabajo de autenticación basado en SAML. Para los proveedores que no son SAML, Adobe gestiona un flujo de trabajo personalizado similar).
1. Access Enabler navega por el explorador hasta el servicio SAML SP (Proveedor de servicios) de Adobe, pasando todos los parámetros apropiados.
1. SAML SP invoca el SAML IdP (proveedor de identidad) apropiado en el proveedor de televisión de pago del usuario, utilizando el perfil del explorador web SAML como se indica en los metadatos de IdP. De este modo, se navega eficazmente el usuario hasta el sitio de IdP (proveedor de televisión de pago), donde el usuario se autentica.
1. Después de la autenticación correcta, se redirige al usuario de nuevo al SAML SP de Adobe, pasando un GUID de autenticación en la respuesta SAML.
1. SAML SP de Adobe crea una sesión en el servidor donde se almacena el GUID de autenticación y redirige al usuario de nuevo a la página del programador original. (La sesión del servidor se elimina al recuperar Access Enabler del token authN).
1. Access Enabler recupera el GUID de autenticación del servidor de Adobe para incluirlo en el token con un ID de dispositivo que mantiene la autenticación de Adobe Primetime. Cuando el DRM de Flash está en el dispositivo, esto se realiza a través de las API de Flash Access (componente DRM del Flash Player) que habilitan el enlace del GUID al ID del dispositivo y devuelven un token de autenticación. De lo contrario, esto se realiza a través de las API de JS a través de HTTPS utilizando almacenamiento basado en HTML5 o a través de componentes nativos específicos.
1. Access Enabler utiliza el token de autenticación para realizar solicitudes de autorización al proveedor de televisión de pago. En los dispositivos con Flash Access habilitado, las solicitudes siempre se realizan mediante API de Flash Access para que el token de autorización resultante esté enlazado al dispositivo. En dispositivos que no son de Flash Access, HTTPS se utiliza para la comunicación segura de cliente a servidor.
1. Tras una autorización correcta, la autenticación de Adobe Primetime crea un token de autorización de larga duración (&quot;authZ&quot;) y lo pasa al activador de acceso, que lo almacena en el sistema local.
1. Access Enabler utiliza el token authZ para crear tokens de medios de corta duración que se utilizan para el acceso de visualización real. Para garantizar la seguridad, estos tokens de corta duración deben ser validados por otro componente de autenticación de Adobe Primetime, el verificador de tokens de medios.

![](assets/authn-authz-entitlmnt-flow.png)


*Figura 4: Flujo de trabajo de Access Enabler de autenticación y autorización*

##### Proporcionar una interfaz de usuario de derechos {#entitlement-ui}

Los programadores deben crear su propia interfaz de usuario para el flujo de trabajo de acceso en su sitio web o aplicación. Algunos elementos, como el proceso de inicio de sesión real, son proporcionados por el proveedor de televisión de pago y algunos elementos están disponibles de forma opcional como parte de la autenticación de Adobe Primetime. Como mínimo, el programador hace lo siguiente:

* **Implementa una interfaz de selección de proveedores** que permite a un nuevo usuario identificar a su proveedor de televisión de pago e iniciar sesión por primera vez. Para el desarrollo, Access Enabler proporciona una interfaz de usuario básica que proporciona al cliente una selección de proveedores de televisión de pago e inicia el proceso de inicio de sesión. Para un entorno de producción, los programadores deben implementar su propio cuadro de diálogo de selector de proveedor. Algunos proveedores de televisión de pago redirigen a su propio sitio para el inicio de sesión y algunos requieren que sus páginas de inicio de sesión se muestren dentro de un iframe. Los programadores deben implementar la rellamada que crea este iframe, en caso de que el cliente elija uno de esos proveedores.
* **Identifica los recursos protegidos.** Los recursos protegidos son aquellos que requieren autorización para acceder. Al ofrecer estos recursos, la interfaz del programador debe indicar la necesidad de autorización antes de la visualización. Con la autorización correcta, la interfaz debería mostrar que el recurso ya está autorizado.
* **Crea y mantiene una lista de proveedores de televisión de pago** para controlar el acceso de los usuarios únicamente a los proveedores especificados.
* **Muestra que un usuario está autenticado.** El programador debe indicar el estado de autenticación del cliente como parte de cualquier medio que se utilice para identificar los recursos protegidos. Los programadores pueden consultar Access Enabler para determinar si un cliente ya se ha autenticado.

#### Compatibilidad con el cierre de sesión único {#single-logout-support}

En la mayoría de los casos, el programador es responsable de administrar los inicios de sesión de los usuarios mediante una simple llamada de API. La llamada logout() dirige la autenticación de Primetime para cerrar la sesión del usuario actual mediante:

* Eliminación de todos los tokens de AuthN y AuthZ
* Borrar toda la información de autenticación y autorización para ese usuario
* Inicio de un flujo de trabajo específico del proveedor de televisión de pago para borrar la sesión de autenticación del usuario con el proveedor (por ejemplo, si la autenticación se realizó utilizando el protocolo de solicitud de autenticación SAML, el cierre de sesión se puede realizar utilizando el protocolo de cierre de sesión único SAML).

Si el usuario deja el equipo inactivo durante el tiempo suficiente para que sus tokens caduquen, puede volver a su sesión e iniciar sesión correctamente. La autenticación de Adobe Primetime garantiza que todos los tokens se eliminen y notifica al proveedor de televisión de pago que también elimine su sesión.


Cuando se inicia el cierre de sesión desde un sitio que no está integrado con la autenticación de Adobe Primetime, el proveedor de televisión de pago puede invocar el servicio de autenticación de Adobe Primetime Single Logout a través de un redireccionamiento del explorador.

## Más allá de los flujos de derechos básicos: funciones adicionales {#beyond-basics}

Los flujos de derechos básicos son Inicio de sesión, Autenticación, Autorización y Cierre de sesión.  A medida que la autenticación de Adobe Primetime madura y se desarrolla, se han añadido y se están añadiendo varias funciones adicionales a los flujos básicos.  Estos incluyen:

* **Metadatos de usuario** - Dependiendo de los acuerdos entre MVPD y programadores, los MVPD pueden intercambiar metadatos de forma segura como código postal, clasificación máxima, ID de canal, etc. Los metadatos permiten varios casos de uso, incluidos los controles parentales, los periodos de congelación regionales para eventos deportivos, etc.
* **Acceso libre temporal** - Permite a los programadores ofrecer acceso gratuito temporal a su contenido protegido (por ejemplo, muestras cortas de programación diaria o presentación gratuita de un gran evento).
* **MVPD de proxy** - Un MVPD puede administrar su propia integración con la autenticación de Adobe Primetime y también administrar el proceso de asignación de derechos en nombre de un grupo de &quot;ProxiedMVPDs&quot; asociados.

## Seguridad {#security}

Esta sección resalta la seguridad y la integridad de la infraestructura de autenticación de Adobe Primetime.

### Seguridad del token {#token-security}

Uno de los objetivos principales de la autenticación de Adobe Primetime es garantizar que el sistema pueda soportar ataques a los datos de asignación de contenido por parte de un usuario no autorizado o un agregador de contenido. Por lo tanto, el acceso a los datos está asegurado en diferentes niveles del flujo de trabajo, con la protección de la generación y el uso de los datos del token de autorización que tienen la mayor importancia. La arquitectura de autenticación de Adobe Primetime está diseñada para garantizar que el contenido del token se mantenga de forma segura y que el token permanezca en el dispositivo al que se emitió.

* **Seguridad de token de AuthN y AuthZ de larga duración** : todos los tokens de larga duración están firmados digitalmente por el servidor de autenticación de Adobe Primetime. Sin embargo, la firma digital difiere de una plataforma a otra, ya que utiliza un ID de dispositivo que difiere en cómo se genera, protege y valida. En todos los casos, una validación del lado del cliente garantiza que la firma digital esté intacta y que se mantenga la integridad del token. Access Enabler almacena de forma segura los tokens validados en ubicaciones específicas del entorno en el que se está ejecutando. Si la validación del ID de dispositivo falla, la sesión de autenticación se invalida, los tokens se restablecen y se solicita al usuario que vuelva a iniciar sesión.
* **Seguridad de tokens de medios de corta duración** - Los tokens de medios de corta duración, que se producen en el último paso antes del acceso al contenido, están firmados por Adobe y cifrados para evitar alteraciones durante el intercambio. Los tokens de contenido multimedia de corta duración también requieren un paso de validación adicional mediante un componente de autenticación de Adobe Primetime adicional, el verificador de tokens de contenido. El TTL del token de corta duración se establece en un valor predeterminado de 5 minutos y se puede reducir, si lo desea. El token de contenido multimedia de corta duración nunca se almacena en caché; se recupera un token nuevo del servidor cada vez que se llama a una API de autorización.

### Seguridad de dispositivos específica de la plataforma {#platform-sp-security}

Las medidas de seguridad utilizadas por la autenticación de Adobe Primetime varían según la plataforma, pero todas son sólidas y están al día.

* **Dispositivos habilitados para Flash** - Cuando Flash Player 10.1+ o AIR 2.5+ está en el dispositivo, la autenticación de Adobe Primetime utiliza la funcionalidad DRM de Flash Player para la protección, también conocida como Flash Access. El Flash proporciona un nivel adicional de protección; la fuerte seguridad del enlace del dispositivo para los tokens basados en Flash significa que, en la mayoría de los casos, el tiempo de vida puede ser mayor, el usuario no tiene que iniciar sesión con tanta frecuencia y la experiencia del usuario suele ser más fluida.
* **Experiencias en el navegador en dispositivos compatibles con HTML5**: En los dispositivos que no son de Flash y que incluyen la capacidad de explorador de HTML5, la autenticación de Adobe Primetime ofrece un medio alternativo de protección limitada para las integraciones basadas en explorador. Sin embargo, como el enlace del dispositivo para HTML5 no es tan fuerte, el tiempo de vida (TTL) de los tokens en las plataformas HTML5 suele ser más corto.
* **Compatibilidad de aplicaciones nativas para dispositivos internos y externos** : Adobe ofrece SDK nativos por sistema operativo (iOS, Android, Windows 8, etc.) que proporcionan una seguridad mejorada sobre la solución HTML5. Estos SDK utilizan API nativas para recuperar un ID de dispositivo y pasarlo de forma segura al servidor de autenticación de Adobe Primetime.
* **Clientless** : la autenticación de Adobe Primetime utiliza el protocolo HTTPS para la comunicación segura. Además, todas las llamadas desde un dispositivo inteligente deben firmarse digitalmente.

## Preguntas frecuentes {#faqs}

**¿Qué es TV en todas partes?**
El movimiento de la industria conocido como TV en todas partes permite a los clientes de televisión de pago acceder al contenido premium al que ya se suscriben en una variedad de dispositivos conectados a Internet, incluyendo computadoras personales, tabletas, smartphones, consolas de juegos, receptores de televisión y televisores &quot;inteligentes&quot;. El desafío de esta iniciativa es hacer que el proceso de autenticación sea lo más sencillo y sencillo posible, permitiendo a los clientes acceder sin problemas a su contenido de suscripción sin barreras prohibitivas y múltiples inicios de sesión.


**¿Qué es la autenticación de Adobe Primetime y cómo se relaciona con TV en todas partes?**
La autenticación de Adobe Primetime hace que TV en todas partes pase de la noción a la realidad al verificar sin problemas el derecho de un usuario a recibir contenido de una manera simple y segura. La autenticación de Adobe Primetime es un servicio alojado que permite una integración back-end rápida basada en las reglas comerciales requeridas tanto por los programadores como por los proveedores de televisión de pago. Esto significa un rápido lanzamiento al mercado para todas las partes, un entorno más seguro para prevenir el fraude y una experiencia de cliente superior, con más contenido de TV disponible para más personas en más plataformas.


**¿Cómo se ofrece/entrega la autenticación de Adobe Primetime?**
La autenticación de Adobe Primetime se ofrece mediante el modelo Software as a Service (SaaS). Esto permite una comunicación más segura entre usuarios finales, programadores y proveedores de televisión de pago para validar el derecho al contenido. Los componentes principales del servicio incluyen Access Enabler del lado del cliente (o la API sin cliente para algunos dispositivos) y el servidor de autenticación de Adobe Primetime alojado. Access Enabler es un archivo pequeño que se carga en la página web de un programador o en la aplicación del reproductor. Se comunica con los servidores de autenticación de Adobe Primetime, que a su vez tienen conexiones integradas en los sistemas de autenticación de varios proveedores de televisión de pago. La autenticación de Adobe Primetime también ofrece un enfoque de API sin cliente para la integración de algunos &quot;dispositivos inteligentes&quot; que no son compatibles con la web (televisores inteligentes, cuadros superiores, consolas de juegos, etc.). El método sin cliente proporciona servicios web RESTful con los que los desarrolladores pueden implementar los flujos de autorizaciones de autenticación de Adobe Primetime en estos dispositivos.


**¿En qué se diferencia la autenticación de Adobe Primetime de otras soluciones de TV en todas partes?**
La autenticación de Adobe Primetime ofrece diferentes ventajas con respecto a las soluciones alternativas de TV en todas partes. Las integraciones directas con proveedores individuales no proporcionan la flexibilidad de un inicio de sesión único y persistente (SSO), ya que los usuarios viajan de un sitio a otro a través de Internet. La autenticación Adobe Primetime también tiene una notable penetración en el mercado; una vez que un programador se integra con la autenticación de Adobe Primetime, se conectan inmediatamente con operadores de televisión de pago que sirven a más del 90% de los hogares en Estados Unidos. Además, la autenticación de Adobe Primetime aprovecha las funciones de seguridad únicas integradas en el tiempo de ejecución de Flash (cuando está disponible) para ayudar a mitigar el fraude, al mismo tiempo que proporciona SDK para que los programadores puedan tener la misma funcionalidad de TV en todas partes integrada en aplicaciones nativas para dispositivos móviles o domésticos donde no hay Flash disponible. Por último, aunque la autenticación de Adobe Primetime está disponible como servicio independiente, también ofrecemos la opción de tener una estrecha integración con otros productos y servicios de Adobe (incluidos Primetime y Adobe Analytics) relacionados con la entrega, protección y monetización del contenido de TV en todas partes.

**¿Qué nivel de seguridad tiene la autenticación de Adobe Primetime?**
La prioridad número uno de la arquitectura de autenticación de Adobe Primetime es garantizar que solo los visores autorizados estén autenticados y que se les conceda acceso al contenido premium. La autenticación de Adobe Primetime vincula estrechamente el acceso al dispositivo de visualización y puede ayudar a limitar las emisiones, sesiones y/o dispositivos de un hogar determinado.


**¿Se requiere Flash Player?**
Se requiere el Flash Player de Adobe 11.x o posterior para la seguridad de enlace de dispositivos más estricta. Sin embargo, la autenticación de Adobe Primetime para TV en todas partes no depende del reproductor ni de la plataforma, ya que se integra con cualquier aplicación de reproducción, incluidos Silverlight y HTML5. Además, la autenticación de Adobe Primetime proporciona compatibilidad nativa para dispositivos como iOS, Android y Xbox donde el Flash Player no está disponible.  Por último, la autenticación de Adobe Primetime proporciona un enfoque sin cliente para los dispositivos que no son capaces de procesar páginas web (consolas de juegos, televisores inteligentes, receptores de configuración).


**¿Qué dispositivos admite la autenticación de Adobe Primetime?**
La autenticación de Adobe Primetime es compatible con prácticamente cualquier dispositivo que tenga el kit web HTML5 para experiencias de visualización dentro del navegador. Además, la autenticación de Adobe Primetime continúa implementando kits de desarrollo de software (SDK) nativos para varias plataformas específicas del dispositivo, incluidas iOS, Android™ y Windows 8. La autenticación de Adobe Primetime admite parcialmente algunos dispositivos que no son compatibles con la web (televisores inteligentes, receptores de televisión, consolas de juegos, etc.) a través de sus API de servicios web RESTful.

**¿La autenticación de Adobe Primetime es compatible con los estándares emergentes para TV en todas partes?**
La autenticación de Adobe Primetime es compatible con **CableLabs OLCA (Acceso a contenido en línea)** [especificación](https://www.cablelabs.com/specifications), que proporciona requisitos técnicos y arquitectura para la entrega de vídeo a un cliente de televisión de pago desde fuentes en línea. Adobe participó en el proyecto conjunto de pruebas de interconexión de CableLabs en junio de 2011 y aprobó el proceso de prueba para la implementación de un proveedor de servicios. La autenticación de Adobe Primetime se verifica (completa y prueba) según las especificaciones OLCA para la autenticación. El componente de autorización se ha completado, pero la verificación de la prueba espera el lanzamiento del entorno de prueba de CableLabs (ETA Nov 2011).

Adobe también es miembro activo de **OATC (Open Authentication Technical Consortium)** y participa en varios de los proyectos de elaboración de especificaciones de los subcomités como parte de ese órgano.

**¿Cómo gestiona la autenticación de Adobe Primetime la administración de identidad federada/inicio de sesión único (SSO)?**
La autenticación de Adobe Primetime le permite proporcionar a los clientes autenticación y autorización de inicio de sesión único (SSO) mediante comunicación de canal de retorno (servidor a servidor) entre la autenticación de Adobe Primetime y los operadores de televisión de pago participantes. Por lo tanto, con la autenticación de Adobe Primetime, no es necesario que los suscriptores inicien sesión de nuevo después de su primera autenticación, siempre y cuando el operador de televisión de pago permita que dicha autenticación persista. Normalmente, este límite se establece en 30 días. Para lograr esto, la autenticación de Adobe Primetime proporciona un dominio común para los tokens de autenticación de nuestros clientes. Esta información de estado de autenticación está disponible para todos los sitios participantes que están integrados con un operador de televisión de pago determinado.

Actualmente, la mayoría de las integraciones de autenticación de Adobe Primetime con operadores de televisión de pago utilizan el protocolo SAML, uno de los estándares de autenticación principales. La autenticación de Adobe Primetime actúa como proveedor de servicios proxy en la arquitectura SAML y persiste en la respuesta de autenticación SAML como token seguro en el dominio común de Adobe. La autenticación de Adobe Primetime es compatible con SAML 2.0.

Aunque la autenticación de Adobe Primetime se utiliza generalmente con soluciones SAML SSO en este punto, la arquitectura de autenticación de Adobe Primetime abstrae los aspectos específicos del protocolo de la integración del programador. Por lo tanto, la compatibilidad con nuevos protocolos, como uno basado en OAuth 2.0 o protocolos personalizados, se puede agregar con el tiempo.

**¿Cuánto cuesta la autenticación de Adobe Primetime para TV en todas partes para los usuarios finales?**
No hay coste adicional para los usuarios finales por el uso de la autenticación de Adobe Primetime.

>[!NOTE]
>
>**Pasos siguientes:** Para obtener más información, póngase en contacto con el representante del Adobe o rellene el formulario de solicitud de información [here](https://www.adobe.com/cfusion/mmform/index.cfm?name=adobepass_rfi).
