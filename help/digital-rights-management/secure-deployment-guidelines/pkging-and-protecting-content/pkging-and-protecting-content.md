---
description: La información sobre el empaquetado y la protección del contenido le permite proteger el contenido.
title: Empaquetado y protección de contenido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---


# Empaquetado y protección de contenido {#packaging-protecting-content}

La información sobre el empaquetado y la protección del contenido le permite proteger el contenido.

## Protección del servidor {#securing-the-server}

Debe proteger físicamente el equipo en el que se produce la administración de directivas y el empaquetado de contenido.

Para obtener más información, consulte [Seguridad física y acceso](../../secure-deployment-guidelines/physical-sec-and-access.md).

Si la implementación del paquete de contenido requiere conectividad de red, debe reforzar el sistema operativo e implementar una solución de firewall adecuada. Para obtener más información, consulte [Topología de red](../../secure-deployment-guidelines/overview/network-topology.md).

## Empaquetar contenido de forma segura {#securely-packaging-content}

El archivo de configuración de la herramienta de línea de comandos de Adobe Primetime DRM Media Packager requiere una credencial PKCS12 que se utiliza durante el empaquetado.

En las herramientas de la serie de comandos Implementación de referencia, la contraseña del archivo de credenciales PKCS12 se almacena en el archivo `flashaccess.properties` en texto claro. Por este motivo, tenga especial cuidado cuando proteja el equipo que aloja este archivo y asegúrese de que el equipo esté en un entorno seguro. Para obtener más información, consulte [Seguridad física y acceso](../../secure-deployment-guidelines/physical-sec-and-access.md).

El empaquetador también utiliza los certificados de servidor de licencias y transporte de servidor de licencias, y se debe proteger la integridad y confidencialidad de esta información. Solo se debe permitir que las entidades autorizadas utilicen el empaquetador. Si las claves privadas están comprometidas, informe a Adobe Systems Incorporated inmediatamente para que se pueda revocar el certificado.

>[!NOTE]
>
>La API permite utilizar la misma clave para varios fragmentos de contenido. Para garantizar el máximo nivel de seguridad, solo debe utilizar esta función para el contenido FMS de velocidad de bits múltiple. No utilice la misma clave para varios archivos que representan contenido diferente.

La API de empaquetado de DRM de Primetime emite advertencias bajo ciertas condiciones. Revise estas advertencias para determinar si los archivos se han cifrado correctamente. Los mensajes de advertencia pueden ser uno de los siguientes:

* La directiva ha caducado y no se puede cifrar una etiqueta o pista no reconocida.
* Los fragmentos de película no se pueden cifrar y las referencias dentro de esos fragmentos pueden no ser válidas.
* Los metadatos no se pueden cifrar.

Si el contenido se empaqueta mediante una directiva con atributos incorrectos, la directiva debe actualizarse. La directiva actualizada debe estar disponible para el servidor de licencias a través de una lista de actualización de directivas u otro mecanismo de entrega. Algunos atributos de directiva no se pueden cambiar una vez creada la directiva. Si estos atributos son incorrectos, retire el contenido de los sitios de distribución, revoque la directiva para que no se puedan conceder licencias futuras y vuelva a cifrar el contenido.

Cuando se completa el empaquetado, la clave de embalaje se recoge en la basura y no se destruye explícitamente. Como resultado, la clave de empaquetado permanece presente en la memoria durante algún tiempo. Debe evitar el acceso no autorizado al equipo y asegurarse de que no expone ningún archivo, como volcados principales, que pueda revelar esta información.

## Almacenamiento seguro de directivas {#securely-storing-policies}

El SDK de Adobe Primetime DRM le permite desarrollar aplicaciones que se pueden utilizar en el empaquetado de contenido y la creación de directivas.

Al crear estas aplicaciones, puede permitir que algunos usuarios creen y modifiquen políticas, y limitar a otros usuarios a que solo apliquen políticas existentes al contenido. Debe implementar los controles de acceso necesarios y crear cuentas de usuario con diferentes privilegios para la creación de directivas y la aplicación de directivas.

Las políticas no se firman ni se protegen de modificaciones hasta que se utilizan en el embalaje. Si le preocupa que los usuarios de herramientas de empaquetado puedan modificar las políticas, firme las políticas para asegurarse de que no se puedan modificar.

Para obtener más información sobre la creación de aplicaciones con el SDK, consulte las API de DRM de Primetime en [Referencias de API de Primetime](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).

## Cifrado de claves asimétricas {#asymmetric-key-encryption}

El cifrado de claves asimétricas, también llamado cifrado de claves públicas, utiliza pares de claves. Una clave es para el cifrado y la otra es para el descifrado.

La clave de descifrado, o *`private key`*, se mantiene en secreto; la clave de cifrado, o *`public key`*, está disponible para todo aquel que esté autorizado a cifrar contenido. Cualquier persona con acceso a la clave pública puede cifrar el contenido. Sin embargo, solo las personas con acceso a la clave privada pueden descifrar el contenido. La clave privada no se puede reconstruir a partir de la clave pública.

Al empaquetar contenido, la clave pública del servidor de licencias se utiliza para cifrar la clave de cifrado de contenido (CEK) en los metadatos de DRM. Debe asegurarse de que solo el servidor de licencias tenga acceso a la clave privada del servidor de licencias. Si otra persona tiene la clave, puede descifrar y ver el contenido.

>[!CAUTION]
>
>Asegúrese de obtener el certificado del servidor de licencias que incluye la clave pública de un origen de confianza. De este modo, puede asegurarse de que es la clave del servidor de licencias y no una clave pública no fiable. Si los atacantes sustituyeran su clave pública por la clave del servidor de licencias, podrían descifrar su contenido.

Para obtener más información sobre cómo empaquetar contenido, consulte [Uso del SDK de Adobe Primetime DRM para proteger contenido](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_protecting_content.pdf).