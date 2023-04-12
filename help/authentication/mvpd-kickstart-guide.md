---
title: Plan de integración directa de MVPD
description: Plan de integración directa de MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---


# Guía de inicio rápido de MVPD: Plan de integración directa de MVPD {#mvpd-dir-int-plan}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Introducción {#mvpd-kickstart-intro}

Bienvenido a la autenticación de Adobe Primetime para TV en todas partes.  Esperamos con interés trabajar con usted.

>[!NOTE]
>
>Esta es la Guía Kickstart para distribuidores de programación de vídeo multicanal (MVPD). Si es programador (proveedor de contenido), consulte la [Guía de inicio rápido para programadores](/help/authentication/programmer-kickstart-guide.md).

La asistencia está disponible en todo momento a través del sistema de tickets de autenticación Primetime en Zendesk. Aquí también puede encontrar ejemplos, documentación y tutoriales en vídeo para nuestros procesos. Para usar [Zendesk](https://adobeprimetime.zendesk.com/), deberá registrarse y crear una cuenta en https://tve.zendesk.com/home. No hay límite en la cantidad de usuarios que puede registrar y que pueden ver o publicar comentarios en un ticket archivado. Todas las preguntas de asistencia deben dirigirse a: tve-support en adobe.com

**Contactos del equipo**:

**Asistencia** - Para todas las preguntas, incidentes o solicitudes de características **tve-support@adobe.com**.

## 1. Reuniones iniciales {#kickoff-meetings}

El ámbito de estas reuniones es el inicio de debates técnicos entre el Adobe y el MVPD. En este punto del proceso, la documentación debe compartirse entre ambas partes. Como continuación, Adobe debe abrir un ticket en nuestro sistema de tickets (https://tve.zendesk.com/) para realizar un seguimiento del estado de la integración.

## 2. Características {#features}

Adobe configurará una llamada de estado semanal para analizar y realizar un seguimiento de la programación general, los pasos, la cronología y los detalles de implementación de la integración. En esta fase, el Adobe realiza una revisión de las especificaciones del MVPD. El resultado de esto debería ser una página de especificaciones que detalle todas las características necesarias para el MVPD. El MVPD enviará al Adobe un documento de especificación, en el que se detallará la implementación de autenticación/autorización del MVPD.

Elementos para aclarar, consulte [Funciones de integración de MVPD](/help/authentication/mvpd-integr-features.md).

Hay varias configuraciones que deberán describirse en detalle en este punto:

* **URL del logotipo de MVPD** - Este es un archivo con las siguientes dimensiones: 112 x 33 píxeles. El logotipo lo muestran los programadores en sus sitios cuando el usuario hace clic en el botón &quot;Iniciar sesión&quot; para seleccionar su proveedor de televisión de pago.
* **Valores TTL (tiempo de vida)** - El TTL suele ser configurado por el MVPD durante el proceso de autenticación/autorización. Sin embargo, el Adobe puede anular esos valores TTL y proporcionar valores diferentes según lo acordado por el Programador y el MVPD.
* **Nombre para mostrar** - Esto lo muestran los programadores en sus sitios cuando el usuario hace clic en el botón &quot;Iniciar sesión&quot; para seleccionar su proveedor de televisión de pago.
* **Credenciales de prueba** - Ambos perfiles (ensayo y producción) deben tener una lista de credenciales de prueba.

>[!IMPORTANT]
>
>Cada vez que un usuario inicie un flujo de derechos, se asociará con un ID de usuario único, opaco y único.  El ID de usuario se utiliza para identificar el usuario de la aplicación de un programador, pero se origina en el MVPD.

>[!CAUTION]
>
>Un aviso importante para cada MVPD: el ID de usuario NO debe contener ningún PII (información de identificación personal), información que se pueda usar por sí sola o con otra información para identificar al usuario, ponerse en contacto con él o localizarlo.

## 2. Intercambio de metadatos {#metadata-ex}

Las dos partes deben intercambiar los metadatos para todos los entornos implicados (producción, ensayo, etc.).

* **Adobe**
   * Para el entorno de ensayo, los metadatos de SP del Adobe de ensayo se pueden recuperar desde: [Metadatos del sp de ensayo de autenticación](https://sp.auth-staging.adobe.com/sp/metadata)
   * Para el entorno de producción, los metadatos del SP del Adobe se pueden recuperar desde: [Metadatos del sp de producción de autenticación](https://sp.auth.adobe.com/sp/metadata)

* **MVPD**
   * Para añadir metadatos (ensayo/producción).

## 4. Permitir lista de IP {#allow-ip-list}

Las siguientes IP deben incluirse en la lista blanca del cortafuegos de MVPD. Póngase en contacto con Adobe para obtener la lista de IP.

* La autenticación de Primetime requiere que los cortafuegos se abran en los puertos 80 y 443, para permitir el acceso a recursos restringidos.

* El MVPD necesita añadir una lista de direcciones IP para los servidores de autenticación y autorización (si este es el caso).

## 5. Desarrollo {#deve}

La duración de la fase de desarrollo se determinará después de examinar las especificaciones y teniendo en cuenta los temas que ambas partes firman. Adobe debe escribir código personalizado para la parte de autorización.

>[!NOTE]
>
>Tenga en cuenta que la autorización se realiza por recurso. La transacción de autorización se realiza generalmente con una cadena de ID, que se pasa desde el sitio del programador y representa el canal para el cual el usuario solicita la autorización. Este ID de recurso se establece entre el programador y MVPD y puede ser tan granular como sea necesario.

## 6. Entornos de Adobe {#adobe-env}

Adobe proporciona diferentes entornos para diferentes etapas del proceso de desarrollo:

* **Precalificación** (PRE-QUAL): El entorno PRE-QUAL contiene el candidato de la próxima versión. Adobe integra inicialmente nuevos socios en este entorno, antes de actualizar la integración al entorno de versiones. Los socios tienen dos semanas para probar el entorno PRE-QUAL y deben solicitar explícitamente cualquier cambio en la configuración PRE-QUAL (póngase en contacto con su representante de Adobe para obtener más información sobre el proceso de solicitud de cambio). Los errores corrigen el déclencheur de nuevas implementaciones en este entorno.
* **Versión** (VERSIÓN): La versión de producción actual de Adobe se implementa en un entorno en vivo aquí.

Para obtener más información sobre cómo utilizar los entornos de Adobe, consulte [Explicación de los entornos de Adobe](/help/authentication/understanding-the-adobe-environments.md)

## 7. Implementación de ensayo {#stag-env}

En función de los metadatos recibidos de la MVPD, Adobe creará y configurará una nueva MVPD en el sistema de autenticación de Primetime. Esto se implementará en el entorno de ensayo de preigualdad de Adobe y se configurará con nuestro programador de pruebas (TestDistributors).

El MVPD debe hacer la misma implementación en su entorno de control de calidad, ensayo y prueba.

## 8. Probar y solucionar problemas {#tes-troubleshoot}

En esta fase, el Adobe y la prueba MVPD y la resolución de problemas de la integración. Para ayudar a probar la integración, el equipo de autenticación de Primetime puede utilizar el sitio de prueba de la API de Adobe. Para obtener más información sobre el uso del sitio de prueba de la API de Adobe, consulte [Comprobación de la autenticación y los flujos de autorización mediante el sitio de prueba de la API de Adobe](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).

Cuando las pruebas y la solución de problemas han finalizado correctamente, la integración se activa en el entorno de ensayo de versiones de Adobe. En este punto, Adobe puede integrar el MVPD con un programador real.

## 9. Implementación de producción {#prod-dep}

* El MVPD debe implementarse primero en el perfil de producción para poder probar la conectividad.

* El Adobe se implementa en la producción precualificada.

* Ahora todas las partes pueden realizar pruebas en el perfil de producción.

* Si todo está bien en este punto, Adobe puede mover la integración al entorno de producción de versiones (&quot;activo&quot;), que está disponible para todos los usuarios.

## 10. Procedimientos de escalada {#esc-proc}

Una vez que la integración está activa en producción, es fundamental proporcionar la mejor experiencia al cliente. Para garantizar la mejor respuesta en el caso de un problema de servidor inactivo, los MVPD deben proporcionar documentación sobre el procedimiento de escalación para los problemas que se señalen a la atención del Adobe.

A su vez, Adobe proporciona MVPD con el proceso de escalación de autenticación de Primetime más actual.


<!--- [!RELATEDINFORMATION]
>
>* [Programmer Kickstart Guide](/help/authentication/programmer-kickstart-guide.md)
>* [MVPD Integration Guide](/help/authentication/mvpd-integr-features.md)
-->
