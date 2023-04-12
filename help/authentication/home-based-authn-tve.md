---
title: Autenticación basada en el hogar para TV en todas partes
description: Autenticación basada en el hogar para TV en todas partes
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1676'
ht-degree: 0%

---


# Autenticación basada en el hogar para TV en todas partes

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## ¿Qué es la autenticación basada en el hogar? {#whatis-home-based-authn}

La autenticación basada en el hogar (HBA) es una función de TV en todas partes que permite a los suscriptores de televisión de pago ver contenido de TV en línea sin introducir credenciales de MVPD cuando están en casa, lo que mejora significativamente la experiencia del usuario con el flujo de autenticación.

Definición de autenticación basada en el hogar por el Comité de Tecnología de Autenticación Abierta (OATC): &quot;La autenticación automática interna es el proceso mediante el cual un MVPD/OVD utiliza características de la red doméstica (o identificadores a los que se puede acceder automáticamente entre dispositivos de la red doméstica) para autenticar qué cuenta de suscriptor está asociada a esa red doméstica, de modo que los usuarios no tengan que introducir manualmente sus credenciales al establecer una sesión de TVE para acceder al contenido protegido por TVE.&quot;



Para obtener más información sobre HBA y los estándares de la industria, lea la [Casos de uso y requisitos de OATC](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/Defining%20TVE%20Home-Based%20Authentication%20(HBA)%20%20Use%20Cases%20and%20Requirements%20Recommended%20Practice%20Version%201_0%20FINAL%20DRAFT%20FOR%20BOARD%20APPROVAL.pdf){target=_blank} documentación y **Directrices de experiencia del usuario de OATC para HBA**.

>[!NOTE]
>
>Algunos flujos de HBA forman parte del paquete de flujo de trabajo Premium. Póngase en contacto con su representante de ventas de Primetime si le interesa utilizar esta funcionalidad.

## Por qué el HBA es importante para usted {#why-hba}

El HBA es importante porque prácticamente elimina la barrera de inicio de sesión de los visores que están en casa y que ya tienen una suscripción por cable. Además, la autenticación basada en el hogar puede aumentar significativamente la participación de los espectadores y ofrecer una mejor experiencia de usuario para el contenido de TV en todas partes.

Actualmente, casi la mitad de los intentos de iniciar sesión no tienen éxito.

Una vez que el HBA fue activado por uno de los 5 MVPD principales, su tasa de conversión de autenticación **aumentado en un 40%** (del 45% al 63%)

![](assets/authn-conv-pre-post.png)

Además, debajo puede ver la tasa de conversión de inicio de sesión para un canal integrado con diferentes MVPD: los que han habilitado HBA para él y los que no tienen HBA. La tasa de conversión para quienes tienen HBA es considerablemente mayor que la de quienes no tienen HBA.

![](assets/hba-vs-non-hba.png)

Seis meses después de habilitar el HBA para la mayoría de los canales integrados con este MVPD, observamos un aumento del 82% en usuarios únicos (el número de usuarios que acceden a los canales de TV en todas partes a través de este MVPD casi se duplicó).

2w3Por el contrario, como puede ver en el gráfico siguiente, otros MVPD que no habían habilitado HBA solo tuvieron un aumento del 26% en los usuarios únicos en los últimos 6 meses.

![](assets/unique-visitors-incr.png)

A partir de nuestros datos, recopilados 6 meses antes y 6 meses después de habilitar el HBA, vimos un gran aumento en la participación de los espectadores para los canales habilitados para el HBA. Prácticamente los usuarios de MVPD que han habilitado HBA tienden a observar un 30% más de contenido que los usuarios de MVPD que no tienen HBA habilitado.

![](assets/user-engagement-increase.png)

## Compatibilidad con HBA de autenticación de Primetime {#auth-hba-support}

En esta sección se describe el soporte de HBA que proporciona la autenticación de Primetime, el comportamiento de las plataformas de autenticación de Primetime en los flujos de HBA y también se ofrecen detalles técnicos útiles para implementar HBA.

Características de autenticación de Primetime que admiten HBA

* Capacidad para establecer diferentes TTL de autenticación para HBA en comparación con autenticaciones que no son HBA (también requiere soporte para MVPD)
* Posibilidad de seleccionar automáticamente un MVPD (omitir el selector de MVPD) si la autenticación ha caducado. Esto resulta útil, especialmente cuando los TTL de HBA son pequeños.
* Capacidad de exponer a los programadores si la autenticación era HBA o no (también requiere soporte MVPD)

### Experiencia del usuario del HBA en plataformas de autenticación de Primetime {#hba-user-exp}

Las siguientes tablas proporcionan información sobre la experiencia del usuario para las plataformas soportadas cuando el HBA está habilitado y cuando el HBA no está habilitado:

