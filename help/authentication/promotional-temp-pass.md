---
title: Pase temporal promocional
description: Pase temporal promocional
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1523'
ht-degree: 0%

---


# Pase temporal promocional {#promotional-temp-pass}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Resumen de características {#feature-summary}

El pase temporal promocional permite a los programadores ofrecer acceso temporal a su contenido protegido a los usuarios que no tengan credenciales de cuenta con un MVPD.

El pase temporal promocional está diseñado para utilizarse en campañas promocionales en las que un usuario, después de proporcionar información de identificación válida (por ejemplo, una dirección de correo electrónico) al programador, podrá consumir un **número predefinido de diferentes títulos de VOD para un período de tiempo predefinido**.

>[!IMPORTANT]
>
>Adobe no almacena información de identificación personal (PII). Por lo tanto, el programador debe establecer un hash sobre la información proporcionada por el usuario único en las API de autenticación de Primetime.

El Pase temporal promocional está construido sobre la [Pase temporal](/help/authentication/temp-pass.md) , lo que significa que incluye todas las funcionalidades de Temp Pass.

Una vez que se supera el número máximo predefinido de títulos de VOD o el período de tiempo predefinido, ese usuario no podrá acceder al contenido del mismo dispositivo o utilizando la misma información de identificador de usuario (por ejemplo, la dirección de correo electrónico) hasta que se borren los tokens de autorización del servidor de autenticación de Adobe Primetime.

>[!NOTE]
>
>Temp Pass forma parte del paquete Premium Workflow . Póngase en contacto con su representante de ventas de Primetime si le interesa utilizar esta funcionalidad.

## Comparación de paso temporal y de paso temporal promocional {#tp-ptp-comparison}

| Pase temporal | Pase temporal promocional |
|----------------------------------|----------------------------------------------------------------------------------------|
| Acceso al contenido <ul><li>basado en el tiempo</li></ul> | Acceso al contenido <ul><li>basado en el tiempo</li><li>en función del número de recursos</li></ul> |
| Seguridad de acceso basada en <ul><li>ID del dispositivo</li></ul> | Seguridad basada en <ul><li>ID del dispositivo</li><li>hash sobre la información de identificador de usuario proporcionada (por ejemplo, correo electrónico)</li></ul> |
| API de error de cliente disponible | API de error de cliente disponible |
| Restauración / Depuración disponible | Restauración / Depuración disponible |

## Detalles de las funciones {#feature-details}

Esta función permite a los usuarios acceder al contenido promocional desde un dispositivo específico (teléfono y tableta) después de haber proporcionado información única, como la dirección de correo electrónico, en la aplicación del programador.

El programador proporcionará un hash sobre la PII del usuario en las API de autenticación y autorización. Este hash se utilizará junto con el ID del dispositivo para generar una clave única para identificar el usuario y el dispositivo.

En función del ID del dispositivo y de la información proporcionada por el usuario y siguiendo la lógica siguiente, la autenticación de Adobe Primetime determinará si el usuario se encuentra en una nueva versión de prueba o en una existente:

