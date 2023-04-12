---
title: Guía de inicio rápido del programador
description: Guía de inicio rápido del programador
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---


# Guía de inicio rápido del programador {#programmer-kickstart-guide}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Introducción {#prog-kickstart-guide-intro}

Bienvenido a la autenticación de Adobe Primetime para TV en todas partes. Esperamos con interés trabajar con usted.

>[!NOTE]
>
>Esta es la Guía Kickstart para programadores (proveedores de contenido). Si está con un Distribuidor de Programación de Vídeo Multicanal (MVPD), asegúrese de ver la [Guía de inicio rápido de MVPD](/help/authentication/mvpd-kickstart-guide.md).


Contactos de autenticación de Adobe Primetime:

* Soporte: para todas las preguntas, incidentes o solicitudes de características, `tve-support@adobe.com`
* Se asignará a su proyecto un contacto de habilitación antes del inicio del proyecto.

La siguiente información describe algunos primeros pasos importantes para llevarnos a un inicio sólido y eficiente. El objetivo es ofrecer una explicación y expectativas sobre cómo trabajaremos con los socios para lograr integraciones. Tenga en cuenta que las secciones &quot;proporcionará&quot; / &quot;El Adobe proporcionará&quot; a continuación para cada artículo. Se enumeran mediante una lista de comprobación o una guía a medida que trabajamos en el proyecto.

Este documento supone que los programadores están registrados para trabajar con un socio MVPD elegido.

## Programación de la versión {#release-schedule}

El ciclo de desarrollo de la velocidad de Adobe está planificado para que pueda ver cuándo se programan nuestras versiones y cómo se promociona cada versión a través de nuestro sistema de desarrollo.

Después de completar cada sprint, está disponible para QE, o para ver nuevas implementaciones en nuestro servidor UAT.

Aproximadamente cada 6 semanas se realizará una versión en el servidor de Adobe Pre-Qualification. (Este es el servidor donde realizamos nuestra próxima versión propuesta mientras realizamos el QE final). Estas compilaciones incluirán todo el trabajo completado en sprints desde la última caída. En este momento, hay disponible un período de garantía de dos semanas para que los socios prueben esta versión.

Suponiendo que no surgieran problemas críticos durante las dos semanas anteriores a la ventana de prueba, la versión se promocionará a la producción en directo. Esto significa que la integración estará disponible en el entorno de la versión de Adobe, pero los socios eligen cuándo hacen pública la versión.

<!--For the latest release schedule information, see the Release Calendar.-->

## Documentación de soporte {#supp-doc}

El Adobe proporcionará:

* Guía de implementación: **`https://tve.zendesk.com/entries/498741-tve-deployment-guide`**
* Acceso a nuestro sistema de asistencia al cliente de Zendesk. Aquí también puede encontrar ejemplos, información y tutoriales en vídeo sobre algunos de los procesos. Para acceder a este documento en Zendesk, junto con otros documentos publicados allí, deberá registrarse y crear una cuenta en `https://tve.zendesk.com/home`. No hay límite en la cantidad de usuarios que puede registrar.  Puedes ver y compartir comentarios en cualquier ticket archivado. Todas las preguntas de asistencia deben dirigirse a `tve-support@adobe.com`.
* [Guía de integración del programador](/help/authentication/programmer-integration-guide-overview.md)
* Biblioteca de verificador de tokens de medios: `https://tve.zendesk.com/entries/471323-media-token-validator-library`.

## Configuración del entorno de prueba {#test-env-setup}

Adobe lo configurará primero con el sitio de prueba de Adobe, donde el Adobe actúa como MVPD para fines de prueba. A continuación, su equipo puede configurar un sitio web de prueba que llame a la API de Adobe. Utilice el selector MVPD predeterminado y seleccione &quot;Adobe&quot; como idP.

Proporcionará:

1. ID del solicitante. Es una cadena que identifica de forma exclusiva la marca del sitio web o la aplicación que realiza solicitudes de autenticación de Adobe Primetime. La cadena en sí es arbitraria pero necesita ser acordada entre Adobe y el Programador
1. Información del canal. Se trata de un conjunto de cadenas que identifica los canales de contenido que solicita el ID del solicitante. En muchos casos, el canal y el ID del solicitante son los mismos. Sin embargo, es posible que tenga varios canales de contenido que se puedan solicitar con el mismo ID. Las cadenas de nombre de canal deben corresponder a los canales de televisión por cable. Algunos MVPD validarán este valor a través del protocolo AuthN y/o AuthZ.
1. Nombres de dominio (para permitir ese ID de solicitante). Será una lista de nombres de dominio reales que se enumerarán por Adobe para aceptar el ID del solicitante. Esto garantiza que solo los dominios aprobados tengan acceso a la autenticación de Adobe Primetime con sus metadatos. NOTA: los nombres de dominio válidos para la producción pueden ser diferentes para la prueba/ensayo y ambos deben proporcionarse e identificarse.

Adobe configurará la cuenta y el Adobe proporcionará:

* Inicio de sesión y contraseña para acceder al sitio de prueba

## Configuración con MVPD {#setup-mvpd}

En esta sección se describe lo que necesita cuando migre del sitio de prueba de Adobe para trabajar con un MVPD.

Proporcionará (a través de MVPD):

* **Dos conjuntos de credenciales**:
   * AuthN + AuthZ : inicio de sesión/contraseña de un usuario autenticado y autorizado
   * AuthN + NonAuthZ : inicio de sesión/contraseña para un usuario autenticado pero no autorizado
* **ID de recurso**. Se trata de un identificador de contenido específico que se validará con un MVPD a través del protocolo AuthZ. Puede tratarse de canales, programas, episodios o recursos; debe acordarse con su MVPD.

La autenticación de Adobe Primetime admite un esquema de metadatos basado en MRSS, lo que significa que los ID de recurso pueden ser tan específicos como sea necesario y pueden incluir identificadores que pueden ser exclusivos de un MVPD específico.

**NUEVA integración MVPD**: Es importante recordar que su MVPD elegido juega un papel integral en la finalización de cualquier integración. El Adobe necesita escribir código para cada MVPD según sus especificaciones. Hasta que estos pasos estén completos, no podrá seleccionar ese MVPD en el cuadro de diálogo ni completar las pruebas de producto. Adobe debe programar este trabajo con antelación para que se ajuste al siguiente sprint disponible. (Para obtener información sobre la programación actual, consulte el Calendario de versiones).

**Integraciones existentes de MVPD**: Si su MVPD elegido ya está configurado con Adobe, los pasos de conectividad deberían ser mucho más simples (más rápidos) y, a menudo, la conectividad se puede lograr mediante cambios de configuración.

>[!NOTE]
>
>El MVPD TODAVÍA tendrá que habilitar al Programador, y firmar cualquier acuerdo comercial relevante.

**QE con MVPD**: Todas las integraciones implicarán una FC conjunta, y dado que el usuario final es, en última instancia, cliente de la MVPD, muchos han establecido ciclos de prueba antes de impulsar &quot;live&quot;. Dado que esto implica la programación de los recursos de MVPD, esta es una área potencial para el retraso.

<!--
>[RELATEDINFORMATION]
>[MVPD Kickstart Guide](help\authentication\mvpd-kickstart-guide.md)
-->