| Flujo de usuario: tipo de plataforma | swf, iOS, Android |
|---|---|
| Con HBA habilitado | Cuando los usuarios están en casa, se autentican automáticamente. Una vez que caduca el token HBA AuthN, los usuarios se vuelven a autenticar automáticamente. |
| Sin HBA | Se solicita a los usuarios que seleccionen su MVPD e introduzcan sus credenciales, incluso si están en casa. Una vez que caduque el token de AuthN, los usuarios deben volver a introducir sus credenciales. |

| Flujo de usuario: tipo de plataforma | js, Windows (nativo) |
|---|---|
| Con HBA habilitado | Cuando los usuarios están en casa, se autentican automáticamente. Una vez que caduque el token HBA AuthN, los usuarios deben volver a seleccionar su MVPD desde el selector y se autenticarán automáticamente. |
| Sin HBA | Se pide a los usuarios que seleccionen su MVPD e introduzcan sus credenciales, incluso si están en casa. Una vez que el token AuthN caduca, los usuarios deben volver a introducir sus credenciales. |

| Flujo de usuario: tipo de plataforma | API de REST sin cliente (segunda autenticación de pantalla) |
|---|---|
| Con HBA habilitado | Cuando los usuarios están en casa y utilizan una aplicación de API de REST sin cliente, se autentican automáticamente en el segundo dispositivo de pantalla después de introducir el código de registro y seleccionar su MVPD. Una vez que caduca el token HBA AuthN, los usuarios se vuelven a autenticar automáticamente (en el segundo dispositivo de pantalla). |
| Sin HBA | Se pide a los usuarios que seleccionen su MVPD e introduzcan sus credenciales, incluso si están en casa. Una vez que el token AuthN caduca, los usuarios deben volver a introducir sus credenciales. |

### Detalles técnicos de implementación de HBA {#tech-details-hba}

#### Protocolo OAuth 2.0 {#oauth-2-protocol}

En el flujo del HBA para los MVPD integrados con el protocolo de autenticación OAuth 2.0, el MVPD emite un token de actualización y el Adobe emite un token de autenticación del HBA:

* El token de actualización tiene un TTL determinado por los requisitos comerciales del MVPD.
* TTL del token de autenticación del HBA **debe ser menor o igual que** el TTL del token de actualización.


*Descripción del flujo de autenticación del HBA para el protocolo OAuth 2.0*


