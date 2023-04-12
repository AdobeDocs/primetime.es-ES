---
title: Información general de Roku SSO
description: Acerca de Roku SSO
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---


# Información general de Roku SSO {#overview}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Introducción {#roku-sso-intro}

Este documento describe la información necesaria para aprovechar la capacidad de inicio de sesión único en los dispositivos Roku. La autenticación de Adobe Primetime colabora con Roku para mejorar la experiencia del usuario con el inicio de sesión y para facilitar el inicio de sesión único en todas las aplicaciones de TV en todas partes para suscriptores de TV.

La solución se basa en la API de REST sin clientes de la autenticación de Adobe Primetime, por lo que la mayoría de los programadores no necesitan actualizar sus aplicaciones para beneficiarse del inicio de sesión único.

## Habilitación de Roku SSO {#enable-roku-sso}

Roku SSO está habilitado de forma predeterminada a menos que el programador o MVPD solicite que SSO esté deshabilitado.

Cada programador puede activar o desactivar SSO en la plataforma Roku para integraciones específicas.

### Qué debe hacer un programador para que funcione Roku SSO {#make-roku-sso-work}

Para las aplicaciones de programadores que implementan la API de REST en dispositivos cliente, el SSO de Roku funcionará sin ningún cambio. El sistema operativo Roku agregará dos encabezados HTTP en cualquier solicitud a los puntos finales de autenticación de Adobe Primetime.

Para las aplicaciones de programadores que implementen una solución de Servidor a Servidor para la api de REST , el programador debe ponerse en contacto con el equipo de Roku y solicitar una configuración en la que estos dos encabezados se envíen a su dominio en todos los flujos de api.

Se utilizará el ID de suscriptor proporcionado por Roku en lugar del ID de dispositivo que pase la aplicación para garantizar el SSO entre aplicaciones (y entre dispositivos).

Para obtener detalles específicos sobre el formato de los encabezados necesarios, póngase en contacto con su representante de Adobe.

### Posibles problemas {#possible-issues}

Los programadores deben comprobar que sus implementaciones actuales basadas en la API de REST sin clientes de Adobe no impiden el SSO de la plataforma de Roku. Consulte a continuación una lista de posibles problemas y cómo deben resolverse.

| Problema | Causa posible | Posibles soluciones | |-|-|-| |No se ha enviado ningún encabezado SSO de Roku a Adobe|Uso de HTTP en lugar de HTTPS para llamadas a dominios de autenticación de Adobe Primetime|Uso de HTTPS| |El logotipo de MVPD no se muestra/no se actualiza para los tokens de SSO|La interfaz de usuario depende del almacenamiento local|Las aplicaciones deben actualizar la interfaz de usuario (y el almacenamiento local, si es necesario) después de comprobar la autenticación| |Cierre de sesión activado sin AuthZ|Diseño de aplicación|La aplicación debe actualizarse para que nunca se cierre la sesión entre bastidores|

## Preguntas frecuentes {#faq}

* **¿Cómo funcionará el SSO?**

   SSO funcionará en todas las aplicaciones de programador con autenticación de Adobe Primetime en todos los dispositivos Roku asociados al mismo usuario de Roku.
No todos los MVPD permitirán Roku SSO.

* **¿Habrá algún cambio en los TTL de autenticación?**

   El primer token de autenticación válido se utilizará para realizar SSO y, en este caso, todas las demás aplicaciones que se autenticarán mediante SSO utilizarán el mismo TTL hasta que caduque. Por lo tanto, cuando se navega de una aplicación a otra, la segunda aplicación comparte el TTL de la primera aplicación que se autentica.

* **¿Funcionará otra funcionalidad de Adobe como antes?**

   Toda la funcionalidad de autenticación de Primetime funcionará como antes.

* **¿Existe un proceso de inclusión/exclusión de programadores que se beneficie de SSO en la plataforma Roku?**

   Este será un cambio de configuración en el TVE Dashboard de Adobe. Cada programador puede activar o desactivar SSO en la plataforma Roku para integraciones específicas.
