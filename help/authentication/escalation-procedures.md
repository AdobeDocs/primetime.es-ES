---
title: Procedimientos de escalación
description: Procedimientos de escalación
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---

# Procedimientos de escalación {#escalation-procedures}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

>[!IMPORTANT]
> 
>Llame a la línea directa : **+1-205-693-9813** y enviar un correo electrónico a **tve-support@adobe.com** incluido **URGENTE: INCIDENTE** en la línea de asunto.

## Introducción {#introduction}

En este documento se describen los procedimientos de apoyo para incidentes graves (**GRAVEDAD 1** ) que afectan a la autenticación de Adobe Primetime, a la supervisión de la concurrencia de Primetime y a sus socios.\
 

## Definición de un incidente de nivel 1 de GRAVEDAD {#definition-of-a-severity-1-level-incident}

A **GRAVEDAD 1** el incidente de nivel es **LIVE** situación, **en el entorno de producción**, que no permite completar los flujos de autenticación y/o autorización para un canal y un MVPD, lo que afecta a un gran número de suscriptores del MVPD que realizan el flujo.


## Ejemplos de incidentes de GRAVEDAD 1 {#examples-of-severity-1-incidentcs}

* El activador de acceso de producción alojado en  `https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js` (o `https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js`) no está disponible.

* Para un MVPD específico, el Adobe ya no redirige/muestra la página de inicio de sesión, después de que el usuario seleccione el MVPD (en cualquiera de los navegadores compatibles).

* El socio recibe un gran número de informes que los usuarios no pueden autenticar ni autorizar con un MVPD específico.

* Durante el proceso de autenticación, el usuario se atasca en una página de error de Adobe sin la posibilidad de reiniciar el flujo de autenticación/autorización.


| Ejemplos de lo que es **NOT** a Incidente de gravedad 1 |
|---|
| Para problemas de este tipo, el Adobe proporcionará apoyo para las investigaciones, pero no son incidentes de Gravedad 1:<ul><li>Uno o varios suscriptores no pueden realizar el flujo debido a un problema de versión de Flash (falta Flash, bloqueadores de Flashes, versión de Flash incorrecta).</li><li>Uno o varios suscriptores no pueden autenticarse y permanecer en la página de inicio de sesión de MVPD.</li><li>Uno o varios suscriptores están autenticados pero no pueden reproducir videos.</li><li>Uno o varios suscriptores/todos encuentran un error de JavaScript en el sitio del programador</li></ul> |

## Flujos de escalación de gravedad 1 {#severity-1-escalation-flows}

Los incidentes de gravedad 1 pueden iniciarlos un Adobe o un socio de autenticación de Adobe Primetime. A continuación se presentan los pasos de cada uno.

### Flujo iniciado por el socio {#partner-initiated-flow}

1. El socio identifica un incidente de Gravedad 1 (como se describió anteriormente) que requiere atención inmediata del Adobe.
1. El socio envía un correo electrónico a **tve-support@adobe.com** incluido **URGENTE: INCIDENTE** en la línea de asunto y añadiendo la siguiente información:
   * Título
   * Descripción y pasos para reproducir
   * Sistema operativo/Explorador
   * SDK y versión
   * Dispositivos afectados
   * % de usuarios afectados
   * Seguimiento HTTP o registros de dispositivo que muestran el problema
   * (opcional) Cualquier captura de pantalla o vídeo disponible que demuestre el problema
1. Si el Adobe no responde al ticket en 30 minutos, el socio llama al siguiente número:
   **1-205-693-9813**

   >[!IMPORTANT]
   >Si no incluye &quot;URGENT-INCIDENT&quot; en el título del ticket, no será recogido por nuestro sistema de notificación**.

### Flujo iniciado por el Adobe {#adobe-initiated-flow}

#### ...para un problema de autenticación de Adobe Primetime {#adobe-initiated-flow-authn-issue}

1. Adobe identifica un problema interno y abre un ticket con nuestro sistema de seguimiento.

1. Adobe notifica al administrador del programa del socio y al contacto técnico, especificando el número de incidencia y el impacto estimado del problema.

1. El Adobe trabaja para resolver el incidente y mantiene informados a todos los asociados afectados.

#### ...para un problema de socio (programador/MVPD) {#adobe-initiated-flow-partner-issue}

1. Adobe identifica un problema relacionado con la integración con un MVPD o en uno de los sitios del programador.

1. El Adobe notifica al socio afectado <u>siguiendo los procedimientos de apoyo establecidos con dicho socio</u> y abre un ticket con la organización de asistencia del socio.

1. Si, durante el análisis de impacto, el Adobe identifica que el problema pertenece a una de las decisiones previamente acordadas sobre escenarios de incidentes, consulte **Decisiones previamente acordadas sobre escenarios de incidentes**, actuará en consecuencia sin esperar a la entrada del socio.

1. Adobe esperará a que el socio actualice las actualizaciones y a que se le notifique cuando se haya restaurado el servicio.

## Decisiones previamente acordadas sobre escenarios de incidentes {#pre-agreed-descn}

Hay algunas situaciones en las que se realizará una acción predeterminada en el caso de que ocurra ese escenario:

|  | Situación | Descripción | Acciones |
|---|---|---|---|
| S1 | Adobe identifica un problema con la integración de un MVPD durante las operaciones normales de producción. | Durante las operaciones normales de producción, el Adobe identifica un problema con uno de los MVPD que hace imposible la realización de los flujos de autenticación/autorización (por ejemplo, certificados caducados, respuestas SAML caducadas, puertos cerrados, parámetros modificados, etc.) | - Adobe notificará al MVPD y a los programadores afectados.  </br> </br> - Adobe desactivará este MVPD para todos los programadores afectados. </br> </br> - El Adobe abrirá un ticket con el MVPD siguiendo el procedimiento de soporte acordado con ese MVPD |
| S2 | Adobe activa un nuevo MVPD para un Programador y el Programador permite el MVPD antes de la fecha de lanzamiento. | Adobe está activando un nuevo MVPD para un sitio de programadores, y el sitio está mostrando el nuevo MVPD en el selector, aunque no se suponía que lo hiciera. | - Adobe notificará al programador sobre el nuevo MVPD que aparece en el selector antes de la fecha programada. </br> </br>  - El programador tomará medidas para eliminarlo del selector si es necesario. |
| S3 | Adobe activa un nuevo MVPD para un programador incluso si el MVPD no está listo para entrar en producción | Adobe está activando un nuevo MVPD para un programador, pero el MVPD aún no ha implementado el soporte para la integración, por lo que los flujos de autenticación/autorización no se pueden realizar | - Adobe realizará la implementación solo si el programador lo solicita </br> </br> - El programador será responsable de garantizar el permiso del MVPD una vez que se hayan realizado todas las pruebas. |

## Expectativas De Respuesta Para Incidentes De Gravedad 1 {#response-expectations-for-severity-one-incidents}

* Respuesta inicial: 30 minutos (24/7)
* Plan de acción: 1 hora (24/7)
* Resolución: ASAP (24/7)
