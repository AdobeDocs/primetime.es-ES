---
title: Registro de la aplicación Amazon FireOS
description: Registro de la aplicación Amazon FireOS
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# Registro de la aplicación Amazon FireOS {#amazon-fireos-application-registration}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>

## Introducción {#intro}

A partir de la versión 3.0 del SDK de FireOS AccessEnabler, estamos cambiando el mecanismo de autenticación con los servidores de Adobe. En lugar de utilizar una clave pública y un sistema secreto para firmar el requestorID, presentamos el concepto de una cadena de declaración de software que se puede utilizar para obtener un token de acceso que se utiliza posteriormente para todas las llamadas que el SDK hace a nuestros servidores. Además de una Declaración de software, también deberá crear un vínculo profundo para su aplicación.

Más información, consulte [Registro de cliente dinámico](/help/authentication/dynamic-client-registration.md)

## ¿Qué es una declaración de software? {#what}

Una instrucción de software es un token de JWT que contiene información sobre su aplicación. Cada aplicación debe tener una Declaración de Software única que nuestros servidores utilizan para identificar la aplicación en el sistema de Adobe. La declaración de software debe pasarse cuando se inicializa el SDK de AccessEnabler y se utilizará para registrar la aplicación con Adobe. Tras el registro, el SDK recibirá un ID de cliente y un secreto de cliente que se utilizarán para obtener un token de acceso. Cualquier llamada que el SDK realice a nuestros servidores requerirá un token de acceso válido. El SDK es responsable de registrar la aplicación, obtener y actualizar el token de acceso.

**Nota:** Las declaraciones de software son específicas de la aplicación y una declaración de software individual no se puede usar en más de una aplicación. Tenga en cuenta que esto también se aplica a las aplicaciones que ofrecen acceso a varios canales.

## ¿Cómo obtener una declaración de software? {#how-to}

### Si tiene acceso al panel de control de Televisión del Adobe:

- Abra el explorador y vaya a <https://console.auth.adobe.com>
- Vaya a `Channels` y seleccione el canal.
- Vaya a `Registered Applications` Tabulación.
- Haga clic en `Add new application`.
- Proporcione un nombre y una versión para su aplicación y seleccione las plataformas en las que estará disponible (por ejemplo, Android en nuestro caso).
- Proporcione un nombre de dominio eligiendo entre una lista de dominios ya configurados para el programador.
- Inserte los cambios en el servidor y vuelva a la pestaña Aplicaciones registradas del canal .
- Debería ver una lista con todas las aplicaciones registradas. Haga clic en el `Download` en la aplicación que acaba de crear. Nota: Es posible que tenga que esperar unos minutos antes de que su Declaración de software esté lista para la descarga.
- Se descargará un archivo de texto. Utilice su contenido como su Declaración de software.

Más información, consulte [Administración dinámica de registros de clientes](/help/authentication/dynamic-client-registration-management.md)

### Si no tiene acceso al panel de control de Televisión del Adobe:

Enviar un ticket a <tve-support@adobe.com>. Incluya toda la información necesaria, incluyendo canal, nombre de aplicación, versión y plataformas, y alguien de nuestro equipo de soporte creará una declaración de software para usted.

## ¿Cómo usar la Declaración de software? {#use}

Después de obtener su declaración de software, debe pasarla como un parámetro en el constructor Access Enabler. Se recomienda alojar la Declaración de software en una ubicación remota. De esta manera, puede revocar y cambiar fácilmente la Declaración de Software sin lanzar una nueva versión de su aplicación.

## Cómo utilizar la declaración de software {#use-both}

En el archivo de recursos de la aplicación `strings.xml` añada el siguiente código:

```XML
<string name="software_statement">softwarestatement value</string>
```
