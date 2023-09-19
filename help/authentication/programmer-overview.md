---
title: Información general para programadores
description: Información general para programadores
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '4272'
ht-degree: 0%

---

# Información General Para Programadores {#programmers-overview}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.

## Introducción {#introduction}

Esta descripción general está dirigida al proveedor de contenido (programador) que planea integrar Adobe ® Pass en su sitio web o aplicación. Para obtener documentación adicional, incluidas las guías de KickStart e Integración, consulte Información relacionada a continuación.

Hoy en día, sus espectadores pueden acceder a Internet en cualquier momento y en cualquier lugar, y solicitar acceso a contenido protegido directamente de usted, el programador. Es posible que deseen ver un evento único o que busquen derechos de visualización para toda una serie de televisión que esté transmitiendo.

Pero antes de permitir el acceso a su contenido protegido, debe determinar si un cliente tiene derecho a ver ese contenido. ¿Tienen una suscripción con un Multichannel Video Programming Distributor (MVPD)? Si es así, ¿incluye esa suscripción su programación?

La determinación de los derechos de un visualizador no siempre es sencilla para un programador. Las MVPD tienen los datos de identificación y privilegios de acceso para sus clientes.  Añada el hecho de que los visualizadores que intentan acceder a su contenido protegido se suscriben a una variedad de MVPD, cada una de las cuales tiene diferentes sistemas, y es fácil ver que determinar el derecho del visualizador a contenido protegido puede complicarse rápidamente y ser técnicamente difícil:

![](assets/user-ent-by-progr.png)

*Imagen: Derecho De Usuario Determinado Directamente Por El Programador*

La autenticación de Adobe Primetime para TV en todas partes media de forma segura estas transacciones de derechos entre programadores y MVPD. La autenticación de Adobe Primetime facilita, agiliza y asegura que los programadores proporcionen contenido protegido a clientes válidos:

![](assets/user-ent-mediatedby-authn.png)

*Imagen: derecho de usuario mediado por la autenticación de Adobe Primetime*

La autenticación de Adobe Primetime actúa como su proxy en los intercambios con MVPD participantes, de modo que puede presentar a sus visualizadores una interfaz coherente entre sitios. La autenticación de Adobe Primetime también le permite proporcionar a sus visualizadores autenticación y autorización de inicio de sesión único (SSO). Se realiza un seguimiento de la autenticación y la autorización de todos los servicios participantes, de modo que un suscriptor no necesita volver a iniciar sesión después de su primera autenticación en su propio sistema.

* **Autenticación** - Proceso de confirmar con un MVPD que un usuario determinado es un cliente conocido.
* **Autorización** - Proceso de confirmar con un MVPD que un usuario autenticado tiene una suscripción válida a un recurso especificado.

### Funcionamiento de la autenticación de Adobe Primetime {#HowItWorks}

La aplicación de visualización de contenido del programador interactúa con la autenticación de Adobe Primetime mediante el componente de cliente Access Enabler o los servicios web RESTful de la API sin cliente (para dispositivos no web, como televisores inteligentes, consolas de juegos, decodificadores, etc.). Access Enabler se ejecuta en el sistema del usuario, donde facilita todos los flujos de trabajo de asignación de derechos.  El componente Habilitador de acceso se descarga desde su sitio de alojamiento durante el Adobe cuando los clientes acceden al sitio y solicitan contenido protegido.  Los servidores de autenticación de Adobe Primetime alojan los servicios web RESTful utilizados en la solución sin cliente.

La autenticación de Adobe Primetime gestiona los flujos de trabajo de derechos reales al tiempo que proporciona primitivas que utiliza para lo siguiente:

* Establece tu identidad. (El programador es el &quot;solicitante&quot; en el flujo de derechos de autenticación de Adobe Primetime).
* Autenticar a un usuario con una MVPD en particular.  (MVPD es el &quot;proveedor de identidad&quot; o &quot;IdP&quot; en el flujo de derechos de autenticación de Adobe Primetime).
* Autorizar a un usuario con el MVPD para un recurso en particular.
* Cierre la sesión del usuario.

