---
description: La información sobre el empaquetado y la protección del contenido le permite proteger el contenido.
seo-description: La información sobre el empaquetado y la protección del contenido le permite proteger el contenido.
seo-title: Empaquetado y protección del contenido
title: Empaquetado y protección del contenido
uuid: 9bf89f86-082e-40f9-8deb-c9774a9d8e02
translation-type: tm+mt
source-git-commit: a33e1f290fcf78e6f131910f6037f4803f7be98d

---


# Empaquetado y protección de contenido {#packaging-protecting-content}

La información sobre el empaquetado y la protección del contenido le permite proteger el contenido.

## Seguridad del servidor {#securing-the-server}

Debe proteger físicamente el equipo en el que se produce la administración de directivas y el empaquetado de contenido.

Para obtener más información, consulte Seguridad [física y acceso](../../secure-deployment-guidelines/physical-sec-and-access.md).

Si la implementación de empaquetado de contenido requiere conectividad de red, debe endurecer el sistema operativo e implementar una solución de cortafuegos adecuada. Para obtener más información, consulte Topología [de red](../../secure-deployment-guidelines/overview/network-topology.md).

## Empaquetado seguro de contenido {#securely-packaging-content}

El archivo de configuración de la herramienta de línea de comandos de Adobe Primetime DRM Media Packager requiere una credencial PKCS12 que se utiliza durante el empaquetado.

En las herramientas de la serie de comandos Implementación de referencia, la contraseña del archivo de credenciales PKCS12 se almacena en el `flashaccess.properties` archivo en texto sin formato. Por este motivo, tenga especial cuidado al proteger el equipo que aloja este archivo y asegúrese de que el equipo se encuentra en un entorno seguro. Para obtener más información, consulte Seguridad [física y acceso](../../secure-deployment-guidelines/physical-sec-and-access.md).

El empaquetador también utiliza los certificados de servidor de licencias y transporte del servidor de licencias, y debe protegerse la integridad y confidencialidad de esta información. Sólo las entidades autorizadas podrán utilizar el empaquetador. Si las claves privadas están comprometidas, informe a Adobe Systems Incorporated inmediatamente para que se pueda revocar el certificado.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>La API le permite utilizar la misma clave para varios fragmentos de contenido. Para garantizar el mayor nivel de seguridad, debe utilizar esta función únicamente para el contenido FMS de velocidad de bits múltiple. No utilice la misma clave para varios archivos que representen contenido diferente.

La API de empaquetado de DRM Primetime emite advertencias bajo ciertas condiciones. Revise estas advertencias para determinar si los archivos se han cifrado correctamente. Los mensajes de advertencia pueden ser uno de los siguientes:

* La directiva ha caducado y no se puede cifrar una etiqueta o pista no reconocida.
* Los fragmentos de película no se pueden cifrar y las referencias dentro de esos fragmentos pueden no ser válidas.
* No se pueden cifrar los metadatos.

Si el contenido se empaqueta mediante una directiva con atributos incorrectos, es necesario actualizar la directiva. La directiva actualizada debe estar disponible para el servidor de licencias mediante una lista de actualización de directivas u otro mecanismo de entrega. Algunos atributos de directiva no se pueden cambiar una vez creada la directiva. Si estos atributos son incorrectos, retire el contenido de los sitios de distribución, revoque la directiva para que no se puedan conceder licencias futuras y vuelva a cifrar el contenido.

Cuando se completa el empaquetado, la clave de empaquetado se recolecta como basura y no se destruye explícitamente. Como resultado, la clave de empaquetado permanece presente en la memoria durante algún tiempo. Debe evitar el acceso no autorizado a la máquina y asegurarse de no exponer ningún archivo, como los volcados principales, que pueda revelar esta información.

## Almacenamiento seguro de directivas {#securely-storing-policies}

El SDK de DRM de Adobe Primetime le permite desarrollar aplicaciones que se pueden utilizar en el empaquetado de contenido y la creación de políticas.

Al crear estas aplicaciones, puede permitir que algunos usuarios creen y modifiquen políticas, y limitar a otros usuarios a aplicar únicamente directivas existentes al contenido. Debe implementar los controles de acceso necesarios y crear cuentas de usuario con diferentes privilegios para la creación de directivas y la aplicación de políticas.

Las políticas no se firman ni se protegen de modificaciones hasta que se utilizan en el empaquetado. Si le preocupa que los usuarios de herramientas de empaquetado puedan modificar políticas, firme las políticas para asegurarse de que no se puedan modificar.

Para obtener más información sobre la creación de aplicaciones con el SDK, consulte Primetime DRM API en Referencias [API de](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References)API Primetime.

## Cifrado de claves asimétricas {#asymmetric-key-encryption}

El cifrado asimétrico de claves, también llamado cifrado de claves públicas, utiliza pares de claves. Una clave es para cifrado y la otra es para descifrado.

La clave de descifrado, o la *`private key`* clave, se mantiene en secreto; la clave de cifrado, o la *`public key`*, está disponible para cualquier persona autorizada para cifrar contenido. Cualquier persona que tenga acceso a la clave pública puede cifrar el contenido. Sin embargo, solo alguien con acceso a la clave privada puede descifrar el contenido. La clave privada no se puede reconstruir a partir de la clave pública.

Al empaquetar contenido, la clave pública del servidor de licencias se utiliza para cifrar la clave de codificación de contenido (CEK) en los metadatos DRM. Debe asegurarse de que sólo el servidor de licencias tiene acceso a la clave privada del servidor de licencias. Si otra persona tiene la clave, puede descifrar y ver el contenido.

>[!CAUTION]
>
>Asegúrese de obtener el certificado del servidor de licencias que incluye la clave pública de un origen de confianza. De este modo, puede asegurarse de que es la clave del servidor de licencias y no una clave pública no fiable. Si los atacantes sustituyeran su clave pública por la clave del servidor de licencias, podrían descifrar su contenido.

Para obtener más información sobre cómo empaquetar contenido, consulte [Uso del SDK de DRM de Adobe Primetime para la protección de contenido](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_protecting_content.pdf).