* nuevo hash sobre la información proporcionada por el usuario (por ejemplo, correo electrónico), nuevo id. de dispositivo => nueva prueba
* hash existente sobre la información proporcionada por el usuario (por ejemplo, correo electrónico), nuevo id. de dispositivo => prueba existente (con hash existente sobre la información proporcionada por el usuario (por ejemplo, correo electrónico)
* nuevo hash sobre la información proporcionada por el usuario (por ejemplo, correo electrónico), ID de dispositivo existente => prueba existente (con el ID de dispositivo existente)
* hash existente sobre la información proporcionada por el usuario (por ejemplo, correo electrónico), ID de dispositivo existente => prueba existente

>[!NOTE]
>La validación y el hash de la información proporcionada por el usuario se gestionan por el programador, no por Adobe.

**La función Paso temporal promocional se puede configurar en función de las siguientes propiedades:**

* Clave de información proporcionada por el usuario (por ejemplo, correo electrónico)
* Número de recursos que el usuario puede consumir
* TTL: el lapso de tiempo en el que el usuario tiene derecho a consumir el número configurado de recursos

### Metadatos de usuario {#user-metadata}

A fin de facilitar la aplicación de la aplicación del Programador, **se expone la información de metadatos del usuario** en el pase temporal promocional, con las claves correspondientes (para activar las claves, póngase en contacto con tve-support@adobe.com):

* **remain_resources**: el número de recursos restantes que el usuario actual tiene derecho a consumir
* **used_assets**: la lista de recursos que el usuario actual ya ha consumido
* **expiration_date**: la fecha de caducidad del usuario actual

### ¿Cómo se calcula el tiempo de visualización? {#compute-viewing-time}

La cantidad de tiempo que un pase temporal sigue siendo válido no se correlaciona con la cantidad de tiempo que un usuario invierte viendo contenido en la aplicación del programador. Tras la solicitud inicial de autorización del usuario mediante el Paso temporal promocional, se calcula un tiempo de caducidad añadiendo el tiempo de solicitud actual inicial al TTL (período de tiempo de duración) especificado por el Programador.

### Autenticación y autorización {#authn-authz}

Para los flujos de transferencia temporal promocional, la autenticación y autorización no se comunican con un MVPD real, **de modo que todas las solicitudes de autorización se completarán correctamente** siempre que se cumplan todas estas condiciones:

* los tokens de autorización son válidos para los recursos especificados
* número de **used_assets** es inferior al límite establecido por el programador
* **expiration_date** es posterior a la fecha actual.

### Comportamiento de la comprobación preliminar {#preflight-beh}

Cuando se realiza una solicitud de comprobación previa o de preautorización para un MVPD de pase temporal promocional, la respuesta de comprobación previa correspondiente devuelta contendrá la lista completa de recursos de la solicitud de comprobación previa como comprobación previa correcta.

La lógica detrás de esto es: las condiciones de autorización de Pasos temporales promocionales se basan en el límite de tiempo y de recursos, no en recursos específicos. Más concretamente, siempre que se cumpla la limitación temporal y que no se supere el límite de recursos, se autorizarán los recursos llamados.

### SSO {#sso}

SSO no está habilitado para instancias de Pase temporal promocional, que se configura con &quot;Autenticación por solicitante&quot; habilitado. Esto significa que cuando el usuario cambia de la aplicación A a otra aplicación B que están integradas con el mismo pase temporal promocional, el usuario no iniciará sesión automáticamente.

### Cerrar sesión {#logout}

Todos los tokens de un dispositivo se eliminan al cerrar la sesión. Por lo tanto, el cambio del paso temporal promocional a un MVPD seleccionado por el usuario normal no debe depender de esta implementación. La recomendación es utilizar la variable `setSelectedProvider(null)` para borrar el estado de la aplicación y, a continuación, reiniciar el flujo de autenticación, que tiene una mejor experiencia de usuario.

### Diagrama de flujo de paso temporal promocional {#promo-tempass-flowdia}

![Diagrama de flujo de paso temporal promocional](assets/promo-temp-pass-flow.png)

*Figura: Flujo de paso temporal promocional*

## Implementar pase temporal promocional {#impl-promo-tempass}

Pasar temporal promocional requiere las siguientes funcionalidades del lado del cliente:

* **Información del identificador de usuario, por ejemplo propagación de direcciones de correo electrónico** (envío de la dirección de correo electrónico del usuario en los flujos de autenticación y autorización). La autenticación de Adobe Primetime requiere el correo electrónico para enlazar los tokens de autenticación y autorización (similar al caso de la `device_ID`, requerido en todas las llamadas).
* **Forzar autenticación** - permitir al programador forzar un flujo de autenticación cuando el usuario ya está autenticado. Esta funcionalidad es necesaria para forzar la actualización de los metadatos de un usuario (la clave de metadatos del usuario) **used_assets** contiene el número de recursos disponibles) cada vez que se inicia la aplicación. Dado que el usuario puede iniciar sesión en varios dispositivos, los metadatos de usuario presentes en el dispositivo durante el inicio de la aplicación no son fiables y es necesario actualizarlos para reflejar el estado actual de ese usuario específico (identificado por dirección de correo electrónico).


>[!IMPORTANT]
>La autenticación forzada solo es posible en iOS y Android.
>La autenticación de Primetime no tiene un mecanismo integrado para detener el flujo libre después de que hayan pasado los X minutos. La autenticación de Primetime dejará de realizarse **autorización** y **short media** tokens una vez que el usuario consume los recursos libres de Y. Depende de los programadores restringir el acceso una vez que caduque el pase temporal promocional.

