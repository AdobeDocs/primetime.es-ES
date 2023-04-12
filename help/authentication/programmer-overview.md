---
title: Información general para programadores
description: Información general para programadores
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '4272'
ht-degree: 0%

---


# Información General Para Programadores {#programmers-overview}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Introducción {#introduction}

Esta información general está dirigida al proveedor de contenido (programador) que planea integrar Adobe® Pass en su sitio web o aplicación. Para obtener documentación adicional, incluidas las guías de inicio e integración, consulte Información relacionada a continuación.

Hoy sus espectadores pueden acceder a Internet en cualquier momento y lugar, y solicitar acceso a contenido protegido directamente de usted, el Programador. Es posible que quieran ver un evento único, o que estén buscando derechos de visualización para toda una serie de televisión que estén emitiendo.

Pero antes de permitir el acceso a su contenido protegido, debe determinar si un cliente tiene derecho a ver dicho contenido. ¿Tienen una suscripción con un distribuidor de programación de vídeo multicanal (MVPD)? En caso afirmativo, ¿incluye la suscripción su programación?

La determinación de la asignación de derechos de un visor no siempre es sencilla para un programador. Los MVPD tienen los datos de identificación y privilegios de acceso para sus clientes.  Añada el hecho de que los espectadores que intentan acceder a su contenido protegido se suscriben a una variedad de MVPD, cada uno de los cuales tiene sistemas diferentes, y es fácil ver que determinar el derecho del espectador a contenido protegido puede volverse complicado y técnicamente complicado:

![](assets/user-ent-by-progr.png)

*Figura: Derechos De Usuario Determinados Directamente Por El Programador*

La autenticación de Adobe Primetime para TV en todas partes media de forma segura estas transacciones de derechos entre programadores y MVPD. La autenticación de Adobe Primetime facilita, agiliza y garantiza que los programadores proporcionen contenido protegido a clientes válidos:

![](assets/user-ent-mediatedby-authn.png)

*Figura: Derechos de usuario mediados por la autenticación de Adobe Primetime*

La autenticación de Adobe Primetime actúa como su proxy en los intercambios con los MVPD participantes, de modo que pueda presentar a sus visualizadores una interfaz coherente entre sitios. La autenticación de Adobe Primetime también le permite proporcionar a sus visualizadores autenticación y autorización de inicio de sesión único (SSO). Se realiza un seguimiento de la autenticación y autorización de todos los servicios participantes, de modo que el suscriptor no necesita iniciar sesión de nuevo después de su primera autenticación en su propio sistema.

* **Autenticación** - El proceso de confirmar con un MVPD que un usuario dado es un cliente conocido.
* **Autorización** - El proceso de confirmar con un MVPD que un usuario autenticado tiene una suscripción válida a un recurso especificado.

### Cómo funciona la autenticación de Adobe Primetime {#HowItWorks}

La aplicación de visualización de contenido del programador interactúa con la autenticación de Adobe Primetime mediante el componente cliente Access Enabler o los servicios web RESTful de la API sin cliente (para dispositivos que no son compatibles con la web, como televisores inteligentes, consolas de juegos, receptores de Internet, etc.). Access Enabler se ejecuta en el sistema del usuario, donde facilita todos los flujos de trabajo de asignación de derechos.  El componente Access Enabler se descarga desde su sitio de alojamiento en Adobe cuando los clientes acceden al sitio y solicitan contenido protegido.  Los servidores de autenticación de Adobe Primetime alojan los servicios web RESTful utilizados en la solución sin cliente.

La autenticación de Adobe Primetime gestiona los flujos de trabajo de asignación de derechos reales al proporcionar los primitivos que utiliza para:

* Establezca su identidad. (El programador es el &quot;solicitante&quot; en el flujo de derechos de autenticación de Adobe Primetime).
* Autenticar a un usuario con un MVPD concreto.  (El MVPD es el &quot;proveedor de identidad&quot; o el &quot;IdP&quot; en el flujo de autorizaciones de autenticación de Adobe Primetime).
* Autorice a un usuario con el MVPD para un recurso en particular.
* Cierre la sesión del usuario.

