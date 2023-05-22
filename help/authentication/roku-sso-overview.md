---
title: Información general de Roku SSO
description: Acerca de Roku SSO
exl-id: 77b154bc-c09f-49d4-b1af-cc33bc6dd22b
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Información general de Roku SSO {#overview}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.

## Introducción {#roku-sso-intro}

Este documento describe la información necesaria para aprovechar la capacidad Inicio de sesión único en dispositivos Roku. La autenticación de Adobe Primetime colabora con Roku para mejorar la experiencia de inicio de sesión del usuario y para facilitar el inicio de sesión único en las aplicaciones de TV Everywhere para los suscriptores de TV.

La solución se basa en la API de REST sin cliente de la autenticación Adobe Primetime, por lo que la mayoría de los programadores no necesitarán actualizar sus aplicaciones para beneficiarse del inicio de sesión único.

## Activación de Roku SSO {#enable-roku-sso}

El SSO de Roku está habilitado de forma predeterminada a menos que el programador o la solicitud de MVPD para SSO estén deshabilitados.

Cada programador puede activar o desactivar el SSO en la plataforma Roku para integraciones específicas.

### Qué debe hacer un programador para que funcione Roku SSO {#make-roku-sso-work}

Para aplicaciones de programadores que implementan la API de REST en dispositivos cliente, el SSO de Roku funcionará sin ningún cambio. Roku OS agregará dos encabezados HTTP en cualquier solicitud a los puntos finales de autenticación de Adobe Primetime.

Para las aplicaciones de los programadores que implementan una solución de servidor a servidor para la API de REST , el programador debe ponerse en contacto con el equipo de Roku y solicitar una configuración en la que estos dos encabezados se envíen a su dominio en todos los flujos de API.

Se debe utilizar el ID de suscriptor proporcionado por Roku en lugar del ID de dispositivo que la aplicación pase para garantizar el SSO entre aplicaciones (y entre dispositivos).

Para obtener detalles específicos sobre el formato de los encabezados necesarios, póngase en contacto con el representante del Adobe.

### Posibles problemas {#possible-issues}

Los programadores deben comprobar que sus implementaciones actuales basadas en la API de REST sin cliente de Adobe no impiden el inicio de sesión único de la plataforma de Roku. Consulte a continuación una lista de posibles problemas y cómo deben resolverse.

| Problema | Posible causa | Posibles soluciones | |-|-|-| |No se ha enviado ningún encabezado SSO de Roku al Adobe|Se utiliza HTTP en lugar de HTTPS para llamadas a dominios de autenticación de Adobe Primetime|Se utiliza HTTPS| |No se muestra el logotipo de MVPD / no se actualiza para los tokens SSO|La IU depende del almacenamiento local|Las aplicaciones deben actualizar la IU (y el almacenamiento local, si es necesario) después de comprobar la autenticación| |Cierre de sesión activado sin AuthZ|Diseño de aplicación|La aplicación debe actualizarse para no cerrar nunca la sesión entre bastidores|

## FAQ {#faq}

* **¿Cómo funcionará el SSO?**

   SSO funcionará en todas las aplicaciones de Programador con autenticación Adobe Primetime en todos los dispositivos Roku asociados con el mismo usuario Roku.
No todas las MVPD permitirán el SSO de Roku.

* **¿Habrá algún cambio en los TTL de autenticación?**

   El primer token de autenticación válido se utilizará para realizar el SSO y, en este caso, todas las demás aplicaciones que se autenticarán mediante SSO utilizarán el mismo TTL hasta que caduque. Por lo tanto, al navegar de una aplicación a otra, la segunda aplicación compartirá el TTL de la primera aplicación que se autentica.

* **¿Funcionarán otras funciones de Adobe como antes?**

   Toda la funcionalidad de autenticación de Primetime funcionará como antes.

* **¿Existe un proceso de inclusión/exclusión del programador que se beneficia de SSO en la plataforma Roku?**

   Este será un cambio de configuración en el Tablero de TVE de Adobe. Cada programador puede activar o desactivar el SSO en la plataforma Roku para integraciones específicas.
