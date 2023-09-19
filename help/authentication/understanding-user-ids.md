---
title: Explicación de los ID de usuario
description: Explicación de los ID de usuario
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---

# Explicación de los ID de usuario {#understanding-user-ids}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.

Conceptualmente, cada usuario que inicia un flujo de asignación de derechos se asocia con un único ID de usuario único. Sin embargo, a lo largo de un flujo de derechos, ese ID de usuario se puede presentar de diferentes maneras, en función de la API de la que obtenga el ID.

El `sessionGUID` en el token de medios corto se encuentra la forma segura del ID de usuario, que está disponible a través de la variable `sendTrackingData()` llamada. En todas las integraciones actuales, se trata de un GUID persistente para el usuario a lo largo del tiempo y los dispositivos. El origen del GUID comienza con el ID de usuario de la respuesta de autenticación proveniente de MVPD. Sin embargo, algunas MVPD podrían cambiar de opinión en el futuro y comenzar a enviar un GUID transitorio. Si un programador desea asegurarse de que el ID del usuario de origen de MVPD en la respuesta AuthN sea persistente, debe solucionarlo en sus acuerdos con MVPD.

Estas son las diferentes formas en que el ID de usuario se representa en las API de autenticación de Adobe Primetime:

| Propiedad | Finalidad | Con hash | Firmado digitalmente | Descripción |
| --- | --- | --- | --- | --- |
| Propiedad GUID sendTrackingData() | Seguimiento/análisis | Sí | No | : el ID de usuario de MVPD, con hash por Adobe. El ID de usuario no se puede rastrear hasta el origen de la MVPD. </br> </br> : Este formulario del ID no está firmado digitalmente, por lo que no es seguro para la prevención de fraudes. Sin embargo, es suficientemente bueno para el análisis.  </br> </br> : Esta forma del ID de usuario se proporciona del lado del cliente en todos los eventos que la autenticación de Adobe Primetime genera en el flujo AuthN/AuthZ. |
| Propiedad sessionGUID del token de medios cortos | Seguimiento del fraude del uso simultáneo | Sí | Sí | - Es el mismo que el ID de usuario a través de sendTrackingData(); sin embargo, este está firmado digitalmente para proteger su integridad y es lo suficientemente bueno como para utilizarse en el seguimiento de fraudes. </br> </br> - Está pensado para ser procesado en el servidor después de usar nuestra biblioteca de validador, y puede ser analizado para patrones de fraude antes de lanzar el flujo de vídeo al cliente.  Realizar cualquiera de estas tareas depende del Programador. |
| getMetadata(), propiedad userID | Vinculación de cuentas, investigación de fraude con MVPD | No | No | : Esta propiedad permite a Adobe exponer el ID de usuario de MVPD de origen real al programador. </br> </br> - En la configuración de Adobe se puede establecer como cifrado o no (según la preferencia de MVPD). Si está cifrado, se cifrará con la clave pública del certificado del programador proporcionado al Adobe para que no se exponga de forma clara al cliente. </br> </br> - Esto le da al programador el ID de usuario real de la MVPD, por lo que es algo que puede ser utilizado para la vinculación de cuentas o investigación de fraude directamente con la MVPD. |


**En conclusión**

* En general, la MVPD proporciona un ID único y persistente <u>y lo pasa al Adobe cuando la autenticación se realiza correctamente</u>. En general, es coherente en todas las redes. La excepción es Comcast MVPD, que proporciona un ID de usuario diferente para cada canal.

* El ID de usuario de MVPD no contiene PII y NO es un número de cuenta. No necesita exponerse en forma cifrada, ya que hemos validado con todas las MVPD que no se envía ninguna PII.

El uso del ID de usuario depende del caso de uso:

* Si lo necesita para seguimiento/análisis, el lugar más práctico es obtenerlo de `sendTrackingData()`.
* Si lo necesita en el lado del servidor para la publicación de secuencias, el fraude o los datos operativos, puede obtenerlo del validador de tokens de medios.
* Si lo necesita para vincular cuentas y cometer fraudes más profundos, consulte con su contacto de Adobe la disponibilidad.
