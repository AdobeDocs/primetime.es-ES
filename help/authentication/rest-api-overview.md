---
title: Información general de la API de REST
description: Información general sobre las API de Rest
source-git-commit: 4c3a0dd56b4ef99ac8c57cfde61f792088b0ff4d
workflow-type: tm+mt
source-wordcount: '1644'
ht-degree: 0%

---


# Información general de la API de REST {#rest-api-overview}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.


## Información general {#over}

La API de REST de autenticación de Adobe Primetime proporciona acceso directo a los servicios de autenticación y autorización de TV en todas partes (TVE). Esta API admite dos arquitecturas principales: Dispositivos conectados o de servidor a servidor (por ejemplo, consolas de juegos, televisores inteligentes, receptores de televisión, etc.) aplicaciones que no tienen capacidades de navegación web. 

 

### Servidor a servidor

Las soluciones de servidor a servidor implican aplicaciones cliente de programador que se integran con servicios de programador que se conectan con servicios de autenticación de Adobe Primetime para flujos TVE. Este enfoque cambia la mayor parte de la implementación de TVE del cliente al servidor, donde se puede crear y mantener un módulo de autorización único y unificado. La responsabilidad principal restante de las aplicaciones cliente es la administración de una vista web para la autenticación de usuarios.

 

### Dispositivos conectados

Las aplicaciones de dispositivos conectados se comunican directamente con la autenticación de Primetime a través de las API de REST para realizar la configuración, el registro, las comprobaciones de estado de autenticación y los flujos de autorización, mientras que se requiere una segunda aplicación de pantalla (explorador) para el flujo de autenticación. Por lo tanto, no se utilizan SDK nativos.

 

### Otras arquitecturas

Además de las dos arquitecturas principales basadas en la API de REST, las soluciones de cliente de servidor a servidor y las soluciones de cliente directo para dispositivos inteligentes, existen otras arquitecturas.  El principal de ellos es la arquitectura del SDK, que utiliza un componente cliente llamado Access Enabler que la autenticación de Primetime proporciona a los programadores.  La aplicación utiliza las API de Access Enabler para gestionar el inicio, la autenticación, la autorización y el cierre de sesión.  Toda la comunicación entre la aplicación del programador y los servidores de autenticación de Primetime se produce a través de Access Enabler.  Hay disponible un tipo diferente de Access Enabler para las siguientes plataformas: JavaScript, iOS, tvOS, Android y FireTV.

Aunque es posible utilizar la API de REST directamente en plataformas cliente que admitan SDK nativos fuera de una solución de servidor a servidor, no se recomienda este método.

 

## Ventajas y ventajas de la API de REST {#ProsAndCons}

La API de REST de autenticación de Adobe Primetime se creó para proporcionar una solución de TV en todas partes (TVE) para dispositivos que no tienen capacidades de navegación web ni almacenamiento persistente. La API de REST es compatible con todos los flujos de autenticación y autorización, pero no tiene un componente SDK nativo. Los SDK proporcionados y mantenidos por la autenticación de Adobe Primetime incluyen funcionalidades integradas que implementan reglas comerciales que, en el caso de la API de REST, los programadores deben implementar y mantener. En la tabla Responsabilidades del programador que aparece a continuación describimos las limitaciones de la API de REST actual que deben ser abordadas por los programadores.

 

### Ventajas e inconvenientes de servidor a servidor frente a clientes

Una arquitectura de servidor a servidor permite consolidar la mayor parte de la lógica relacionada con la autenticación y la autorización en una única unidad lógica o implementación.  Este enfoque tiene pros y contras.  Las ventajas incluyen:

* Implementación única para la lógica empresarial de autenticación y autorización.
* Evite la necesidad de implementar esa lógica en cada plataforma admitida mediante las herramientas nativas de esas plataformas.
* La capacidad de actualizar las capacidades sin tener que actualizar a los clientes con todos sus requisitos asociados (por ejemplo, actualizaciones de la tienda de aplicaciones).
* **Más fácilmente** ampliar y personalizar las capacidades authN y authZ (por ejemplo, añadir D2C).
* Gestión directa del tráfico asociado para buenos controles, calidad y seguimiento.

 

Una vez más, los contras se enumeran en las responsabilidades del Programador, pero incluyen lo siguiente:

