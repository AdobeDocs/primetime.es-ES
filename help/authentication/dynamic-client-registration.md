---
title: Registro de cliente dinámico
description: Registro de cliente dinámico
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---


# Registro de cliente dinámico {#dynamic-client-registration}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Contexto {#context}

Para alinearse con las prácticas de seguridad modernas, los requisitos mejorados de los propietarios de experiencia de usuario y plataforma, el SDK para Android de Adobe Primetime Authentication y el SDK para iOS se están moviendo en la dirección de adoptar [Pestañas personalizadas de Android Chrome](https://developer.chrome.com/multidevice/android/customtabs){target=_blank} and [Apple Safari view controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target=_blank}.

La implementación actual de AdobePass utiliza vistas web específicas de la plataforma, para proporcionar el entorno web para mostrar la página de inicio de sesión de MVPD. Estas vistas web no comparten la administración de credenciales con exploradores de plataforma, por lo que el usuario no puede utilizar una contraseña guardada por navegador al utilizar una aplicación de autenticación de Adobe Primetime. Además, por motivos de seguridad, algunas plataformas se están moviendo para eliminar los controladores WebView para las tareas de autenticación. Tanto Google como Apple ofrecen opciones alternativas como &quot;Chrome Custom Tabs&quot; y &quot;Safari View Controller&quot;. Básicamente son pestañas de un solo uso de sus respectivos navegadores. La autenticación de Adobe Primetime adoptará estos nuevos componentes en 2018.

## Detalles {#details}

Actualmente, existen dos maneras en las que la autenticación de Adobe Pass identifica y registra las aplicaciones:

* los clientes basados en navegador se registran mediante la lista de dominios permitidos
* los clientes de aplicaciones nativas, como las aplicaciones iOS y Android, se registran mediante el mecanismo de solicitud firmado

Para abordar los nuevos flujos para Chrome Custom Tabs &amp; Safari View Controller, Adobe Pass propone un nuevo mecanismo de registro de clientes para registrar nuevas aplicaciones. Este mecanismo permitirá un control más seguro y granular de sus aplicaciones y puede utilizarse para registrar aplicaciones en todas las plataformas.

<!--
## Related Information

- [Dynamic Client Registration API](/help/authentication/dynamic-client-registration-api.md)
- [Dynamic Client Registration Management](/help/authentication/dynamic-client-registration-management.md)
-->