| Acciones del usuario | Acciones del sistema |
|---|---|
| El usuario navega al sitio del programador. Cuando se intenta reproducir un vídeo, se muestra el selector de MVPD. El usuario selecciona su MVPD y hace clic en iniciar sesión. | Se realiza una comprobación de fondo. El MVPD aplica su conjunto de reglas para la detección de usuarios (por ejemplo, asigne la dirección IP del usuario con la dirección MAC de los módems aprovisionados por el distribuidor o de los receptores de conexión de banda ancha). |
| Se muestra una pantalla, que persiste durante unos 3 segundos. Se puede mostrar una página intersticial que informe al usuario de que se le está informando de que se está iniciando sesión automáticamente utilizando su cuenta MVPD. | <ol><li>AccessEnabler, que se instala en el lado del programador, envía una solicitud de autenticación (como una solicitud HTTP) al extremo de autenticación de Adobe Primetime.</li><li>El extremo de autenticación de Primetime redirige la solicitud al extremo de autenticación de MVPD. <br />**Nota:** La solicitud contiene el `hba_flag` (intente HBA = true) que indica que el MVPD debe intentar la autenticación del HBA.</li><li>El extremo de autenticación MVPD envía un código de autorización al extremo de autenticación de Adobe Primetime.</li><li>La autenticación de Adobe Primetime utiliza el código de autorización para solicitar un token de actualización y un token de acceso desde el punto final del token de MVPD.</li><li>El MVPD envía una decisión de autenticación y el `hba_status` (true/false) en el parámetro `id_token`.</li><li>Se envía una llamada al extremo del perfil de usuario de MVPD para exponer el [clave hba_status en los metadatos de usuario](/help/authentication/user-metadata-feature.md#obtaining).</li><li>El MVPD establece el TTL del token de actualización en un valor acordado por el MVPD y el Adobe establece el TTL del token AuthN en un valor menor o igual al valor del token de actualización.</li></ol> |
| El usuario está autenticado y ahora puede examinar el contenido de TV en todas partes titulado. | El token de autenticación se pasa al usuario que ahora puede examinar correctamente el sitio del programador. |

#### Protocolo SAML {#saml-protocol}

Descripción del flujo de autenticación del HBA para el protocolo de autenticación SAML

| Acciones del usuario | Acciones del sistema |
|---|---|
| El usuario navega al sitio del programador. Cuando se intenta reproducir un vídeo, se muestra el selector de MVPD. El usuario selecciona su MVPD y hace clic en iniciar sesión. | Se realiza una comprobación de fondo. El MVPD aplica su conjunto de reglas para la detección de usuarios (por ejemplo, asigne la dirección IP del usuario con la dirección MAC de los módems aprovisionados por el distribuidor o de los receptores de conexión de banda ancha). |
| Se muestra una pantalla, que persiste durante unos 3 segundos. Se puede mostrar una página intersticial que informe al usuario de que se le está informando de que se está iniciando sesión automáticamente utilizando su cuenta MVPD. | <ol><li>AccessEnabler, que se instala en el lado del programador, envía una solicitud de autenticación (como una solicitud HTTP) al extremo de autenticación de Adobe Primetime.</li><li>El extremo de autenticación de Primetime redirige la solicitud al extremo de autenticación de MVPD.</li><li>El MVPD debe enviar una decisión de autenticación en forma de respuesta SAML que debe contener el indicador HBA: hba_status (true/false).</li><li>Se envía una llamada al extremo del perfil de usuario de MVPD para exponer el [clave hba_status en los metadatos de usuario](/help/authentication/user-metadata-feature.md#obtaining).</li></ol> |
| El usuario está autenticado y ahora puede examinar el contenido de TV en todas partes titulado. | El token de autenticación se pasa al usuario que ahora puede examinar correctamente el sitio del programador. |


## Cómo activar el HBA {#how-to-activate-hba}

* **Protocolo OAuth:**
   * Para habilitar el HBA, consulte [Guía del usuario del tablero de Primetime TVE](/help/authentication/tve-dashboard-user-guide.md)
* **Protocolo SAML:** La autenticación basada en el hogar se activa en el lado MVPD. El programador o el Adobe no necesitan ninguna acción.
Para obtener más información sobre los MVPD que admiten la autenticación basada en el hogar, consulte [Estado del HBA para MVPD](/help/authentication/hba-status-mvpds.md).

## Preguntas frecuentes {#faqs}


**Pregunta:** ¿Por qué la separación entre la autenticación basada en el hogar y los protocolos SAML y OAuth2?

**Respuesta:** El flujo del HBA es diferente para los dos protocolos. Desde la perspectiva de un programador, no es necesario actuar para garantizar que el HBA esté habilitado para los MVPD de SAML, mientras que para los MVPD de OAuth2, el HBA puede activarse o desactivarse en el panel TVE de Primetime.



**Pregunta:** ¿Es necesario que los usuarios rellenen un nombre de usuario y una contraseña la primera vez que se autentican cuando el HBA está habilitado?

**Respuesta:** No, no se requiere nombre de usuario y contraseña.



**Pregunta:** ¿Cómo se aplican los controles parentales?

**Respuesta 1:** Adobe puede deshabilitar el HBA para integraciones con canales que necesitan aprobación de control parental.

**Respuesta 2:** Adobe está trabajando con OATC en un documento UX que recomienda cómo configurar la experiencia del HBA con los controles parentales.



**Pregunta:** ¿Los proveedores que soportan HBA tienen ventanas TTL más cortas para HBA y luego lo hacen para la autenticación regular?

**Respuesta:** La configuración de TTL es configurable. Recomendamos configurar un TTL más corto para los tokens de autenticación de HBA para evitar un mal manejo.


## Información útil {#useful-info}

* [Acceso instantáneo (HBA) Recommendations](http://www.ctamtve.com/instantaccess){target=_blank} - por CTAM
* [Implementación de muestra de HBA en la aplicación de programador](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/HBA_Flow_Sample.pdf?dc=201604222139-1346){target=_blank} - por Adobe
   <!--* [Home Based Authentication User Experience Guidelines for TV Everywhere](http://oatc.us/Standards/DownloadRecommendedPractices.aspx){target=_blank} - by OATC-->
* [Casos y requisitos de uso de autenticación basada en el hogar](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/Defining%20TVE%20Home-Based%20Authentication%20(HBA)%20%20Use%20Cases%20and%20Requirements%20Recommended%20Practice%20Version%201_0%20FINAL%20DRAFT%20FOR%20BOARD%20APPROVAL.pdf){target=_blank} por OATC
* [Infografía de autenticación basada en el hogar](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/AdobeNewsletterHBA.pdf?dc=201604260953-2640){target=_blank} - por Adobe
* [Autenticación mediante el protocolo OAuth 2.0](/help/authentication/authn-oauth2-protocol.md)
* [Autenticación con MVPD de SAML](/help/authentication/authn-usecase.md)
* [Guía del usuario del tablero de Primetime TVE](/help/authentication/tve-dashboard-user-guide.md)
* [Metadatos de usuario de hba_status](/help/authentication/user-metadata-feature.md#obtaining)