* SSO debe implementarse para cada cliente para plataformas sin SSO de plataforma.
* Los programadores deben implementar la lógica específica de MVPD si es necesario.
* Todas las plataformas que utilizan la API de REST comparten una sola configuración que rige propiedades como los TTL de autenticación.

 

### Dispositivos conectados

Para la mayoría de los dispositivos conectados, la API de REST debe usarse de una u otra forma, ya que un SDK no está disponible. El dispositivo conectado utilizará la API de REST directamente o se integrará con una solución de servidor a servidor que utilice la API de REST.

## Responsabilidades del programador {#programmer-responsibilities}

Lo siguiente se aplica tanto a las aplicaciones de servidor a servidor como a las aplicaciones de dispositivo conectado.

| **Funcionalidad** | **Responsable de la gestión de la funcionalidad** | **Descripción de las limitaciones de la API actual sin cliente y diferencias con respecto a los SDK nativos** |
| --- | --- | --- |
| Ajustes de configuración aplicados por plataforma | Adobe | One **limitación principal** al usar la API de REST en todas las plataformas (incluidos dispositivos móviles como iOS y Android), es que los ajustes de configuración correspondientes a la API de REST en nuestra herramienta de configuración TVE Dashboard se aplican a todos los dispositivos (incluso si hay un dispositivo iOS que ejecute una aplicación nativa implementada sobre nuestra API de REST). Esta limitación **se puede interrumpir** los TTL acordados y la configuración de plataforma acordada con los MVPD, si difieren según cada plataforma. [1](#1) |
| Inicio de sesión único | Programadores | Con la API de REST, SSO solo está disponible en plataformas compatibles con SSO de plataforma (por ejemplo, Apple, Roku, Amazon) mientras que SSO no se puede garantizar para otras plataformas al utilizar la API de REST. Los SDK almacenan en caché los datos de forma entre sitios o aplicaciones. Esto significa que el usuario inicia sesión una vez en un sitio o aplicación y ya ha iniciado sesión en los sitios participantes, sin necesidad de interacción del usuario. [2](#2) |
| Inicio de sesión único | Programadores | En un caso de SSO de SDK nativo, cuando se cierre la sesión desde una aplicación participante, se cerrará la sesión del usuario en todas partes. En la API de REST actual no se admite SLO, cuando se cierre la sesión desde una aplicación, solo se cerrará la sesión del usuario para esa aplicación en particular. |
| Almacenamiento en caché | Programadores | Las implementaciones de la API de REST tendrán que implementar su propio mecanismo de almacenamiento en caché para los elementos de datos acordados por la empresa. Los SDK almacenan automáticamente en caché varios elementos de datos, teniendo en cuenta varias reglas comerciales. Por ejemplo, los metadatos de usuario se almacenan en caché con el mismo TTL que el token de autenticación, mientras que algunos elementos se pueden excluir mediante programación del almacenamiento en caché (comprobación previa). |
| Mecanismo detallado de informes de errores | Programadores | La API de REST se basa principalmente en códigos de error HTTP para informar de errores de aplicaciones, mientras que los SDK tienen un mecanismo detallado de informes de errores que ayuda a los desarrolladores de aplicaciones a comprender mejor lo que está sucediendo. |
| Recuperación de errores de aplicación (reintento en caso de error, detección de bucle, etc.) | Programadores | Las implementaciones de API de REST deben crear sus propios sistemas de recuperación de aplicaciones, mientras que las implementaciones además de los SDK se benefician del sistema de recuperación de errores de los SDK: recuperarse de errores de red transitorios, reintentando ciertas llamadas de red con lógica en su lugar para evitar &quot;bucles&quot;. |
| Autenticación por solicitante | Programadores | Algunos MVPD requieren autenticación para cada sitio o aplicación, ya sea por motivos comerciales o debido a desafíos técnicos. Los SDK aplican esto automáticamente en función de la configuración del TVE Dashboard. Los implementadores de la API de REST deben implementarlo ellos mismos, para no infringir los acuerdos comerciales, o para poder completar la autorización para aquellos MVPD que abarquen sus datos de autenticación por aplicación. |
| Autenticación pasiva | Programadores | Algunos MVPD admiten autenticación &quot;pasiva&quot;, en la que el usuario no tiene que introducir las credenciales y se intenta autenticar al usuario automáticamente. Esto resulta especialmente útil para los MVPD que también tienen como requisito la &quot;autenticación por solicitante&quot;. En tal caso, el UX habilitado por los SDK es fluido, donde el usuario se autentica una sola vez en una aplicación y el SDK realiza la autenticación &quot;pasiva&quot; para otras aplicaciones del ecosistema. El usuario no ve las llamadas pasivas adicionales, simplemente ya estará autenticado, mientras que el MVPD logra el objetivo de tener sesiones de autenticación independientes para cada aplicación. |
| Detección de dispositivos implícita y uniforme | Programadores | Los SDK detectan automáticamente el tipo de dispositivo y envían esa información de forma estándar. Las implementaciones de API de REST son propensas a enviar información diferente, según el implementador, lo que distorsiona o rompe las reglas y estadísticas comerciales entre sitios. **Los programadores deben asegurarse de que nos han enviado correctamente [información del dispositivo](http://tve.helpdocsonline.com/passing-device-information) en cada una de sus** aplicaciones. Para implementaciones de servidor a servidor, la api de REST no identifica correctamente la dirección IP del usuario final, a menos que se realicen pasos adicionales. La dirección IP es importante en algunos casos de uso, como la prevención del fraude o el HBA. Consulte [cómo pasar la dirección IP del cliente en implementaciones del lado del servidor](http://tve.helpdocsonline.com/clientless-integration-cookbook-v2$overall_clientIP). |
| Tamper proof TempPass | Programadores | La aplicación de TempPass se basa en un ID de dispositivo estable. Los SDK utilizan información de hardware/técnicas de huellas digitales para identificar el dispositivo y este mecanismo no es público, por lo que es más seguro y no tiene conflictos. Para las implementaciones de la API de REST, los programadores deben implementar sus propios algoritmos para la identificación y toma de huellas digitales de dispositivos. |
| Enlace de dispositivos | Programadores | Los tokens generados en un dispositivo con una aplicación sobre SDK no son portátiles, lo que dificulta a un usuario malintencionado compartir sus tokens y proporcionar acceso a otros usuarios. Esto se basa en el mismo mecanismo de identificación del dispositivo que el &quot;TempPass de prueba de manipulaciones&quot;. Para la API de REST, los tokens permanecen en la nube, lo que significa que dos dispositivos con los mismos ID de dispositivo que realizan las mismas llamadas recibirán las mismas respuestas/acceso. Los programadores deben asegurarse de que tienen un mecanismo seguro y robusto que no interfiera con la generación o asignación de ID de dispositivo. |
| Conjunto de funciones predecible y certificado | Programadores | El conjunto existente de funciones en cada SDK es coherente, predecible y está completamente certificado y probado. Algunos requisitos comerciales se refuerzan mediante los SDK, por lo que es arriesgado que el programador infrinja los contratos mientras utiliza la API de REST. Aunque la API de REST puede ser más flexible, Adobe garantiza que las implementaciones de SDK apliquen las decisiones empresariales y la configuración desde TVE Dashboard. En el caso de Clientless, cada Programador implementa su propio subconjunto de reglas comerciales que agrupan sus aplicaciones en un momento dado. |


1. Como parte de nuestra nueva iniciativa One API (Una API) planeamos corregir esta limitación y poder aplicar reglas por plataforma en función de la identificación del dispositivo.

2. Adobe sigue trabajando con todas las plataformas principales para implementar el SSO de plataforma que se puede utilizar con nuestra API de REST. Nuestra iniciativa Una API ofrecerá compatibilidad con SSO entre aplicaciones implementadas mediante SDK y aplicaciones nativas implementadas mediante la API de REST.

## Requisitos mínimos de dispositivo {#min_reqs}

Para utilizar la API de REST de autenticación de Primetime, los dispositivos deben cumplir o superar los requisitos técnicos mínimos enumerados en la sección de la API de REST de la [Documento de requisitos de plataforma/dispositivo/herramientas de autenticación de Primetime](#general_clientless_reqs).

## Medios relacionados {#related}

* [Flujo de derechos del programador](https://tve.helpdocsonline.com/entitlement-flow)
* [Referencia de API de REST](http://tve.helpdocsonline.com/registration-code-request)
* [Guía de la API de REST (servidor a servidor)](http://tve.helpdocsonline.com/rest-api-cookbook-server-to-server) 
* [Guía de la API de REST (cliente a servidor)](http://tve.helpdocsonline.com/rest-api-cookbook-client-to-server)

<!--* [Platform / Device / Tool Requirements](#)-->