El programador es responsable de la página web de nivel superior o de la aplicación de reproducción que haga lo siguiente:

* Implementa la interfaz de usuario
* Interactúa con los servicios web Access Enabler o API sin cliente

El objetivo de la autenticación de Adobe Primetime es crear una forma sencilla y modular para que los programadores y las MVPD gestionen la verificación de derechos.

## Explicación de tokens {#understanding-tokens}

La solución de asignación de derechos de autenticación de Adobe Primetime se centra en la generación de fragmentos de datos específicos que se crean al finalizar correctamente los flujos de trabajo de autenticación y autorización. Estos fragmentos de datos se denominan tokens. Los tokens tienen una duración limitada; cuando caducan, deben volver a emitirse reiniciando los flujos de trabajo de autenticación y autorización.

Para obtener más información sobre los tokens, consulte las siguientes secciones:

* [Tipos de tokens](#token-types)
* [Almacenamiento de token](#token-storage)
* [Seguridad de token](#token-security)
* [Uso compartido de tokens](#token-sharing)

### Tipos de tokens {#token-types}

Durante los flujos de trabajo de autenticación y autorización se emiten tres tipos de tokens. Los tokens AuthN y AuthZ son de &quot;larga duración&quot;, lo que proporciona continuidad en la experiencia de visualización del usuario. El token de medios es un token de corta duración que admite las prácticas recomendadas del sector para evitar fraudes mediante la extracción por secuencias. Los programadores especifican los valores de tiempo de vida (TTL) para cada tipo de token en función de los acuerdos celebrados con MVPD. Los programadores deciden el valor TTL que mejor se adapte a su negocio y a sus clientes.

* **Token de AuthN** (&quot;De larga duración&quot;): tras la autenticación correcta, la autenticación de Adobe Primetime crea un token de AuthN asociado tanto al dispositivo solicitante como a un identificador único global (GUID).
   * La autenticación de Adobe Primetime envía el token de AuthN al activador de acceso, que lo almacena en caché de forma segura en el sistema del cliente.  Aunque el token de AuthN está allí y no ha caducado, está disponible para todas las aplicaciones que utilizan la autenticación de Adobe Primetime. El Habilitador de acceso utiliza el token de AuthN para el flujo de autorización.
   * En un momento determinado, solo se almacena en caché un token de AuthN. Siempre que se emite un nuevo token de AuthN y ya existe uno antiguo, la autenticación de Adobe Primetime sobrescribe el token almacenado en caché.
* **Token de AuthZ** (&quot;Larga duración&quot;): tras una autorización correcta, la autenticación de Adobe Primetime crea un token de AuthZ asociado con el dispositivo solicitante y un recurso protegido específico.  El recurso protegido se identifica con un ID de recurso único.
   * La autenticación de Adobe Primetime envía el token de AuthZ al activador de acceso, que lo almacena en caché de forma segura en el sistema local. A continuación, el Access Enabler utiliza el token de AuthZ para crear el token de medios de corta duración que se utiliza para el acceso de visualización real.
   * En cualquier momento dado, solo se almacena en caché un token de AuthZ por recurso. La autenticación de Adobe Primetime puede almacenar en caché varios tokens de AuthZ, siempre y cuando estén asociados a diferentes recursos. Siempre que se emite un nuevo token de AuthZ y ya existe uno antiguo para el mismo recurso, la autenticación de Adobe Primetime sobrescribe el token almacenado en caché.
* **Token de medios** (&quot;De corta duración&quot;): El Habilitador de acceso utiliza el token de AuthZ para generar un token de medios de corta duración (predeterminado: 7 minutos). Este es el punto en el que se considera que se ha producido una solicitud de reproducción correcta.
   * Antes de proporcionar acceso al recurso protegido, el servidor de medios debe utilizar un componente de autenticación de Adobe Primetime, el Verificador de tokens de medios, para validar el token de medios.
   * Dado que el token de medios no está enlazado al dispositivo, su duración es significativamente menor (valor predeterminado: 7 minutos) que la de los tokens de AuthN y AuthZ de larga duración.
   * El token de medios de corta duración está restringido a un uso único y nunca se almacena en caché. Se recupera del servidor de autenticación de Adobe Primetime cada vez que se llama a una API de autorización.

### Almacenamiento de token {#token-storage}

Access Enabler almacena tokens de larga duración (AuthN y AuthZ) en ubicaciones específicas de su entorno:

* **Flash 10.1** (o superior): Los tokens de larga duración se almacenan como objetos compartidos locales.
* **HTML 5**: los tokens de larga duración se guardan de forma segura en el almacén local del explorador HTML5.
* **iOS**: los tokens de larga duración se almacenan en una mesa de trabajo persistente, donde otras aplicaciones cliente de autenticación de Adobe Primetime pueden acceder a ellos.
* **Android**: los tokens de larga duración se almacenan en un archivo de base de datos compartida, donde otras aplicaciones cliente de autenticación de Adobe Primetime pueden acceder a ellos.
* **Dispositivos API sin cliente**: los tokens se almacenan en los servidores de autenticación de Primetime.

### Seguridad de token {#token-security}

El servidor de autenticación de Adobe Primetime firma digitalmente todos los tokens de larga duración utilizando el ID del dispositivo (derivado de las características de hardware del dispositivo). La firma digital difiere en cómo se genera, protege y valida según el entorno:

* **Flash 10.1** (o superior): el ID del dispositivo se basa en la credencial del dispositivo, un certificado único emitido desde el servidor de individualización de Adobe. Esta seguridad es equivalente a la tecnología DRM de FAXS. Esta validación del lado del servidor compara el ID de dispositivo único del token con las credenciales del dispositivo (que se comunican de forma segura desde el Flash Player a la autenticación de Adobe Primetime). La credencial del dispositivo también identifica la versión del cliente de FAXS y la versión de Flash Player (o AIR) a la que se emitió. El enlace del dispositivo es más fuerte que con HTML5, por lo que el tiempo de vida (TTL) de los tokens suele ser mayor con el Flash.
* **HTML 5** - El dispositivo está individualizado en el lado del cliente. Utiliza las características disponibles a través de JavaScript para generar un ID seudodispositivo que incluye versiones de explorador y sistema operativo, una dirección IP y un GUID de cookie de explorador (identificador único global). Este ID de dispositivo de token se compara con el ID de pseudodispositivo actual para el dispositivo. Dado que la dirección IP puede cambiar durante el uso normal, incluso en la misma sesión, la autenticación de Adobe Primetime almacena tokens de HTML5 en dos ubicaciones: localStorage y sessionStorage. Si la IP cambia y el token sessionStorage sigue siendo válido, la sesión se mantiene. Con HTML5, el enlace del dispositivo no es tan fuerte, por lo que el TTL para tokens suele ser más corto que para Flash.
* **Clientes nativos** (iOS y Android): los tokens de larga duración contienen información de individualización de ID de dispositivo nativo y, por lo tanto, están enlazados al dispositivo solicitante. Las solicitudes de autenticación y autorización se envían a través de HTTPS y la biblioteca del Habilitador de acceso firma digitalmente la información del ID del dispositivo antes de enviarla a los servidores back-end. En el servidor, la información del ID de dispositivo se valida con su firma digital asociada.
* **Clientes de API sin cliente** : la solución de API sin cliente tiene su conjunto de protocolos de seguridad que implican firmar digitalmente todas las llamadas de API. Los tokens generados durante los flujos de derechos se almacenan de forma segura en los servidores de autenticación de Adobe Primetime.

La autenticación de Adobe Primetime valida cada token de larga duración para garantizar que el dispositivo que accede al contenido sea el mismo que el que emitió el token. Para todos los tokens, una validación del lado del cliente garantiza que la firma digital esté intacta y que se preserve la integridad del token. Cuando falla la validación del ID del dispositivo, la sesión de autenticación se invalida y se solicita al usuario que vuelva a iniciar sesión, lo que restablece los tokens.

### Uso compartido de tokens {#token-sharing}

Las aplicaciones de plataformas diferentes no comparten tokens. Esto se debe a varias razones, entre ellas las siguientes:

* Como se describe en [Almacenamiento de token](#token-storage)Sin embargo, el método de almacenamiento de tokens varía según la plataforma (por ejemplo, Local Shared Objects para Flash o WebStorage para JavaScript).
* El grado de seguridad del token difiere entre plataformas. Por ejemplo, los tokens de Flash están fuertemente enlazados a un dispositivo mediante FAXES. Los tokens de un entorno JavaScript puro no tienen el mismo nivel de compatibilidad con DRM que en Flash.  Compartir tokens JS con aplicaciones de Flash aumentaría las posibilidades de que tokens menos seguros exploten un entorno más seguro.

## Ciclo de integración del programador {#prog-integ-lifecycle}

![](assets/progr-flow-int-lifecycle.png)

*Figura: Integración de Authentication con el sitio web y la aplicación del programador*


## Flujos lógicos {#logical-flows}

### Diagrama de flujo de derechos {#chart}

El siguiente diagrama de flujo presenta el proceso general de confirmación de la asignación de derechos (mediante el componente de cliente Habilitador de acceso a la autenticación de Adobe Primetime):

![](assets/ent-flowchart.png)

*Figura: Proceso de confirmación del derecho*

### Pasos de autenticación {#authn-steps}

Los siguientes pasos presentan un ejemplo del flujo de autenticación de Adobe Primetime.  Es la parte del proceso de asignación de derechos en la que un programador determina si el usuario es un cliente válido de una MVPD.  En esta situación, el usuario es un suscriptor válido de una MVPD.  El usuario está intentando ver contenido protegido mediante una aplicación de Flash del programador:

1. El usuario navega a la página web del programador, que carga la aplicación Flash del programador y los componentes del activador de acceso de autenticación de Adobe Primetime en el equipo del usuario. La aplicación de Flash utiliza el Habilitador de acceso para establecer la identificación del Programador con la autenticación de Adobe Primetime, y la autenticación de Adobe Primetime prima el Habilitador de acceso con datos de configuración y estado para ese Programador (el &quot;solicitante&quot;). El Habilitador de acceso debe recibir estos datos del servidor antes de realizar cualquier otra llamada de API. Nota técnica: el programador establece su identidad con el activador de acceso `setRequestor()` método; para obtener más información, consulte la [Guía de integración del programador](/help/authentication/programmer-integration-guide-overview.md).
1. Cuando el usuario intenta ver el contenido protegido del Programador, la aplicación del Programador presenta al usuario una lista de MVPD, desde la cual el usuario selecciona un proveedor.
1. Se redirige al usuario a un servidor de autenticación de Adobe Primetime, donde se cifra un [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) Se crea una solicitud para el MVPD seleccionado por el usuario. Esta solicitud se envía como una solicitud de autenticación en nombre del programador al MVPD. Según el sistema de la MVPD, el explorador del usuario se redirige al sitio de la MVPD para iniciar sesión o se crea un iFrame de inicio de sesión en la aplicación del programador.
1. En cualquier caso (redirección o iFrame), MVPD acepta la solicitud y muestra su página de inicio de sesión.
1. El usuario inicia sesión con la MVPD, la MVPD valida el estado del usuario como cliente de pago y luego la MVPD crea su propia sesión HTTP.
1. Cuando se valida al usuario, la MVPD crea una respuesta (SAML y cifrada) que la MVPD devuelve a la autenticación de Adobe Primetime.
1. La autenticación de Adobe Primetime recibe la respuesta de MVPD, observa que hay una sesión HTTP de autenticación de Adobe Primetime abierta, valida la respuesta de SAML de MVPD y redirige de nuevo al sitio del programador.
1. Se vuelve a cargar el sitio del Programador, se vuelve a cargar el Habilitador de acceso y el Programador vuelve a llamar a setRequestor().  La segunda llamada a setRequestor() es necesaria porque la configuración actual ha cambiado. Ahora hay un indicador presente que informa al Habilitador de acceso de que un token AuthN está esperando a generarse en el servidor.
1. Access Enabler ve que hay una autenticación pendiente y solicita el token al servidor de autenticación de Adobe Primetime. El token se recupera del servidor invocando las capacidades DRM del Flash Player.
1. El token de AuthN se almacena en la memoria caché LSO de Flash Player del programador; la autenticación se completa y la sesión se destruye en el servidor de autenticación de Adobe Primetime.

### Pasos de autorización {#authz-steps}

Los siguientes pasos continúan desde el [Pasos de autenticación](#authn-steps):

1. Cuando el usuario intenta acceder al contenido protegido del programador, la aplicación del programador comprueba primero si hay un token AuthN en el equipo o dispositivo local del usuario.  Si ese token no está allí, la variable [Pasos de autenticación](#authn-steps) se siguen las instrucciones anteriores.  Si el token de AuthN está allí, el flujo de autorización continúa con la aplicación del programador que inicia una llamada al activador de acceso con una solicitud para obtener los derechos de visualización del usuario para un elemento específico de contenido protegido.
1. El elemento específico del contenido protegido se representa mediante un &quot;identificador de recurso&quot;.  Podría ser una cadena simple o una estructura más compleja, pero en cualquier caso la naturaleza del identificador de recursos se acuerda con antelación entre el programador y el MVPD.  La aplicación del programador pasa el identificador de recursos al Habilitador de acceso.  Access Enabler comprueba si hay un token de AuthZ en el equipo o dispositivo local del usuario.  Si el token de AuthZ no está allí, el Habilitador de acceso pasa la solicitud al servidor de autenticación de Adobe Primetime back-end.
1. El servidor de autenticación de Adobe Primetime se comunica con el extremo de autorización de MVPD mediante protocolos estandarizados.  Si la respuesta de la MVPD indica que el usuario tiene derecho a ver el contenido protegido, el servidor de autenticación de Adobe Primetime crea un token de AuthZ y lo devuelve al Habilitador de acceso, que almacena el token de AuthZ en el equipo del usuario.
1. Con un token de AuthZ almacenado en el equipo o dispositivo del usuario, la aplicación del programador llama al Habilitador de acceso para obtener un token de medios del servidor de autenticación de Adobe Primetime y proporciona ese token a la aplicación del programador.
1. Por último, la aplicación del programador utiliza el componente Verificador de tokens de medios para confirmar que el usuario correcto está viendo el contenido correcto y, con el token de medios en su lugar, el usuario puede ver el contenido protegido.


## Registro e inicialización {#reg-and-init}

El primer paso para trabajar con la autenticación de Adobe Primetime es registrarse con Adobe o con un socio autorizado de autenticación de Adobe Primetime.

Al registrarse, proporciona una lista de los dominios desde los que se comunicará con la autenticación de Adobe Primetime. Por ejemplo, los dominios de Turner Broadcasting System incluyen tbs.com y tnt.tv como dominios registrados para la autenticación de Adobe Primetime. A cada uno de estos sitios de contenido se le da acceso a la autenticación de Adobe Primetime y se le asigna su propio ID de solicitante (por ejemplo, &quot;TBS&quot; y &quot;TNT&quot;). Si decide agregar sitios adicionales, debe informar al Adobe de los nombres de dominio adicionales para que se coloquen en la lista de dominios permitidos y se les proporcionen ID de solicitante adicionales.

>[!WARNING]
>
>Mientras prueba la integración, asegúrese de que el servidor de prueba se encuentra en un dominio registrado que desea utilizar en producción. Las solicitudes, incluso las solicitudes de prueba, procedentes de dominios que no están en la lista blanca se ignoran. Por ejemplo, si ha solicitado que domain.com se utilice en producción, asegúrese de implementar la integración de prueba en domain.com, test.domain.com y staging.domain.com.
>
>Las solicitudes que contienen un nombre de usuario y/o una contraseña en la dirección URL se ignoran incluso si los dominios están en la lista blanca. Ejemplo: `//username@registered-domain/`

El ID de solicitante identifica de forma exclusiva al cliente del programador en todas las comunicaciones con el componente de cliente Access Enabler de la autenticación de Adobe Primetime. Todos los datos estáticos de autenticación de Adobe Primetime asociados con el programador tienen una clave para este ID.

>[!TIP]
>
>Además del ID de solicitante, al registrarse también recibe direcciones URL funcionales para el componente de cliente del Habilitador de acceso y el Verificador de tokens de medios.

## Pasos de integración {#integration-steps}

>[!TIP]
>
>Si utiliza el Open Source Media Framework de Adobe (&quot;OSMF&quot;) para el desarrollo del reproductor de contenidos, la forma más rápida de utilizar la autenticación de Adobe Primetime es integrar el complemento OSMF *(Obsoleto)* en el código del reproductor.
>
><!--For details, see [Adobe Primetime authentication Plugin For OSMF](https://tve.helpdocsonline.com/9-2-2) in the Programmer Integration Guide.-->

1. [Configuración del solicitante](#requestor)
1. [Administrar autenticación y autorización](#authn-authz)
1. [Compatible con cierre de sesión único](#ssl)

### 1. Configuración del solicitante {#requestor}

#### 1 bis. Registro en el Adobe

El primer paso es registrarse con Adobe o con un socio autorizado de autenticación de Adobe Primetime.  Cuando se registra, se le emiten uno o más identificadores únicos globales (GUID). Cada GUID que se emita está asociado a un dominio desde el que se permite el acceso a la autenticación de Adobe Primetime. Pasa un GUID (denominado ID del solicitante) para el dominio solicitante para registrar su identidad en cada sesión en la que interactúe con el Habilitador de acceso. Para obtener más información, consulte [Registro e inicialización](#reg-and-init) en la Guía de integración del programador.

#### 1 ter. Integración del Habilitador de acceso inicial

El siguiente paso es integrar Access Enabler en la aplicación o página web del reproductor de medios existente:

* Puede incrustar la versión del Flash, `AccessEnabler.swf`, en un reproductor de vídeo basado en Flash o puede incrustarlo directamente en el HTML de la página web. Puede comunicarse con el SWF del Habilitador de acceso en ActionScript o JavaScript. La API base es el ActionScript, pero si prefiere trabajar con JavaScript, encontrará una biblioteca de envoltorios completa para incluirla en sus páginas.
* En los entornos que no son de Flash, puede:
   * Utilice la versión de HTML 5/JavaScript, AccessEnabler.js, y comunique con él a través de la API de JavaScript
   * Utilice la extensión nativa de AIR para la autenticación de Adobe Primetime para combinar código nativo con clases de ActionScript integradas
   * Utilice una de las versiones de cliente nativas de la biblioteca Access Enabler (iOS o Android)

### 2. Administrar la autenticación y la autorización {#authn-authz}

#### 2 bis. Comunicarse con el Habilitador de acceso

La comunicación entre el Habilitador de acceso y su página web o aplicación de reproducción es asíncrona. La aplicación llama a los métodos del Habilitador de acceso, y el Habilitador de acceso responde mediante llamadas de retorno que se registran en la biblioteca del Habilitador de acceso.

* Cuando la aplicación realiza una solicitud de autorización, el Habilitador de acceso inicia automáticamente una solicitud de autenticación, si no hay un token de AuthN válido en el sistema local. Cuando la autenticación se realiza correctamente, el token AuthN del usuario se almacena localmente para que no tenga que volver a iniciar sesión. Si se ha autenticado correctamente a través de la autenticación de Adobe Primetime en cualquier otro contexto (por ejemplo, a través del sitio web de MVPD o con un programador diferente), el habilitador de acceso tiene acceso al token de AuthN local y no se necesita una autenticación adicional.
* Cuando un usuario intenta acceder al contenido protegido, envía una solicitud de autorización al Habilitador de acceso. Después de verificar (o iniciar) la autenticación, el Habilitador de acceso se pone en contacto con la MVPD (a través del servidor de autenticación de Adobe Primetime) para determinar si el cliente tiene derecho a ver el contenido protegido. La aplicación solo necesita enviar la solicitud al Habilitador de acceso y, a continuación, administrar la respuesta (éxito o error de autorización). Si la autorización se realiza correctamente, se almacena un token de AuthZ en el sistema cliente.  Por último, la aplicación recibe un token de medios de corta duración para utilizarlo en su propio procedimiento de autorización.

>[!NOTE]
>
>* La autenticación se produce como un intercambio SAML, entre la autenticación de Adobe Primetime como proveedor de servicios (SP) y la MVPD como proveedor de identidad (IdP).
>
>* La autorización utiliza un intercambio de servicio web de canal de retorno (servidor a servidor) entre la autenticación de Adobe Primetime (el SP) y un MVPD (el IdP).


#### 2 ter. Proporción De Una Interfaz De Usuario De Derechos {#entitlement-ui}

Proporcione su propia interfaz de usuario para que el usuario tenga acceso a su contenido. Algunos elementos, como el proceso de inicio de sesión real, los proporciona la MVPD y algunos elementos están disponibles de forma opcional como parte de la autenticación de Adobe Primetime. Como mínimo, debe hacer lo siguiente:

* **Implementar una interfaz de selección de MVPD que permita a un nuevo usuario identificar su MVPD e iniciar sesión por primera vez**. Para el desarrollo, el Access Enabler proporciona una interfaz de usuario básica que ofrece al cliente una variedad de MVPD e inicia el proceso de inicio de sesión. Para la producción, debe implementar su propio cuadro de diálogo Selector de MVPD. Algunas MVPD redirigen a su propio sitio para iniciar sesión y otras requieren que sus páginas de inicio de sesión se muestren dentro de un iFrame. Debe implementar una llamada de retorno que cree este iFrame para controlar los casos en los que la MVPD del usuario muestra su página de inicio de sesión en un iFrame.
* **Identificación de contenido protegido**. El contenido protegido requiere autorización para acceder a. La interfaz debe indicar qué contenido está protegido y qué contenido se ha autorizado.  El estado de autorización suele indicarse con iconos &quot;desbloqueados&quot; y &quot;bloqueados&quot;.
* **Mostrar que un usuario está autenticado**. Debe indicar el estado de autenticación de un usuario como parte de cualquier medio que utilice para identificar contenido protegido. Puede consultar el Habilitador de acceso para determinar si el cliente ya se ha autenticado.

#### 2 quater. Integración del verificador de tokens de medios {#int-media-token-ver}

Debe integrar el componente Verificador de tokens de medios de autenticación de Adobe Primetime en su servidor de medios.  De este modo, el verificador de tokens existente puede reconocer los tokens de medios de corta duración proporcionados desde la autenticación de Adobe Primetime con una autorización correcta. El Verificador de tokens de medios valida los tokens de medios como el último paso de seguridad antes de proporcionar al usuario acceso al contenido protegido. Recibirá la ubicación desde la que desea descargar el Media Token Verifier cuando se registre en Adobe.

### 3. Compatibilidad con el cierre de sesión único {#ssl}

En la mayoría de los casos, el reproductor de contenido es responsable de administrar los cierres de sesión de los usuarios a través de una sencilla API de Access Enabler. Cuando llama a logout(), el Habilitador de acceso hace lo siguiente:

* Cerrar sesión del usuario actual
* Borra toda la información de autenticación y autorización del usuario que ha cerrado la sesión
* Elimina todos los tokens AuthN y AuthZ del sistema local del usuario

Si el usuario deja el equipo inactivo el tiempo suficiente para que los tokens caduquen, puede volver a la sesión e iniciar el cierre de sesión correctamente. La autenticación de Adobe Primetime garantiza que todos los tokens se eliminen y notifica a la MVPD que también elimine su sesión.

Cuando el cierre de sesión se inicia desde un sitio que no está integrado con la autenticación de Adobe Primetime, la MVPD puede invocar el servicio de cierre de sesión único de autenticación de Adobe Primetime mediante una redirección del explorador.

## Explicación de los ID de usuario {#user-ids}

Conceptualmente, cada usuario que inicia un flujo de derechos se asocia con un único ID de usuario único.  Sin embargo, a lo largo de un flujo de derechos, ese ID de usuario se puede presentar de diferentes maneras, en función de la API de la que obtenga el ID.

El sessionGUID del token de medios corto es la forma segura del UserID, que está disponible a través de la llamada sendTrackingData().   En todas las integraciones actuales, se trata de un GUID persistente para el usuario a lo largo del tiempo y los dispositivos, pero el origen del GUID comienza con el UserID en la respuesta SAML de MVPD.   Sin embargo, algunas MVPD podrían cambiar de opinión en el futuro y comenzar a enviar un GUID transitorio.  Si un programador desea asegurarse de que el ID de usuario de origen de MVPD en la respuesta AuthN sea persistente, debe solucionarlo en sus acuerdos con MVPD.

Estas son las diferentes formas en que el ID de usuario se representa en las API de autenticación de Adobe Primetime:

* `sendTrackingData()` Propiedad GUID: esta es la versión con hash de Adobe del UserID de MVPD.  Tiene un hash que impide que se pueda rastrear este ID de usuario hasta el origen desde la MVPD.   Este ID es único y suele ser persistente, pero no se puede compartir con la MVPD para comparar el comportamiento de uso específico con el que tienen las MVPD de su parte.   No está firmado digitalmente, por lo que no es imperdonable para la prevención del fraude, pero es lo suficientemente bueno para el análisis.  Esta forma de ID de usuario se proporciona del lado del cliente en todos los eventos que la autenticación de Adobe Primetime genera en el flujo AuthN/AuthZ.
* Token de medios corto `sessionGUID` propiedad: es lo mismo que el ID de usuario mediante `sendTrackingData()`, sin embargo, este está firmado digitalmente para proteger su integridad.  Esto hace que este valor sea lo suficientemente bueno para el seguimiento de fraude del uso simultáneo. Está pensado para procesarse en el servidor después de utilizar nuestra biblioteca de validación y puede analizarse en busca de patrones de fraude antes de lanzar el flujo de vídeo al cliente.  Realizar cualquiera de estas tareas depende del Programador.
* `getMetadata() userID `propiedad: esta propiedad permitirá que el Adobe exponga el UserID de MVPD de origen real al programador. Se cifrará con la clave pública del certificado que tenemos del Programador, para que no se exponga en el claro al cliente. Esto le da al programador el ID de usuario real de la MVPD, por lo que es algo que puede usarse para vincular cuentas o investigar fraudes directamente con la MVPD.

**En conclusión**

* El ID de usuario de MVPD es un ID único persistente general, aunque no garantizado, que **se generan a partir de las MVPD y se pasan al Adobe cuando la autenticación es correcta**. En general, es coherente en todas las redes, con algunas excepciones.
* El ID de usuario de MVPD no contiene PII y NO es un número de cuenta. No necesita exponerse en forma cifrada, ya que hemos validado con todas las MVPD que no se envía ninguna PII.


El uso del ID de usuario depende del caso de uso:

* Si lo necesita para seguimiento/análisis, el lugar más práctico es obtenerlo de `sendTrackingData()`.
* Si lo necesita en el lado del servidor para la publicación de secuencias, el fraude o los datos operativos, puede obtenerlo en Media Token Validator.
* Si lo necesita para vincular cuentas y cometer fraudes más profundos, consulte con su contacto de Adobe la disponibilidad.

<!--
>[!RELATEDINFORMATION]
>
>* **Kickstart Guides** These guides explain the initial steps to take once you have decided to begin integrating with Adobe Primetime authentication.
>* **Programmer Integration Guide** This is a lower level technical guide for Programmers, directed primarily to the software engineers who code and test the applications and systems involved in the integration.
>* [Overview For MVPDs](/help/authentication/mvpd-overview.md) This provides a similar level of conceptual information as in this Programmer overview, but is directed toward MVPDs.
-->
