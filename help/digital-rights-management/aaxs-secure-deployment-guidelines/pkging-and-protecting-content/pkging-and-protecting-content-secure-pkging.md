---
title: Empaquetar contenido de forma segura
description: Empaquetar contenido de forma segura
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Empaquetar contenido de forma segura {#securely-packaging-content}

El archivo de configuración de la herramienta de línea de comandos de Adobe Access Media Packager requiere una credencial PKCS12 que se utiliza durante el empaquetado.

En las herramientas de la línea de comandos de implementación de referencia, la contraseña del archivo de credenciales PKCS12 se almacena en el archivo flashaccess.properties en texto claro. Por este motivo, tenga especial cuidado al proteger el equipo que aloja este archivo y asegúrese de que se encuentre en un entorno seguro. (Consulte [Seguridad física y acceso](../../aaxs-secure-deployment-guidelines/physical-sec-and-access.md)).

El empaquetador también utiliza los certificados de servidor de licencias y transporte de servidor de licencias. Debe protegerse tanto la integridad como la confidencialidad de esta información. Solo se debe permitir que las entidades autorizadas utilicen el empaquetador. Si alguna de las claves privadas está en peligro, informe inmediatamente a Adobe Systems Incorporated para que se pueda revocar el certificado.

>[!NOTE]
>
>La API permite utilizar la misma clave para varios fragmentos de contenido. Para garantizar el máximo nivel de seguridad, recomendamos que esta función solo se utilice para contenido FMS con una velocidad de bits múltiple. No se recomienda utilizar la misma clave para varios archivos que representen contenido diferente.

La API de paquetes de acceso a Adobe emite advertencias bajo ciertas condiciones. Debe revisar estas advertencias para determinar si los archivos se han cifrado correctamente. Los mensajes de advertencia pueden indicar que la política ha caducado, que una etiqueta o pista no reconocida no se cifrará, que los fragmentos de película no se cifrarán (y que las referencias dentro de esos fragmentos pueden no ser válidas) y que los metadatos no se cifrarán.

Si el contenido se empaqueta mediante una directiva con atributos incorrectos, la directiva debe actualizarse y la directiva actualizada debe estar disponible para el servidor de licencias a través de una lista de actualización de directivas u otro mecanismo para enviar la directiva actualizada al servidor. Algunos atributos de directiva no se pueden cambiar una vez creada la directiva. Si estos atributos son incorrectos, retire el contenido de los sitios de distribución, revoque la directiva para que no se puedan conceder licencias futuras y vuelva a cifrar el contenido.

Una vez finalizado el embalaje, la clave de embalaje no se destruye explícitamente; sin embargo, es basura recolectada. Por lo tanto, la clave de embalaje permanece presente en la memoria durante un período de tiempo; debe evitar el acceso no autorizado al equipo y tomar medidas para asegurarse de que no expone ningún archivo, como volcados principales, que pueda revelar esta información.