El programador es responsable de su página web de nivel superior o aplicación de reproductor que haga lo siguiente:

* Implementa la interfaz de usuario
* Interactúa con los servicios web de API Access Enabler o Clientless

El objetivo de la autenticación de Adobe Primetime es crear una forma sencilla y modular para que los programadores y los MVPD puedan gestionar la verificación de derechos.

## Explicación de los tokens {#understanding-tokens}

La solución de autorizaciones de autenticación de Adobe Primetime se centra en la generación de fragmentos de datos específicos que se crean al completar correctamente los flujos de trabajo de autenticación y autorización. Estos datos se denominan tokens. Los tokens tienen una vida útil limitada; cuando caducan, es necesario volver a emitir los tokens mediante el reinicio de los flujos de trabajo de autenticación y autorización.

Para obtener más información sobre los tokens, consulte las secciones siguientes:

* [Tipos de tokens](#token-types)
* [Almacenamiento de tokens](#token-storage)
* [Seguridad del token](#token-security)
* [Uso compartido de tokens](#token-sharing)

### Tipos de tokens {#token-types}

Se emiten tres tipos de tokens durante los flujos de trabajo de autenticación y autorización. Los tokens AuthN y AuthZ tienen una duración prolongada, lo que proporciona continuidad en la experiencia de visualización del usuario. El token de medios es un token de corta duración que proporciona compatibilidad con las prácticas recomendadas del sector para evitar el fraude mediante la extracción de flujo. Los programadores especifican los valores de tiempo de vida (TTL) para cada tipo de token en función de los acuerdos realizados con los MVPD. Los programadores deciden sobre un valor TTL que mejor sirva a su negocio y a sus clientes.

* **Token AuthN** (&quot;De larga duración&quot;): Tras la autenticación correcta, la autenticación de Adobe Primetime crea un token AuthN asociado tanto al dispositivo solicitante como a un identificador único global (GUID).
   * La autenticación de Adobe Primetime envía el token AuthN al activador de acceso, que lo almacena en caché de forma segura en el sistema del cliente.  Mientras el token AuthN está allí y no ha caducado, está disponible para todas las aplicaciones que utilizan la autenticación de Adobe Primetime. Access Enabler utiliza el token AuthN para el flujo de autorización.
   * En un momento dado, solo se almacena en caché un token AuthN. Siempre que se emite un nuevo token AuthN y ya existe uno antiguo, la autenticación de Adobe Primetime sobrescribe el token almacenado en caché.
* **Token de AuthZ** (&quot;De larga duración&quot;): Tras la autorización correcta, la autenticación de Adobe Primetime crea un token AuthZ asociado al dispositivo solicitante y a un recurso protegido específico.  El recurso protegido se identifica mediante un ID de recurso único.
   * La autenticación de Adobe Primetime envía el token AuthZ al activador de acceso, que lo almacena en caché de forma segura en el sistema local. A continuación, Access Enabler utiliza el token AuthZ para crear el testigo de contenido multimedia de corta duración que se utiliza para el acceso de visualización real.
   * En un momento dado, solo se almacena en caché un token AuthZ por recurso. La autenticación de Adobe Primetime puede almacenar en caché varios tokens de AuthZ, siempre que estén asociados a distintos recursos. Siempre que se emite un nuevo token AuthZ y ya existe uno antiguo para el mismo recurso, la autenticación de Adobe Primetime sobrescribe el token almacenado en caché.
* **Token de medio** (&quot;De corta duración&quot;): Access Enabler utiliza el token AuthZ para generar una duración corta (valor predeterminado: 7 minutos) Token de medios. Este es el punto en el que se considera que se ha producido una solicitud de reproducción correcta.
   * Antes de proporcionar acceso al recurso protegido, el servidor de medios debe utilizar un componente de autenticación de Adobe Primetime, el verificador de tokens de medios, para validar el token de medios.
   * Dado que el token de medios no está enlazado al dispositivo, su duración es considerablemente menor (de forma predeterminada: 7 minutos) que el de los tokens de larga duración AuthN y AuthZ.
   * El token de contenido multimedia de corta duración está restringido a un uso único y nunca se almacena en caché. Se recupera del servidor de autenticación de Adobe Primetime cada vez que se llama a una API de autorización.

### Almacenamiento de tokens {#token-storage}

Access Enabler almacena tokens de larga duración (AuthN y AuthZ) en ubicaciones específicas de su entorno:

* **Flash 10.1** (o superior): Los tokens de larga duración se almacenan como objetos compartidos locales.
* **HTML5**: Los tokens de larga duración se mantienen de forma segura en la tienda local del explorador HTML5.
* **iOS**: Los tokens de larga duración se almacenan en una mesa de trabajo persistente, desde donde otras aplicaciones cliente de autenticación de Adobe Primetime pueden acceder a ellos.
* **Android**: Los tokens de larga duración se almacenan en un archivo de base de datos compartido, desde donde otras aplicaciones cliente de autenticación de Adobe Primetime pueden acceder a ellos.
* **Dispositivos API sin cliente**: Los tokens se almacenan en los servidores de autenticación de Primetime.

### Seguridad del token {#token-security}

El servidor de autenticación de Adobe Primetime firma digitalmente todos los tokens de larga duración mediante el ID del dispositivo (derivado de las características de hardware del dispositivo). La firma digital difiere en la forma en que se genera, protege y valida según el entorno:

* **Flash 10.1** (o superior): El ID del dispositivo se basa en la credencial del dispositivo, un certificado único emitido desde el servidor de Individualización de Adobe. Esta seguridad es equivalente a la tecnología FAXS DRM. Esta validación del lado del servidor compara el ID de dispositivo único del token con la credencial del dispositivo (comunicado de forma segura del Flash Player a la autenticación de Adobe Primetime). La credencial del dispositivo también identifica la versión del cliente FAXS y la versión de Flash Player (o AIR) a la que se emitió. El enlace del dispositivo es más fuerte que con HTML5, por lo que el tiempo de vida (TTL) de los tokens suele ser mayor con el Flash.
* **HTML5** - El dispositivo está individualizado en el lado del cliente. Utiliza características disponibles mediante JavaScript para producir un ID de seudodispositivo que incluya versiones de navegador y sistema operativo, una dirección IP y un GUID de cookie de navegador (identificador único global). Este ID de dispositivo de token se compara con el ID del seudodispositivo actual del dispositivo. Como la dirección IP puede cambiar durante el uso normal, incluso en la misma sesión, la autenticación de Adobe Primetime almacena tokens de HTML5 en dos ubicaciones: localStorage y sessionStorage. Si la IP cambia y el token sessionStorage sigue siendo válido, la sesión se mantiene. Con HTML5, el enlace del dispositivo no es tan fuerte, por lo que el TTL para los tokens suele ser más corto que para el Flash.
* **Clientes nativos** (iOS y Android): los tokens de larga duración contienen información de personalización del ID de dispositivo nativo y, por lo tanto, están enlazados al dispositivo solicitante. Las solicitudes de autenticación y autorización se envían a través de HTTPS y la información de ID del dispositivo se firma digitalmente mediante la biblioteca de Access Enabler antes de enviarla a los servidores back-end. En el servidor, la información del ID del dispositivo se valida con su firma digital asociada.
* **Clientes de API sin cliente** : La solución API sin cliente tiene su conjunto de protocolos de seguridad que implican la firma digital de todas las llamadas API. Los tokens generados durante los flujos de derechos se almacenan de forma segura en los servidores de autenticación de Adobe Primetime.

La autenticación de Adobe Primetime valida cada token de larga duración para garantizar que el dispositivo que accede al contenido sea el mismo que el que emitió el token. Para todos los tokens, una validación del lado del cliente garantiza que la firma digital esté intacta y que se mantenga la integridad del token. Cuando falla la validación del ID de dispositivo, la sesión de autenticación se invalida y se solicita al usuario que vuelva a iniciar sesión, lo que restablece los tokens.

### Uso compartido de tokens {#token-sharing}

Las aplicaciones de distintas plataformas no comparten tokens. Esto se debe a varios motivos, entre ellos:

* Tal como se describe en [Almacenamiento de tokens](#token-storage), el método de almacenamiento de tokens varía según la plataforma (por ejemplo, Objetos compartidos locales para Flash, WebStorage para JavaScript).
* El grado de seguridad de los tokens difiere entre plataformas. Por ejemplo, los tokens de Flash están fuertemente enlazados a un dispositivo mediante FAXS. Los tokens en un entorno JavaScript puro no tienen el mismo nivel de compatibilidad con DRM que en el Flash.  El uso compartido de tokens JS con aplicaciones de Flash aumentaría la posibilidad de que los tokens menos seguros explotaran un entorno más seguro.

## Ciclo de vida de integración de programadores {#prog-integ-lifecycle}

![](assets/progr-flow-int-lifecycle.png)

*Figura: Integración de la autenticación con el sitio web y la aplicación del programador*


## Flujos lógicos {#logical-flows}

### Diagrama de flujo de derechos {#chart}

El siguiente diagrama de flujo presenta el proceso general de confirmación de la asignación de derechos (mediante el componente cliente Access Enabler de autenticación de Adobe Primetime):

![](assets/ent-flowchart.png)

*Figura: Proceso de confirmación de la asignación de derechos*

### Pasos de autenticación {#authn-steps}

Los siguientes pasos presentan un ejemplo del flujo de autenticación de Adobe Primetime.  Esta es la parte del proceso de asignación de derechos en la que un programador determina si el usuario es un cliente válido de un MVPD.  En esta situación, el usuario es un suscriptor válido de un MVPD.  El usuario está intentando ver contenido protegido mediante una aplicación de Flash del programador:

1. El usuario navega a la página web del programador, que carga la aplicación de Flash del programador y los componentes de Access Enabler de autenticación de Adobe Primetime en el equipo del usuario. La aplicación de Flash utiliza Access Enabler para establecer la identificación del programador con la autenticación de Adobe Primetime, y la autenticación de Adobe Primetime asigna al activador de acceso con la configuración y los datos de estado para ese programador (el &quot;solicitante&quot;). Access Enabler debe recibir estos datos del servidor antes de realizar cualquier otra llamada API. Nota técnica: el programador establece su identidad con el activador de acceso `setRequestor()` método; para obtener más información, consulte la [Guía de integración del programador](/help/authentication/programmer-integration-guide-overview.md).
1. Cuando el usuario intenta ver el contenido protegido del programador, la aplicación del programador presenta al usuario una lista de MVPD, desde los cuales el usuario selecciona un proveedor.
1. Se redirige al usuario a un servidor de autenticación de Adobe Primetime, donde se cifra un [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) se crea la solicitud para el MVPD seleccionado por el usuario. Esta solicitud se envía como una solicitud de autenticación en nombre del programador al MVPD. Según el sistema de MVPD, el navegador del usuario se redirige al sitio de MVPD para iniciar sesión, o se crea un iFrame de inicio de sesión en la aplicación del programador.
1. En cualquier caso (redirección o iFrame), el MVPD acepta la solicitud y muestra su página de inicio de sesión.
1. El usuario inicia sesión con el MVPD, el MVPD valida el estado del usuario como cliente que paga y, a continuación, el MVPD crea su propia sesión HTTP.
1. Cuando se valida el usuario, el MVPD crea una respuesta (SAML y cifrada), que el MVPD devuelve a la autenticación de Adobe Primetime.
1. La autenticación de Adobe Primetime recibe la respuesta MVPD, ve que hay una sesión HTTP de autenticación de Adobe Primetime abierta, valida la respuesta SAML de MVPD y redirige de nuevo al sitio del programador.
1. El sitio del programador se vuelve a cargar, el activador de acceso se vuelve a cargar y el programador llama a setRequestor() de nuevo.  La segunda llamada a setRequestor() es necesaria porque la configuración actual ha cambiado: ahora hay un indicador presente que informa al Access Enabler de que hay un token AuthN esperando a generarse en el servidor.
1. Access Enabler observa que hay una autenticación pendiente y solicita el token al servidor de autenticación de Adobe Primetime. El token se recupera del servidor invocando las funciones DRM del Flash Player.
1. El token AuthN se almacena en la caché LSO de Flash Player del programador; la autenticación ya ha finalizado y la sesión se ha destruido en el servidor de autenticación de Adobe Primetime.

### Pasos de autorización {#authz-steps}

Los siguientes pasos continúan en desde el [Pasos de autenticación](#authn-steps):

1. Cuando el usuario intenta acceder al contenido protegido del programador, la aplicación del programador comprueba primero si hay un token AuthN en el equipo o dispositivo local del usuario.  Si ese token no está ahí, entonces la variable [Pasos de autenticación](#authn-steps) se siguen los anteriores.  Si el token AuthN está allí, el flujo de autorización continúa con la aplicación del programador iniciando una llamada al habilitador de acceso con una solicitud para obtener los derechos de visualización del usuario para un elemento específico de contenido protegido.
1. El elemento específico de contenido protegido se representa mediante un &quot;identificador de recurso&quot;.  Podría ser una cadena simple o una estructura más compleja, pero en cualquier caso la naturaleza del identificador del recurso se acuerda con antelación entre el Programador y el MVPD.  La aplicación del programador pasa el identificador de recurso al activador de acceso.  Access Enabler comprueba si hay un token AuthZ en el equipo o dispositivo local del usuario.  Si el token AuthZ no está allí, Access Enabler pasa la solicitud al servidor de autenticación de Adobe Primetime back-end.
1. El servidor de autenticación de Adobe Primetime se comunica con el extremo de autorización de los MVPD mediante protocolos estandarizados.  Si la respuesta de MVPD indica que el usuario está autorizado a ver el contenido protegido, el servidor de autenticación de Adobe Primetime crea un token AuthZ y lo devuelve al activador de acceso, que almacena el token AuthZ en el equipo del usuario.
1. Con un token AuthZ almacenado en el equipo o dispositivo del usuario, la aplicación del programador llama a Access Enabler para obtener un token multimedia del servidor de autenticación de Adobe Primetime y proporciona ese token a la aplicación del programador.
1. Por último, la aplicación del programador utiliza el componente Verificador de tokens de medios para confirmar que el usuario correcto está viendo el contenido correcto y, con el token de medios en su lugar, el usuario puede ver el contenido protegido.


## Registro e inicialización {#reg-and-init}

El primer paso para trabajar con la autenticación de Adobe Primetime es registrarse con Adobe o con un socio autorizado para la autenticación de Adobe Primetime.

Al registrarse, proporciona una lista de los dominios desde los que se comunicará con la autenticación de Adobe Primetime. Por ejemplo, los dominios de Turner Broadcasting System incluyen tbs.com y tnt.tv como dominios registrados para la autenticación de Adobe Primetime. A cada uno de estos sitios de contenido se les otorga acceso a la autenticación de Adobe Primetime y se le asigna su propio ID de solicitante (por ejemplo, &quot;TBS&quot; y &quot;TNT&quot;). Si decide agregar sitios adicionales, debe informar al Adobe de los nombres de dominio adicionales para que se los coloque en la lista de dominios permitidos y se le asignen ID de solicitante adicionales.

>[!WARNING]
>
>Mientras está probando la integración, asegúrese de que el servidor de prueba esté en un dominio registrado que desee utilizar en la producción. Se omiten las solicitudes, incluso las solicitudes de prueba, procedentes de dominios no incluidos en la lista blanca. Por ejemplo, si ha solicitado que domain.com se utilice en la producción, asegúrese de que está implementando la integración de prueba en domain.com, test.domain.com y staging.domain.com.
>
>Las solicitudes que contienen nombre de usuario y / o contraseña en la dirección URL se ignoran incluso si los dominios están en la lista blanca. Ejemplo: `//username@registered-domain/`

El ID del solicitante identifica de forma exclusiva al cliente del programador en todas las comunicaciones con el componente cliente Access Enabler de la autenticación de Adobe Primetime. Todos los datos estáticos de autenticación de Adobe Primetime asociados con el programador tienen una clave para este ID.

>[!TIP]
>
>Además del ID del solicitante, al registrarse también recibe direcciones URL funcionales para el componente cliente Access Enabler y el verificador de tokens de medios.

## Pasos de la integración {#integration-steps}

>[!TIP]
>
>Si utiliza el Open Source Media Framework de Adobe (&quot;OSMF&quot;) para el desarrollo de su reproductor de medios, la forma más rápida de utilizar la autenticación de Adobe Primetime es integrar el complemento OSMF *(obsoleto)* en el código del reproductor.
>
><!--For details, see [Adobe Primetime authentication Plugin For OSMF](https://tve.helpdocsonline.com/9-2-2) in the Programmer Integration Guide.-->

1. [Configuración del solicitante](#requestor)
1. [Administración de autenticación y autorización](#authn-authz)
1. [Compatibilidad con el cierre de sesión único](#ssl)

### 1. Configuración del solicitante {#requestor}

#### 1 bis. Registro con Adobe

El primer paso es registrarse con Adobe o con un socio autorizado para la autenticación de Adobe Primetime.  Al registrarse, se emiten uno o más identificadores únicos globales (GUID). Cada GUID que se emite está asociado a un dominio desde el cual se permite el acceso a la autenticación de Adobe Primetime. Pasa un GUID (llamado ID del solicitante) para el dominio solicitante a fin de registrar su identidad para cada sesión en la que interactúe con Access Enabler. Para obtener más información, consulte [Registro e inicialización](#reg-and-init) en la Guía de integración del programador.

#### 1 ter. Integración inicial de Access Enabler

El siguiente paso es integrar Access Enabler en la aplicación o página web del reproductor de contenidos existente:

* Puede incrustar la versión de Flash, `AccessEnabler.swf`, en un reproductor de vídeo basado en Flash o puede incrustarlo directamente en el HTML de la página web. Puede comunicarse con el SWF de Access Enabler en ActionScript o JavaScript. La API base es de ActionScript, pero si prefiere trabajar con JavaScript, hay una biblioteca de contenedores completa disponible para su inclusión en las páginas.
* Para los entornos que no son de Flash, puede:
   * Utilice la versión de HTML5/JavaScript, AccessEnabler.js, y comuníquese con ella a través de la API de JavaScript
   * Utilice la autenticación de la extensión nativa de AIR para Adobe Primetime para combinar código nativo con clases de ActionScript integradas
   * Utilice una de las versiones de cliente nativas de la biblioteca de Access Enabler (iOS o Android)

### 2. Gestión de la autenticación y la autorización {#authn-authz}

#### 2 bis. Comunicación con Access Enabler

La comunicación entre Access Enabler y su página web o aplicación de reproductor es asíncrona. La aplicación llama a los métodos Access Enabler y Access Enabler responde mediante llamadas de retorno que se registran en la biblioteca de Access Enabler.

* Cuando la aplicación realiza una solicitud de autorización, Access Enabler inicia automáticamente una solicitud de autenticación si no hay un token AuthN válido en el sistema local. Cuando la autenticación se realiza correctamente, el token AuthN del usuario se almacena localmente para que no necesite iniciar sesión de nuevo. Si se han autenticado correctamente mediante la autenticación de Adobe Primetime en cualquier otro contexto (por ejemplo, a través del sitio web de MVPD o con un programador diferente), Access Enabler tiene acceso al token AuthN local y no se necesita una autenticación adicional.
* Cuando un usuario intenta acceder al contenido protegido, envía una solicitud de autorización al activador de acceso. Después de comprobar (o iniciar) la autenticación, Access Enabler se pone en contacto con el MVPD (a través del servidor de autenticación de Adobe Primetime) para determinar si el cliente tiene derecho a ver el contenido protegido. La aplicación solo necesita enviar la solicitud al activador de acceso y, a continuación, gestionar la respuesta (éxito o error de autorización). Si la autorización se realiza correctamente, se almacena un token AuthZ en el sistema cliente.  Por último, la aplicación recibe un token multimedia de corta duración para utilizarlo en su propio procedimiento de autorización.

>[!NOTE]
>
>* La autenticación se produce como un intercambio SAML, entre la autenticación de Adobe Primetime como proveedor de servicios (SP) y el MVPD como proveedor de identidad (IdP).
>
>* La autorización utiliza un intercambio de servicio web de canal de retorno (servidor a servidor) entre la autenticación de Adobe Primetime (el SP) y un MVPD (el IdP).



#### 2 ter. Proporcionar Una Interfaz De Usuario Con Derecho {#entitlement-ui}

Usted proporciona su propia interfaz de usuario para el acceso del usuario a su contenido. Algunos elementos, como el proceso de inicio de sesión real, son proporcionados por el MVPD y algunos elementos están disponibles de forma opcional como parte de la autenticación de Adobe Primetime. Como mínimo, debe hacer lo siguiente:

* **Implemente una interfaz de selección de MVPD que permita a un nuevo usuario identificar su MVPD e iniciar sesión por primera vez**. Para el desarrollo, Access Enabler proporciona una interfaz de usuario básica que proporciona al cliente una selección de MVPD e inicia el proceso de inicio de sesión. Para la producción, debe implementar su propio cuadro de diálogo Selector de MVPD. Algunos MVPD redirigen a su propio sitio para iniciar sesión, y algunos requieren que sus páginas de inicio de sesión se muestren dentro de un iFrame. Debe implementar una llamada de retorno que cree este iFrame para controlar los casos en los que el MVPD del usuario muestra su página de inicio de sesión en un iFrame.
* **Identificar contenido protegido**. El contenido protegido requiere autorización para acceder. La interfaz debe indicar qué contenido está protegido y qué contenido se ha autorizado.  El estado de autorización se indica a menudo con los iconos &quot;desbloqueado&quot; y &quot;bloqueado&quot;.
* **Mostrar que un usuario está autenticado**. Debe indicar el estado de autenticación de un usuario como parte de los medios que utilice para identificar el contenido protegido. Puede consultar Access Enabler para determinar si el cliente ya se ha autenticado.

#### 2 quáter. Integración del verificador de tokens de medios {#int-media-token-ver}

Debe integrar el componente Verificador de tokens de medios de autenticación de Adobe Primetime en su servidor de medios.  Esto es para que el verificador de tokens existente pueda reconocer los tokens de medios de corta duración proporcionados a partir de la autenticación de Adobe Primetime con una autorización correcta. El verificador de tokens de medios valida los tokens de medios como el último paso de seguridad antes de proporcionar al usuario acceso a contenido protegido. Recibe la ubicación desde la cual descargar el verificador de tokens de medios al registrarse con Adobe.

### 3. Compatibilidad con el cierre de sesión único {#ssl}

En la mayoría de los casos, el reproductor multimedia es responsable de administrar los inicios de sesión de los usuarios mediante una sencilla API de Access Enabler. Cuando llama a logout(), Access Enabler hace lo siguiente:

* Cierre la sesión del usuario actual
* Borra toda la información de autenticación y autorización para el usuario que ha cerrado la sesión
* Elimina todos los tokens de AuthN y AuthZ del sistema local del usuario

Si el usuario deja el equipo inactivo el tiempo suficiente para que sus tokens caduquen, puede volver a la sesión e iniciar sesión correctamente. La autenticación de Adobe Primetime garantiza que se eliminen todos los tokens y notifica al MVPD que también debe eliminar su sesión.

Cuando se inicia el cierre de sesión desde un sitio que no está integrado con la autenticación de Adobe Primetime, el MVPD puede invocar el servicio de autenticación de Adobe Primetime Single Logout a través de un redireccionamiento del explorador.

## Explicación de los ID de usuario {#user-ids}

Conceptualmente, cada usuario que inicia un flujo de derechos está asociado a un único ID de usuario.  Sin embargo, durante el flujo de autorizaciones, ese ID de usuario se puede presentar de diferentes maneras, según la API desde la que obtenga el ID.

El sessionGUID en el token de medios cortos es la forma segura del UserID, que está disponible a través de la llamada sendTrackingData() .   En todas las integraciones actuales, se trata de un GUID persistente para el usuario en todo el tiempo y los dispositivos, pero la fuente del GUID comienza con el UserID en la respuesta SAML de MVPD.   Sin embargo, algunos MVPD podrían cambiar de opinión en el futuro y empezar a enviar un GUID transitorio.  Si un programador desea asegurarse de que el UserID de origen de MVPD en la respuesta AuthN sea persistente, debe hacerlo en sus acuerdos con MVPD.

Estas son las diferentes formas en que el ID de usuario se representa en las API de autenticación de Adobe Primetime:

* `sendTrackingData()` Propiedad GUID : es la versión con hash de Adobe del UserID de MVPD.  Tiene un hash para que este ID de usuario no pueda volver a rastrearse en el origen desde el MVPD.   Este ID es único y suele ser persistente, pero no se puede compartir con el MVPD para comparar el comportamiento de uso específico con lo que los MVPD tienen de su lado.   No se firma digitalmente, por lo que no se puede falsificar para la prevención del fraude, pero es lo suficientemente bueno para los análisis.  Esta forma de ID de usuario se proporciona del lado del cliente en todos los eventos que genera la autenticación de Adobe Primetime en el flujo AuthN/AuthZ.
* Token de medio corto `sessionGUID` propiedad : es igual que el UserID mediante `sendTrackingData()`Sin embargo, este se firma digitalmente para proteger su integridad.  Esto hace que este valor sea lo suficientemente bueno para el seguimiento del fraude en el uso simultáneo. Está diseñado para procesarse en el servidor después de usar la biblioteca de validador, y se puede analizar si hay patrones de fraude antes de lanzar el flujo de vídeo al cliente.  Realizar cualquiera de estas tareas depende del Programador.
* `getMetadata() userID `propiedad : Esta propiedad permitirá que Adobe exponga el UserID de MVPD de origen real al programador. Se cifrará con la clave pública del certificado que tenemos del programador, para que no se exponga claramente al cliente. Esto le da al programador el UserID real de MVPD, por lo que es algo que puede utilizarse para vincular cuentas o investigar fraudes directamente con el MVPD.

**En conclusión**

* El ID de usuario de MVPD es un ID único persistente, aunque no garantizado, que es **se generan a partir de los MVPD y se pasan a Adobe en caso de autenticación correcta**. Por lo general, es coherente en todas las redes con algunas excepciones.
* El ID de usuario de MVPD no contiene PII y NO es un número de cuenta. No es necesario que se exponga de forma cifrada, ya que hemos validado con todos los MVPD que no se está enviando ningún PII.


El uso del ID de usuario depende del caso de uso:

* Si lo necesita para el seguimiento/análisis, el lugar más práctico es obtenerlo de `sendTrackingData()`.
* Si lo necesita en el lado del servidor para la publicación de flujos, el fraude o los datos operativos, puede obtenerlo del Validador de tokens de medios.
* Si lo necesita para la vinculación de cuentas y un fraude más profundo, consulte a su contacto de Adobe para obtener disponibilidad.

<!--
>[!RELATEDINFORMATION]
>
>* **Kickstart Guides** These guides explain the initial steps to take once you have decided to begin integrating with Adobe Primetime authentication.
>* **Programmer Integration Guide** This is a lower level technical guide for Programmers, directed primarily to the software engineers who code and test the applications and systems involved in the integration.
>* [Overview For MVPDs](/help/authentication/mvpd-overview.md) This provides a similar level of conceptual information as in this Programmer overview, but is directed toward MVPDs.
-->