---
seo-title: Empaquetado seguro de contenido
title: Empaquetado seguro de contenido
uuid: a5e7cc17-353b-47d1-b89c-a2ba3c9faca1
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Empaquetado seguro de contenido {#securely-packaging-content}

El archivo de configuración de la herramienta de línea de comandos de Adobe Access Media Packager requiere una credencial PKCS12 que se utiliza durante el empaquetado.

En las herramientas de la línea de comandos de implementación de referencia, la contraseña del archivo de credenciales PKCS12 se almacena en el archivo flashaccess.properties en texto sin formato. Por este motivo, tenga especial cuidado al proteger el equipo que aloja este archivo y asegúrese de que se encuentre en un entorno seguro. (Consulte Seguridad [física y acceso](../../aaxs-secure-deployment-guidelines/physical-sec-and-access.md)).

El empaquetador también utiliza los certificados de servidor de licencias y transporte del servidor de licencias. Debe protegerse tanto la integridad como la confidencialidad de esta información. Sólo las entidades autorizadas podrán utilizar el empaquetador. Si alguna de las claves privadas está en peligro, informe inmediatamente a Adobe Systems Incorporated para que se pueda revocar el certificado.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>La API le permite utilizar la misma clave para varios fragmentos de contenido. Para garantizar el mayor nivel de seguridad, recomendamos que esta función solo se utilice para el contenido FMS de velocidad de bits múltiple. No se recomienda utilizar la misma clave para varios archivos que representen contenido diferente.

La API de empaquetado de Adobe Access emite advertencias bajo determinadas condiciones. Debe revisar estas advertencias para determinar si los archivos se han cifrado correctamente. Los mensajes de advertencia pueden indicar que la directiva ha caducado, que una etiqueta o pista no reconocida no se cifrará, que los fragmentos de película no se cifrarán (y que las referencias dentro de esos fragmentos pueden no ser válidas) y que los metadatos no se cifrarán.

Si el contenido se empaqueta con una directiva con atributos incorrectos, la directiva debe actualizarse y la directiva actualizada debe estar disponible para el servidor de licencias a través de una lista de actualizaciones de directivas u otro mecanismo para entregar la directiva actualizada al servidor. Algunos atributos de directiva no se pueden cambiar una vez creada la directiva. Si estos atributos son incorrectos, retire el contenido de los sitios de distribución, revoque la política para que no se puedan conceder licencias futuras y vuelva a cifrar el contenido.

Cuando se completa el embalaje, la clave de embalaje no se destruye explícitamente; sin embargo, es basura recolectada. Por lo tanto, la clave de embalaje permanece presente en la memoria durante un período de tiempo; debe protegerse contra el acceso no autorizado a la máquina y tomar medidas para asegurarse de que no expone ningún archivo, como los volcados principales, que pueda revelar esta información.
