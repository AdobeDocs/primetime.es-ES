---
title: Registro de aplicaciones de iOS/tvOS
description: Registro de aplicaciones de iOS/tvOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---


# Registro de aplicaciones de iOS/tvOS {#iostvos-application-registration}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Introducción {#Intro}

A partir de la versión 3.0 del SDK de AccessEnabler de iOS/tvOS, se está cambiando el mecanismo de autenticación con los servidores de Adobe. En lugar de utilizar una clave pública y un sistema secreto para firmar el requestorID, presentamos el concepto de una cadena de instrucción Software que puede utilizarse para obtener un token de acceso que se utiliza posteriormente para todas las llamadas que el SDK hace a nuestros servidores. Además de una instrucción de software, también necesitará un esquema de URL personalizado para su aplicación.

Para obtener más información, consulte [Registro de cliente dinámico](/help/authentication/dynamic-client-registration.md)

## ¿Qué es una declaración de software? {#Soft_state}

Una instrucción de software es un token de JWT que contiene información sobre su aplicación. Cada aplicación debe tener una declaración de software única que nuestros servidores utilizan para identificar la aplicación en el sistema de Adobe. La declaración de software debe pasarse cuando se inicializa el SDK de AccessEnabler y se utilizará para registrar la aplicación con Adobe. Tras el registro, el SDK recibirá un ID de cliente y un secreto de cliente que se utilizarán para obtener un token de acceso. Cualquier llamada que el SDK realice a nuestros servidores requerirá un token de acceso válido. El SDK es responsable de registrar la aplicación, obtener y actualizar el token de acceso.

**Nota:** Una instrucción de software es específica de la aplicación y no se puede usar la misma instrucción de software en más de una aplicación. Tenga en cuenta que las instrucciones de software a nivel de programador también siguen el mismo proceso, es decir, solo pueden utilizarse para una aplicación única, ya sea un solo canal o multicanal. Esta limitación también se aplica al esquema personalizado.

## ¿Cómo obtener una declaración de software? {#obtain}

### Si tiene acceso al panel de control de Televisión del Adobe:

- Abra el explorador y vaya a <https://console.auth.adobe.com>
- Vaya a `Channels` y seleccione el canal.
- Vaya a `Registered Applications` Tabulación.
- Haga clic en `Add new application`.
- Proporcione un nombre y una versión para la aplicación y seleccione las plataformas en las que estará disponible. iOS/tvOS en nuestro caso.
- Inserte los cambios en el servidor y vuelva a la pestaña Aplicaciones registradas del canal .
- Debería ver una lista con todas las aplicaciones registradas. Haga clic en el   `Download` en la aplicación que acaba de crear. Es posible que tenga que esperar unos minutos antes de que su Declaración de software esté lista para la descarga.
- Se descargará un archivo de texto. Utilice su contenido como su Declaración de software.

Para obtener más información, consulte [Administración dinámica de registros de clientes](/help/authentication/dynamic-client-registration-management.md).

### Si no tiene acceso al panel de control de Televisión del Adobe:

Enviar un ticket a <tve-support@adobe.com>. Incluya toda la información necesaria como canal, nombre de aplicación, versión y plataformas, y alguien de nuestro equipo de soporte creará una declaración de software para usted.

## ¿Cómo usar la Declaración de software? {#use}

Después de obtener su declaración de software, debe pasarla como un parámetro en el constructor Access Enabler. Se recomienda alojar la Declaración de software en una ubicación remota. De esta manera, puede revocar y cambiar fácilmente la Declaración de Software sin lanzar una nueva versión de su aplicación.

## Generación de un esquema de URL personalizado para la aplicación {#generating}

### Si tiene acceso al panel de control de Televisión del Adobe:

- Abra el explorador y vaya a <https://console.auth.adobe.com>
- Vaya a `Channels` y seleccione el canal.
- Vaya a `Custom Schemes` Tabulación.
- Haga clic en `Generate a new custom scheme`.
- Se generará un nuevo esquema personalizado para la aplicación. Ejemplo: `adbe.1JqxQsYhQOCIrwPjaooY8w://`
- Inserte los cambios en el servidor.

### Si no tiene acceso al panel de control de Televisión del Adobe:

Enviar un ticket a <tve-support@adobe.com>. Incluya el id de canal y alguien de nuestro equipo de asistencia creará un esquema personalizado para usted.

## Cómo usar el esquema personalizado {#use_custom}

En la aplicación `info.plist` añada el siguiente código:

```plist
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>adbe.u-XFXJeTSDuJiIQs0HVRAg</string> // replace this with your custom scheme
            </array>
        </dict>
    </array>
```
