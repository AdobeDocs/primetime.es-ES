---
title: Explicación de los ID de usuario
description: Explicación de los ID de usuario
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---


# Explicación de los ID de usuario {#understanding-user-ids}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

Conceptualmente, cada usuario que inicia un flujo de derechos está asociado a un único ID de usuario único. Sin embargo, durante el flujo de autorizaciones, ese ID de usuario se puede presentar de diferentes maneras, según la API desde la que obtenga el ID.

La variable `sessionGUID` en el token de medios cortos es la forma segura del ID de usuario, que está disponible a través de la variable `sendTrackingData()` llamada a . En todas las integraciones actuales, se trata de un GUID persistente para el usuario a lo largo del tiempo y los dispositivos. El origen del GUID comienza con el ID de usuario de la respuesta de autenticación proveniente del MVPD. Sin embargo, algunos MVPD podrían cambiar de opinión en el futuro y empezar a enviar un GUID transitorio. Si un programador desea asegurarse de que el ID de usuario de origen de MVPD en la respuesta AuthN sea persistente, debe hacerlo en sus acuerdos con MVPD.

Estas son las diferentes formas en que el ID de usuario se representa en las API de autenticación de Adobe Primetime:

| Propiedad | Objetivo | Protegido | Firmado digitalmente | Descripción |
| --- | --- | --- | --- | --- |
| sendTrackingData() propiedad GUID | Seguimiento/análisis | Sí | No | - El ID de usuario de MVPD, cifrado por Adobe. El ID de usuario no se puede rastrear hasta el origen en el MVPD. </br> </br> - Esta forma de ID no se firma digitalmente, por lo que no es segura para la prevención del fraude. Sin embargo, es lo suficientemente bueno para el análisis.  </br> </br> : esta forma del ID de usuario se proporciona en el lado del cliente en todos los eventos que genera la autenticación de Adobe Primetime en el flujo AuthN/AuthZ. |
| Propiedad sessionGUID del token de medios cortos | Seguimiento de fraudes de uso simultáneo | Sí | Sí | : Es igual que el ID de usuario a través de sendTrackingData(), sin embargo, este se firma digitalmente para proteger su integridad y es lo suficientemente bueno para ser utilizado para el seguimiento de fraudes. </br> </br> - Está pensado para ser procesado en el servidor después de usar nuestra biblioteca de validadores, y puede ser analizado por patrones de fraude antes de lanzar el flujo de vídeo al cliente.  Realizar cualquiera de estas tareas depende del Programador. |
| getMetadata() userID, propiedad | Vinculación de cuentas, investigación de fraude con MVPD | No | No | : Esta propiedad permite a Adobe exponer el ID de usuario de MVPD de origen real al programador. </br> </br> - En la configuración de Adobe puede configurarse como cifrado o no (dependiendo de la preferencia de MVPD). Si está encriptado, se cifrará con la clave pública del certificado del programador proporcionado al Adobe, para que no se exponga claramente al cliente. </br> </br> - Esto le da al programador el ID de usuario real del MVPD, por lo que es algo que puede ser utilizado para la vinculación de cuentas o la investigación de fraude directamente con el MVPD. |


**En conclusión**

* En general, el MVPD proporciona un ID único persistente <u>y lo pasa al Adobe en caso de autenticación correcta</u>. Por lo general, es coherente en todas las redes. La excepción es Comcast MVPD, que proporciona un ID de usuario diferente para cada canal.

* El ID de usuario de MVPD no contiene PII y NO es un número de cuenta. No es necesario que se exponga de forma cifrada, ya que hemos validado con todos los MVPD que no se está enviando ningún PII.

El uso del ID de usuario depende del caso de uso:

* Si lo necesita para el seguimiento/análisis, el lugar más práctico es obtenerlo de `sendTrackingData()`.
* Si lo necesita en el lado del servidor para la publicación de flujos, el fraude o los datos operativos, puede obtenerlo del validador de tokens de medios.
* Si lo necesita para la vinculación de cuentas y un fraude más profundo, consulte a su contacto de Adobe para obtener disponibilidad.

