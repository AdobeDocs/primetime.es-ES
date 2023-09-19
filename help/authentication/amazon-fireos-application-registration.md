---
title: Registro de aplicaciones de Amazon FireOS
description: Registro de aplicaciones de Amazon FireOS
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# Registro de aplicaciones de Amazon FireOS {#amazon-fireos-application-registration}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.

</br>

## Introducción {#intro}

A partir de la versión 3.0 del SDK de FireOS AccessEnabler, estamos cambiando el mecanismo de autenticación con los servidores de Adobe. En lugar de utilizar una clave pública y un sistema secreto para firmar el ID de solicitante, presentamos el concepto de una cadena de declaración de software que se puede utilizar para obtener un token de acceso que luego se utiliza para todas las llamadas que el SDK realiza a nuestros servidores. Además de una Declaración de software, también deberá crear un vínculo profundo para su aplicación.

Para obtener más información, consulte [Registro dinámico de clientes](/help/authentication/dynamic-client-registration.md)

## ¿Qué es una declaración de software? {#what}

Una declaración de software es un token JWT que contiene información sobre su aplicación. Cada aplicación debe tener una Declaración de Software única que nuestros servidores utilizan para identificar la aplicación en el sistema de Adobe. La declaración de software debe pasarse al inicializar el SDK de AccessEnabler y se utilizará para registrar la aplicación con el Adobe. Tras el registro, el SDK recibirá un ID de cliente y un secreto de cliente que se utilizarán para obtener un token de acceso. Cualquier llamada que el SDK realice a nuestros servidores requerirá un token de acceso válido. El SDK es responsable de registrar la aplicación, obtener y actualizar el token de acceso.

**Nota:** Las declaraciones de software son específicas de la aplicación y una declaración de software individual no se puede utilizar para más de una aplicación. Tenga en cuenta que esto también se aplica a las aplicaciones que ofrecen acceso a varios canales.

## ¿Cómo obtener una declaración de software? {#how-to}

### Si tiene acceso al Tablero de TVE de Adobe:

- Abra el explorador y vaya a <https://console.auth.adobe.com>
- Vaya a `Channels` y seleccione su canal.
- Vaya a `Registered Applications` Ficha.
- Haga clic en `Add new application`.
- Proporcione un nombre y una versión para su aplicación y seleccione las plataformas en las que estará disponible (por ejemplo, Android en nuestro caso).
- Proporcione un Nombre de dominio eligiendo de una lista de dominios ya configurados para su Programador.
- Inserte los cambios en el servidor y, a continuación, vuelva a la pestaña Aplicaciones registradas del canal.
- Debería ver una lista con todas las aplicaciones registradas. Haga clic en `Download` botón en la aplicación que acaba de crear. Nota: Es posible que tenga que esperar unos minutos antes de que su Declaración de software esté lista para su descarga.
- Se descargará un archivo de texto. Utilice su contenido como Declaración de software.

Para obtener más información, consulte [Dynamic Client Registration Management](/help/authentication/dynamic-client-registration-management.md)

### Si no tiene acceso al Tablero de TVE de Adobe:

Envíe un ticket a <tve-support@adobe.com>. Incluya toda la información necesaria, incluidos el canal, el nombre de la aplicación, la versión y las plataformas. Alguien de nuestro equipo de asistencia creará una declaración de software para usted.

## ¿Cómo utilizar la Declaración de software? {#use}

Después de obtener la Declaración de software, debe pasarla como un parámetro en el constructor del Habilitador de acceso. Se recomienda alojar la Declaración de software en una ubicación remota. De este modo, puede revocar y cambiar fácilmente la Declaración de software sin lanzar una nueva versión de su aplicación.

## Cómo utilizar la declaración de software {#use-both}

En el archivo de recursos de su aplicación `strings.xml` agregue el siguiente código:

```XML
<string name="software_statement">softwarestatement value</string>
```
