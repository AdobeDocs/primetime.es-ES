---
title: Registro de aplicaciones de Android
description: Registro de aplicaciones de Android
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---



# Registro de aplicaciones de Android {#android-application-registration}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Introducción {#intro}

A partir de la versión 3.0 del SDK de AccessEnabler para Android, estamos cambiando el mecanismo de autenticación con los servidores de Adobe. En lugar de utilizar una clave pública y un sistema secreto para firmar el requestorID, presentamos el concepto de una cadena de instrucción Software que puede utilizarse para obtener un token de acceso que se utiliza posteriormente para todas las llamadas que el SDK hace a nuestros servidores. Además de una declaración de software, también deberá crear un vínculo profundo para la aplicación.

Para obtener más información, consulte [Registro de cliente dinámico](/help/authentication/dynamic-client-registration.md)

## ¿Qué es una declaración de software? {#what}

Una instrucción de software es un token de JWT que contiene información sobre su aplicación. Cada aplicación debe tener una declaración de software única que nuestros servidores utilizan para identificar la aplicación en el sistema de Adobe. La declaración de software debe pasarse cuando se inicializa el SDK de AccessEnabler y se utilizará para registrar la aplicación con Adobe. Tras el registro, el SDK recibirá un ID de cliente y un secreto de cliente que se utilizarán para obtener un token de acceso. Cualquier llamada que el SDK realice a nuestros servidores requerirá un token de acceso válido. El SDK es responsable de registrar la aplicación, obtener y actualizar el token de acceso.

>[!NOTE]
>
>Las declaraciones de software son específicas de la aplicación y una declaración de software individual no se puede usar en más de una aplicación. Tenga en cuenta que las instrucciones de software a nivel de programador tienen la misma restricción, solo pueden utilizarse para una aplicación única, ya sea un solo canal o multicanal.

## ¿Cómo obtener una declaración de software? {#how-to-get-ss}

### Si tiene acceso al panel de control de Televisión del Adobe:

* Abra el explorador y vaya a [TVE Dashboard de Adobe Primetime](https://console.auth.adobe.com).
* Vaya a `Channels` y seleccione el canal.
* Vaya a `Registered Applications` Tabulación.
* Haga clic en `Add new application`.
* Proporcione un nombre y una versión para la aplicación y seleccione las plataformas en las que estará disponible. Android en nuestro caso.
* Proporcione un nombre de dominio eligiendo entre una lista de dominios ya configurados para el programador.
* Inserte los cambios en el servidor y vuelva a la pestaña Aplicaciones registradas del canal .
* Debería ver una lista con todas las aplicaciones registradas. Seleccione el **Descargar** en la aplicación que acaba de crear. Es posible que tenga que esperar unos minutos antes de que su Declaración de software esté lista para la descarga.
* Se descargará un archivo de texto. Utilice su contenido como Declaración de software.

Para obtener más información, consulte [Administración dinámica de registros de clientes](/help/authentication/dynamic-client-registration-management.md)

### Si no tiene acceso al panel de control de Televisión del Adobe:

Enviar un ticket a `tve-support@adobe.com`. Incluya toda la información necesaria como canal, nombre de aplicación, versión y plataformas, y alguien de nuestro equipo de soporte creará una declaración de software para usted.

## ¿Cómo usar la Declaración de software? {#how-to-use-ss}

Después de obtener su declaración de software, debe pasarla como un parámetro en el constructor Access Enabler. Se recomienda alojar la Declaración de software en una ubicación remota. De esta manera, puede revocar y cambiar fácilmente la Declaración de Software sin lanzar una nueva versión de su aplicación.

## Cree y utilice un vínculo profundo para la aplicación {#create}

En Android, utilice como valor de vínculo profundo el reverso del nombre de dominio seleccionado al crear la declaración de software

El vínculo profundo creado debe tener un valor único en el dispositivo Android. Cuando varias aplicaciones utilizan el mismo valor de vínculo profundo, los flujos de autenticación y cierre de sesión interferirán.

## Cómo utilizar la declaración de software y el vínculo profundo {#use-both}

En el archivo de recursos de la aplicación `strings.xml` añada el siguiente código:

```JAVA
    <string name="software_statement">softwarestatement value</string>
    <string name="redirect_uri">com.domain_name</string>
```

