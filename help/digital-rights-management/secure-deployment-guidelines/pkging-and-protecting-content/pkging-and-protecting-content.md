---
description: La información sobre el empaquetado y la protección del contenido le permite protegerlo.
title: Empaquetar y proteger contenido
exl-id: f33d382b-07d7-4630-9e44-820d6249fee4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# Empaquetar y proteger contenido {#packaging-protecting-content}

La información sobre el empaquetado y la protección del contenido le permite protegerlo.

## Protección del servidor {#securing-the-server}

Debe proteger físicamente el equipo en el que se produce la administración de directivas y el empaquetado de contenido.

Para obtener más información, consulte [Seguridad física y acceso](../../secure-deployment-guidelines/physical-sec-and-access.md).

Si la implementación del empaquetado de contenido requiere conectividad de red, debe proteger el sistema operativo e implementar una solución de cortafuegos adecuada. Para obtener más información, consulte [Topología de red](../../secure-deployment-guidelines/overview/network-topology.md).

## Empaquetado seguro del contenido {#securely-packaging-content}

El archivo de configuración para la herramienta de línea de comandos del empaquetador de medios DRM de Adobe Primetime requiere una credencial PKCS12 que se utiliza durante el empaquetado.

En las herramientas del esquema de implementación de referencia, la contraseña del archivo de credenciales PKCS12 se almacena en la `flashaccess.properties` archivo en texto no cifrado. Por este motivo, tenga mucho cuidado al proteger el equipo que aloja este archivo y asegúrese de que el equipo se encuentra en un entorno seguro. Para obtener más información, consulte [Seguridad física y acceso](../../secure-deployment-guidelines/physical-sec-and-access.md).

El empaquetador también utiliza los certificados de transporte del servidor de licencias y del servidor de licencias, y se debe proteger la integridad y confidencialidad de esta información. Solo las entidades autorizadas deben poder utilizar el empaquetador. Si las claves privadas están en peligro, informe a Adobe Systems Incorporated inmediatamente para que se pueda revocar el certificado.

>[!NOTE]
>
>La API permite utilizar la misma clave para varios fragmentos de contenido. Para garantizar el máximo nivel de seguridad, solo debe utilizar esta función para contenido FMS de velocidad de bits múltiple. No utilice la misma clave para varios archivos que representen contenido diferente.

La API de empaquetado DRM de Primetime emite advertencias en determinadas condiciones. Revise estas advertencias para determinar si los archivos se han cifrado correctamente. Los mensajes de advertencia pueden ser uno de los siguientes:

* La directiva ha caducado y no se puede cifrar una etiqueta o pista no reconocida.
* Los fragmentos de película no se pueden cifrar y las referencias dentro de esos fragmentos podrían no ser válidas.
* Los metadatos no se pueden cifrar.

Si el contenido se empaqueta mediante una directiva con atributos incorrectos, es necesario actualizar la directiva. La directiva actualizada debe estar disponible para el servidor de licencias a través de una lista de actualización de directivas u otro mecanismo de entrega. Algunos atributos de directiva no se pueden cambiar una vez creada la directiva. Si estos atributos son incorrectos, recupere el contenido de los sitios de distribución, revoque la directiva para que no se puedan conceder licencias futuras y vuelva a cifrar el contenido.

Cuando se completa el empaquetado, la clave de empaquetado se recoge como elemento no utilizado y no se destruye de forma explícita. Como resultado, la clave de empaquetado permanece presente en la memoria durante un tiempo. Debe protegerse contra el acceso no autorizado al equipo y asegurarse de que no expone ningún archivo, como los volcados de núcleo, que pueda revelar esta información.

## Almacenar directivas de forma segura {#securely-storing-policies}

El SDK de DRM de Adobe Primetime le permite desarrollar aplicaciones que se pueden utilizar en el empaquetado de contenido y la creación de directivas.

Al crear estas aplicaciones, puede permitir que algunos usuarios creen y modifiquen directivas, y limitar a otros usuarios a aplicar únicamente directivas existentes al contenido. Debe implementar los controles de acceso necesarios y crear cuentas de usuario con privilegios diferentes para la creación y aplicación de directivas.

Las directivas no se firman ni se protegen de modificaciones hasta que se utilizan en el empaquetado. Si le preocupa que los usuarios de la herramienta de empaquetado puedan modificar directivas, firme las directivas para asegurarse de que no se puedan modificar.

Para obtener más información sobre la creación de aplicaciones con el SDK, consulte las API de DRM de Primetime en [Referencias de API de Primetime](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).

## Cifrado de clave asimétrica {#asymmetric-key-encryption}

El cifrado de clave asimétrica, también denominado cifrado de clave pública, utiliza pares de claves. Una clave es para el cifrado y la otra para el descifrado.

La clave de descifrado o *`private key`*, se mantiene en secreto; la clave de cifrado, o *`public key`*, se pone a disposición de cualquier persona autorizada para cifrar contenido. Cualquier persona con acceso a la clave pública puede cifrar el contenido. Sin embargo, solo alguien con acceso a la clave privada puede descifrar el contenido. La clave privada no se puede reconstruir a partir de la clave pública.

Cuando se empaqueta contenido, se utiliza la clave pública del servidor de licencias para cifrar la clave de cifrado de contenido (CEK) en los metadatos DRM. Debe asegurarse de que solo el servidor de licencias tiene acceso a la clave privada del servidor de licencias. Si otra persona tiene la clave, puede descifrar y ver el contenido.

>[!CAUTION]
>
>Asegúrese de obtener el certificado del servidor de licencias que incluye la clave pública de una fuente de confianza. De este modo, puede asegurarse de que sea la clave del servidor de licencias y no una clave pública no fiable. Si los atacantes sustituyeran la clave pública por la del servidor de licencias, podrían descifrar el contenido.

Para obtener más información sobre cómo empaquetar contenido, consulte [Uso del SDK de DRM de Adobe Primetime para proteger el contenido](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_protecting_content.pdf).
