---
title: Plan de integración directa de MVPD
description: Plan de integración directa de MVPD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---

# Guía de inicio de MVPD: plan de integración directa de MVPD {#mvpd-dir-int-plan}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.

## Introducción {#mvpd-kickstart-intro}

Bienvenido a la autenticación de Adobe Primetime para TV en todas partes.  Esperamos poder trabajar con usted.

>[!NOTE]
>
>Esta es la Guía de KickStart para Distribuidores de Programación de Vídeo Multicanal (MVPD). Si es programador (proveedor de contenido), consulte la [Guía de KickStart para programadores](/help/authentication/programmer-kickstart-guide.md).

El soporte está disponible en todo momento a través del sistema de tickets de autenticación de Primetime en Zendesk. Aquí también puede encontrar ejemplos, documentación y tutoriales de vídeo para nuestros procesos. Para utilizar [Zendesk](https://adobeprimetime.zendesk.com/), tendrá que registrarse y crear una cuenta en https://tve.zendesk.com/home. No hay límite en la cantidad de usuarios que puede registrar y que pueden ver o publicar comentarios en un ticket archivado. Todas las preguntas de soporte deben dirigirse a: tve-support en adobe.com

**Contactos del equipo**:

**Asistencia** - Para todas las preguntas, incidentes o solicitudes de funcionalidades **tve-support@adobe.com**.

## 1. Reuniones de inicio {#kickoff-meetings}

El ámbito de estas reuniones es el inicio de los debates técnicos entre el Adobe y la MVPD. En este punto del proceso, la documentación debe compartirse desde ambas partes. Como seguimiento, el Adobe debe abrir un ticket en nuestro sistema de tickets (https://tve.zendesk.com/) para rastrear el estado de la integración.

## 2. Características {#features}

El Adobe configurará una llamada de estado semanal para analizar y rastrear la programación general, los pasos, el cronograma y los detalles de implementación de la integración. En esta fase, el Adobe realiza una revisión de las especificaciones de la MVPD. El resultado de esto debería ser una página de especificaciones que detalla todas las características necesarias para la MVPD. La MVPD enviará al Adobe un documento de especificación en el que se detalla la implementación de autenticación/autorización de la MVPD.

Elementos para aclarar, consulte [Funciones de integración de MVPD](/help/authentication/mvpd-integr-features.md).

Hay varias configuraciones que se deben describir en detalle en este punto:

* **URL del logotipo de MVPD** - Este es un archivo con las siguientes dimensiones: 112 x 33 píxeles. Los programadores muestran el logotipo en sus sitios cuando el usuario hace clic en el botón &quot;Iniciar sesión&quot; para seleccionar su proveedor de TV de pago.
* **Valores TTL (tiempo de vida)** - El TTL lo suele establecer la MVPD durante el proceso de autenticación/autorización. Sin embargo, el Adobe puede anular esos valores TTL y proporcionar valores diferentes según lo que acuerden el programador y la MVPD.
* **Nombre para mostrar** - Esto se muestra por los programadores en sus sitios cuando el usuario hace clic en el botón &quot;Iniciar sesión&quot; para seleccionar su proveedor de TV de pago.
* **Credenciales de prueba** : Ambos perfiles (ensayo y producción) deben tener una lista de credenciales de prueba.

>[!IMPORTANT]
>
>Cada vez que un usuario inicie un flujo de derechos, se le asociará con un único ID de usuario opaco y único.  El ID de usuario se utiliza para identificar al usuario de la aplicación de un programador, pero se origina a partir de la MVPD.

>[!CAUTION]
>
>Un aviso importante para cada MVPD: el ID de usuario NO debe contener ninguna PII (información de identificación personal), información que puede utilizarse por sí sola o con otra información para identificar, contactar o localizar al usuario.

## 2. Intercambio de metadatos {#metadata-ex}

Las dos partes deben intercambiar los metadatos de todos los entornos implicados (producción, ensayo, etc.).

* **Adobe**
   * Para el entorno de ensayo, los metadatos de SP del Adobe se pueden recuperar de: [Metadatos del sp de ensayo de autenticación](https://sp.auth-staging.adobe.com/sp/metadata)
   * Para el entorno de producción, los metadatos de SP del Adobe se pueden recuperar de: [Metadatos del sp de producción de autenticación](https://sp.auth.adobe.com/sp/metadata)

* **MVPD**
   * Para agregar metadatos (ensayo/producción).

## 4. Lista de IP permitidas {#allow-ip-list}

Las siguientes IP deben incluirse en la lista blanca del cortafuegos de las MVPD. Póngase en contacto con el Adobe para obtener la lista de direcciones IP.

* La autenticación de Primetime requiere que los servidores de seguridad se abran en los puertos 80 y 443, para permitir el acceso a recursos restringidos.

* La MVPD debe añadir una lista de direcciones IP para los servidores de autenticación y autorización (si es el caso).

## 5. Desarrollo {#deve}

La duración de la fase de desarrollo se determinará después de revisar las especificaciones, y teniendo en cuenta los puntos que ambas partes firmen. El Adobe debe escribir código personalizado para la parte de autorización.

>[!NOTE]
>
>Tenga en cuenta que la autorización se realiza por recurso. La transacción de autorización se suele realizar con una cadena de ID, pasada desde el sitio del programador, que representa el canal para el que el usuario solicita autorización. Este identificador de recurso se establece entre el programador y MVPD y puede ser tan granular como sea necesario.

## 6. Entornos de Adobe {#adobe-env}

Adobe proporciona diferentes entornos para diferentes etapas del proceso de desarrollo:

* **Precalificación** (PRE-QUAL): El entorno PRE-QUAL contiene el candidato a la próxima versión. Adobe integra inicialmente nuevos socios en este entorno, antes de actualizar la integración al entorno de lanzamiento. Los socios tienen dos semanas para probar el entorno PRE-QUAL y deben solicitar explícitamente cualquier cambio en la configuración PRE-QUAL (póngase en contacto con su representante de Adobe para obtener más detalles sobre el proceso de solicitud de cambio). Las correcciones de errores almacenan en déclencheur las nuevas implementaciones en este entorno.
* **Versión** (VERSIÓN): La versión de producción actual de Adobe se implementa en un entorno activo aquí.

Para obtener más información sobre cómo utilizar los entornos de Adobe, consulte [Explicación de los entornos de Adobe](/help/authentication/understanding-the-adobe-environments.md)

## 7. Implementación de ensayo {#stag-env}

En función de los metadatos recibidos de MVPD, Adobe creará y configurará una nueva MVPD en el sistema de autenticación de Primetime. Esto se implementará en el entorno de ensayo prequal de Adobe y se configurará con nuestro programador de pruebas (TestDistributors).

Las MVPD deben realizar la misma implementación en su entorno de control de calidad, ensayo y prueba.

## 8. Comprobación y solución de problemas {#tes-troubleshoot}

En esta fase, el Adobe y la MVPD prueban y solucionan el problema de la integración. Para probar la integración, el equipo de autenticación de Primetime puede utilizar el sitio de prueba de la API de Adobe. Para obtener más información sobre el uso del sitio de prueba de la API de Adobe, consulte [Prueba de flujos de autenticación y autorización mediante el sitio de prueba de la API de Adobe](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).

Cuando las pruebas y la solución de problemas han finalizado correctamente, la integración se activa en el entorno de ensayo de la versión de Adobe. En este punto, el Adobe puede integrar el MVPD con un programador real.

## 9. Despliegue de producción {#prod-dep}

* La MVPD debe implementarse primero en el perfil de producción para poder probar la conectividad.

* El Adobe se implementa en la producción de preigualdad.

* Ahora todas las partes pueden realizar pruebas en el perfil de producción.

* Si todo funciona correctamente en este momento, Adobe puede trasladar la integración al entorno de producción de la versión (&quot;live&quot;), que está disponible para todos los usuarios.

## 10. Procedimientos de escalación {#esc-proc}

Una vez que la integración está activa en producción, es fundamental ofrecer la mejor experiencia al cliente. Para garantizar la mejor respuesta en caso de un problema de caída del servidor, las MVPD deben proporcionar documentación sobre el procedimiento de escalación para los problemas que se señalan a la atención del Adobe.

A su vez, Adobe proporciona a las MVPD el proceso de escalación de autenticación de Primetime más actual.


<!--- [!RELATEDINFORMATION]
>
>* [Programmer Kickstart Guide](/help/authentication/programmer-kickstart-guide.md)
>* [MVPD Integration Guide](/help/authentication/mvpd-integr-features.md)
-->
