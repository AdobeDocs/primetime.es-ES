---
title: Empaquetado seguro del contenido
description: Empaquetado seguro del contenido
copied-description: true
exl-id: f554852c-83d9-4b31-8dde-2af577c70989
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Empaquetado seguro del contenido {#securely-packaging-content}

El archivo de configuración de la herramienta de línea de comandos del empaquetador de medios de acceso a Adobe requiere una credencial PKCS12 que se utiliza durante el empaquetado.

En las herramientas de línea de comandos de implementación de referencia, la contraseña del archivo de credenciales PKCS12 se almacena en el archivo flashaccess.properties en texto no cifrado. Por este motivo, tenga mucho cuidado al proteger el equipo que hospeda este archivo y asegúrese de que se encuentra en un entorno seguro. (Consulte [Seguridad física y acceso](../../aaxs-secure-deployment-guidelines/physical-sec-and-access.md)).

El empaquetador también utiliza los certificados de transporte del servidor de licencias y del servidor de licencias. Debe protegerse la integridad y confidencialidad de esta información. Solo las entidades autorizadas deben poder utilizar el empaquetador. Si alguna de las claves privadas está en peligro, informe inmediatamente a Adobe Systems Incorporated para que se pueda revocar el certificado.

>[!NOTE]
>
>La API permite utilizar la misma clave para varios fragmentos de contenido. Para garantizar el máximo nivel de seguridad, recomendamos esta función solo para contenido FMS de velocidad de bits múltiple. No se recomienda utilizar la misma clave para varios archivos que representen contenido diferente.

La API de paquetes de acceso a Adobe emite advertencias en determinadas condiciones. Debe revisar estas advertencias para determinar si los archivos se han cifrado correctamente. Los mensajes de advertencia pueden indicar que la directiva ha caducado, que no se cifrará una etiqueta o pista no reconocida, que los fragmentos de película no se cifrarán (y que las referencias dentro de esos fragmentos pueden no ser válidas) y que los metadatos no se cifrarán.

Si el contenido se empaqueta mediante una directiva con atributos incorrectos, la directiva debe actualizarse y la directiva actualizada debe estar disponible para el servidor de licencias a través de una lista de actualización de directivas u otro mecanismo para enviar la directiva actualizada al servidor. Algunos atributos de directiva no se pueden cambiar una vez creada la directiva. Si estos atributos son incorrectos, recupere el contenido de los sitios de distribución, revoque la directiva para que no se puedan conceder licencias futuras y vuelva a cifrar el contenido.

Cuando se completa el empaquetado, la clave de empaquetado no se destruye explícitamente; sin embargo, se recoge la basura. Por lo tanto, la clave de empaquetado permanece en la memoria durante un período de tiempo; debe protegerse contra el acceso no autorizado a la máquina y tomar medidas para asegurarse de que no exponga ningún archivo, como los volcados de núcleo, que pueda revelar esta información.