## Seguridad {#security}

>[!IMPORTANT]
>Adobe no almacena información de identificación personal (PII). Por lo tanto, el programador debe establecer un hash sobre la información proporcionada por el usuario único en las API de autenticación de Primetime.

**Hash de la información de identificador de usuario**

Adobe recomienda usar la variable **SHA-2** familia o **SHA-256**, **SHA-512** en los datos antes de enviarlos a Adobe.

Por ejemplo, **SHA-256** over **&quot;user@domain.com&quot;** es **&quot;f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&quot;**.

## Restablecer o purgar el pase temporal promocional {#reset-promo-tempass}

Algunas reglas comerciales requieren la depuración regular del pase temporal promocional. Para ello, la autenticación de Primetime proporciona a los programadores un *public* API web, que se describe a continuación:

| `DELETE https://mgmt.auth.adobe.com/reset-tempass/v2/reset` |
|----|
| <ul><li>Protocolo: **https**</li><li>Host:<ul><li>Versión: **mgmt.auth.adobe.com**</li><li>Prequal: **mgmt-prequal.auth.adobe.com**</li></ul></li><li>Ruta: **/reset-tempass/v2/reset**</li><li>Parámetros de consulta: **device_id=all&amp;requestor_id=THE_REQUESTOR_ID&amp;mvpd_id=THE_TEMPASS_MVPD_ID**</li><li>encabezados: ApiKey: **1232293681726481**</li> <li>Respuesta:<ul><li>Correcto: **HTTP 204**</li><li>Error: **HTTP 400** para solicitudes incorrectas, **HTTP 401** si no se especifica ApiKey, **HTTP 403** si ApiKey no es válido</li></ul></li></ul> |

Además de los requisitos para purgar Temp Pass, el Promotional Temp Pass utiliza el hash sobre la información de identificador de usuario enviada como **generic_data** sobre autenticación y autorización para depuración.

Se enviará el hash, no todo el JSON:

```cURL
$ curl -X DELETE -H "Authorization:Bearer H4j7cF3GtJX81BrsgDa10GwSizVz" "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset/generic?key=f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&requestor_id=REF&mvpd_id=FlexibleTempPass"
```

### Clientes admitidos {#supported-clients}

| Clientes de autenticación de Adobe Primetime | Pase temporal promocional | Herramienta Restablecer | Admite código de respuesta específico/error de cliente |
|:--------------------------------------:|:---------------------:|:----------:|:-----------------------------------------------:|
| Activador de acceso JS | SÍ | SÍ | SÍ (a partir de la versión 3.0.0) |
| iOS de cliente nativo | SÍ | SÍ | SÍ (a partir de la versión 1.10) |
| Android de cliente nativo | SÍ | SÍ | SÍ |
| API sin cliente | SÍ | SÍ | NO |


## Limitaciones {#limitations}

Esta sección describe las limitaciones que se aplican a la implementación actual de Pasos temporales promocionales.

### Clientless {#lim-clientless}

**Dispositivos inteligentes sin un ID de dispositivo único**

No todas las aplicaciones de dispositivos inteligentes pueden proporcionar un ID de dispositivo único. En ausencia de uno, la autenticación de Adobe Primetime puede utilizar el UUID generado por el servicio de códigos de registro de Adobe como ID de dispositivo único. Esto significa que cuando el usuario cierra la sesión, se eliminan los tokens de autenticación y autorización. Una vez que el usuario intente autenticarse de nuevo, esta vez con información de usuario diferente (por ejemplo, correo electrónico), el usuario podrá autorizar de nuevo. Adobe recomienda añadir un flujo de IU que no permita a un usuario &quot;engañar&quot; al sistema y añadir lógica para determinar si es un usuario nuevo que solicita una versión de prueba o una versión de prueba existente.

**Restablecimiento/depuración de paso temporal**

Restablecer Temp Pass para clientes no está disponible en los casos específicos de Xbox360 y Xbox One, ya que estas plataformas requieren análisis de ID de dispositivo adicional, no es posible en la herramienta Restablecer temp Pass.

<!--
>[!RELATEDINFORMATION]
>
>* [Preflight Authorization](/help/authentication/preflight-authz.md)
-->