---
title: Compatibilidad con inicio de sesión único
description: Compatibilidad con inicio de sesión único
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 0%

---


# Compatibilidad con inicio de sesión único

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Información general {#overview-sso-support}

En este documento se describen los tipos de inicio de sesión único admitidos y potenciados por la autenticación de Adobe Primetime en distintas plataformas. El objetivo de este documento es arrojar luz sobre lo que se admite y lo que no, cuál es la cobertura de MVPD para cada método SSO y qué se requiere de los programadores para poder beneficiarse de SSO en cada plataforma.

Después de que un usuario inicia sesión con sus credenciales de MVPD, la autenticación de Adobe Primetime genera un token seguro que representa la sesión de autenticación de MVPD y vincula dicho token al dispositivo del usuario mediante un ID de dispositivo. La autenticación de Adobe Primetime almacena el token/ID del dispositivo en un servidor o en el dispositivo. Esto permite a los usuarios introducir sus credenciales con menos frecuencia y mantener las transacciones seguras.

>[!NOTE]
>
>Los flujos de trabajo SSO forman parte del paquete Premium Workflow. Póngase en contacto con su representante de ventas de Primetime si le interesa utilizar esta funcionalidad.

## Estado actual de SSO en varias plataformas {#current-sso-status-platforms}

| Plataforma/dispositivo | Compatibilidad con SSO | Tipo SSO | Cobertura de MVPD | Notas |
|:-------------------:|:-----------:|:---------------------------------------:|-----------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| Web (JavaScript) | Sí | Token de autenticación compartida (SSO de Adobe) | Todo | Sin SSO entre navegadores Siga las instrucciones de la Guía de integración de programadores para JavaScript. Tras seguir las instrucciones, SSO está habilitado de forma predeterminada.  Al habilitar la autenticación por solicitante, se rompe el SSO |
| iOS | Sí | SSO de plataforma: intercambio de tokens | Según la compatibilidad con Apple, la lista está aquí | A partir de iOS 10, Apple &amp; Adobe introdujo la funcionalidad SSO para los programadores y MVPD participantes. Al utilizar el SDK de iOS de Adobe más reciente o al utilizar la API de REST sin clientes de Adobe e implementar la funcionalidad de SSO de Apple, puede beneficiarse del SSO en dispositivos iOS. Más información sobre la implementación del SDK aquí y más detalles sobre la implementación sin cliente aquí. Notas adicionales: - Si no desea utilizar Apple SSO, puede seguir teniendo un SSO limitado entre aplicaciones del mismo proveedor (mismo ID de paquete) que puedan compartir almacenamiento y un ID (IDFV), por lo que SSO se limita solo a las aplicaciones del mismo proveedor. |
| Android | Sí | Token de autenticación compartida (SSO de Adobe) | Todo | Si el usuario no acepta la solicitud de permiso WRITE_EXTERNAL_STORAGE, la biblioteca utilizará un almacenamiento en entornos limitados local. La implicancia en este caso es que no habrá SSO entre distintas aplicaciones al utilizar el almacenamiento local. |
| tvOS: nuevo Apple TV | Sí | SSO de plataforma: intercambio de tokens | Según la compatibilidad con Apple, la lista está aquí | Desde tvOS 10, Apple &amp; Adobe introdujo la funcionalidad SSO para los programadores participantes y los MVPD. Al utilizar el SDK de tvOS de Adobe más reciente o al utilizar la API de REST sin clientes de Adobe e implementar la funcionalidad SSO de Apple, puede beneficiarse del SSO en dispositivos tvOS. Más información sobre el SDK de tvOS: aquí y aquí y más detalles sobre la implementación sin clientes aquí. |
| Roku | Sí | Token de autenticación compartida (SSO de Adobe) | Próximamente se proporcionará una lista completa de cobertura significativa. | Roku SSO funciona de forma predeterminada con la API sin cliente para todos los clientes que respetan las directrices Roku, no se requiere una implementación especial. SSO se basa en la información de identificación del dispositivo que Roku envía de forma segura al Adobe. |
| Amazon FireTV | Sí | Token de autenticación compartida (SSO de Adobe) | Próximamente se proporcionará una lista completa de cobertura significativa. | El SDK de FireTV es compatible con el inicio de sesión único basado en las capacidades de Android. El SSO en esta plataforma solo es posible entre aplicaciones que utilicen el SDK de Adobe FireTV por ahora. Más información sobre el nuevo SDK de FireTV aquí. Las aplicaciones de FireTV implementadas sobre la API sin cliente podrán beneficiarse de SSO para el año 2018. |
| Xbox 360 | No |  |  | No hay ningún ID de dispositivo que podamos aprovechar. Hay un ID de aplicación, por lo que los usuarios no tienen que autenticarse cada vez. |
| Xbox One | No |  |  | No hay ningún ID de dispositivo que podamos aprovechar. Hay un ID de aplicación, por lo que los usuarios no tienen que autenticarse cada vez. |
| Windows 8/10 | No |  |  | No hay ningún ID de dispositivo que podamos aprovechar. Hay un ID de aplicación, por lo que los usuarios no tienen que autenticarse cada vez. |
| Televisores Samsung | No |  |  | No hay ningún ID de dispositivo que podamos aprovechar. Hay un ID de aplicación, por lo que los usuarios no tienen que autenticarse cada vez. |

### Notas sobre Xbox 360 y Xbox One {#notes-xbox-360}

* **Xbox 360**- Xbox 360 depende del servicio Live para proporcionar el token que incorpora el deviceID. El servicio activo se coloca en el valor appID para deviceID, por lo que solo se abarca en la aplicación. Para Xbox 360, Microsoft proporcionó a Adobe una biblioteca Java para ayudarle a analizar el token.

* **Xbox One**- Se emitirá un token web JSON cifrado con el certificado o la clave del editor y firmado por Microsoft. El Adobe extrae el deviceID de un parámetro llamado DPI (Device Partner ID), distinto del PDID del parámetro Xbox 360 (Partner Device ID). El PDID también existe en Xbox One, pero está pensado para ser reemplazado por este nuevo parámetro &quot;Device Pairwise ID&quot; (DPI).


### Desactivación de SSO {#disable-sso}

En determinadas situaciones, algunas aplicaciones o sitios querrán deshabilitar el SSO para satisfacer casos comerciales avanzados.

* **Para JS y SDK nativos** - El equipo de soporte de autenticación de Primetime puede deshabilitar SSO para un par de ID de solicitante/MVPD. No es necesario trabajar en sitios o en aplicaciones nativas.  Una vez que el equipo de soporte de autenticación de Primetime desactive el SSO, las autenticaciones realizadas con el par RequestorId/MVPD especificado no se compartirán con sitios o aplicaciones que utilicen ID de solicitante diferentes. Además, las autenticaciones existentes con diferentes ID de solicitante no serán válidas para la combinación ID de solicitante/MVPD en la que SSO estaba deshabilitado. Técnicamente, la desactivación de SSO se realiza enlazando el token AuthN a la combinación específica ID del solicitante/MVPD.
* **Para la API sin cliente** - Puede deshabilitar SSO en el flujo de autenticación sin clientes especificando un parámetro appId no vacío en las llamadas REST. Puede utilizar cualquier cadena como valor, siempre que esa cadena sea única para el ID del solicitante. Tenga en cuenta que para la API sin cliente, el programador/implementador debe cambiar el sitio o la aplicación para agregar este parámetro específico del solicitante.

>[!IMPORTANT]
>
>NOTA IMPORTANTE PARA EL SSO DE API SIN CLIENTE: Algunos MVPD requieren que cada red (ID del solicitante) realice su propio flujo de autenticación. Para los flujos basados en SDK (iOS, etc.), el SDK la gestiona automáticamente. Sin embargo, para las API sin cliente esto debe ser gestionado por el programador. Recomendamos encarecidamente a los programadores que no habiliten flujos SSO para API sin cliente en este momento y que utilicen una combinación de ID de dispositivo e ID de aplicación para ID de dispositivo. Adobe también trabajará para mejorar los flujos de API sin cliente para que se pueda establecer un SSO adecuado.

### Cerrar sesión {#logout-sso-support}

Los programadores deben tener en cuenta que la acción &quot;Cerrar sesión&quot; en el contexto del inicio de sesión único, cuando se realiza en una aplicación o en un sitio, eliminará todos los tokens del dispositivo y que el usuario cerrará la sesión en todas las aplicaciones o sitios.

Si se cumplen las condiciones de SSO (independientemente de si SSO está habilitado o deshabilitado), el cierre de sesión se realizará y se eliminará toda la información de autenticación y autorización.
