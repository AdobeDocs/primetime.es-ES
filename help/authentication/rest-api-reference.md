---
title: Referencia de API de REST
description: Referencia de la api de Rest
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 4%

---


# Referencia de API de REST {#rest-api-reference}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Formatos de respuesta {#response-formats}


>[!NOTE]
>
> Las API proporcionadas en estos servicios pueden devolver respuestas en XML o JSON (para API que devuelven una respuesta). Existen tres formas diferentes de especificar el formato de respuesta en la solicitud:
>
>* Definir el encabezado aceptar HTTP como `application/xml` o `application/json`.
>* En la carga útil de la solicitud, especifique el parámetro `format=xml` o `format=json`.
>* Llame al extremo del servicio web con extensión `.xml` o `.json`. Por ejemplo, `/regcode.xml` o `/regcode.json`
>
>Puede especificar cualquiera de los métodos anteriores. La especificación de varios métodos con formatos conflictivos puede dar lugar a errores o a resultados no deseados.

## Puntos finales de API de REST {#clientless-endpoints}

&lt;reggie_fqdn>:

* Producción - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Ensayo - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Producción - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Ensayo - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>


## Resumen de servicios web {#web_srvs_summary}

En la tabla siguiente se enumeran los servicios web disponibles para el enfoque sin cliente. Haga clic en los extremos de los servicios web para obtener más información (solicitud y respuesta de ejemplo, parámetros de entrada, métodos HTTP, etc.)


| Sr | Punto final del servicio web | Descripción | <!--[Diag.  </br>Ref](http://tve.helpdocsonline.com/api-reference-v2-test#illustration)-->. | Alojado en | Llamado por |
| --- | --- | --- | --- | --- | --- |
| 1. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode](/help/authentication/registration-code-request.md) | Devuelve el código de registro generado aleatoriamente y el URI de página de inicio de sesión | 2 | Adobe  </br>Reg Code Service | Dispositivo inteligente |
| 2. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode/  </br>  {registrationCode}](/help/authentication/return-registration-record.md) | Devuelve el registro de código de registro que contiene el código de registro UUID, el código de registro y el ID de dispositivo con hash | 8 | Adobe  </br>Reg Code Service | Autenticación de Primetime |
| 3. | [&lt;sp_fqdn>/api/v1/config/  </br>  {requestorId}](/help/authentication/provide-mvpd-list.md) | Devuelve la lista de MVPD configurados para el solicitante | 5 | Adobe  </br>Primetime  </br>autenticación  </br>Servicio | Inicio de sesión  </br>Web  </br>Aplicación |
| 4. | [&lt;sp_fqdn>/api/v1/authentication](/help/authentication/initiate-authentication.md) | Inicia el proceso AuthN informando del evento de selección de MVPD. Crea un registro en la base de datos de autenticación, que se concilia cuando se recibe una respuesta correcta de MVPD (paso 13) | 7 | Adobe  </br>Primetime  </br>autenticación  </br>Servicio | Inicio de sesión  </br>Web  </br>Aplicación |
| 5. | Consumidor de aserción SAML | Flujo de trabajo SAML existente entre la autenticación Primetime y MVPD | 13 | Primetime  </br>autenticación  </br>Servicio | Autenticación de Primetime |
| 6. | [&lt;sp_fqdn>/api/v1/checkauthn/  </br>  {registrationCode}](/help/authentication/check-authentication-flow-by-second-screen-web-app.md) | La aplicación web de inicio de sesión puede comprobar si el flujo de inicio de sesión intentado se ha realizado correctamente |  | Primetime  </br>autenticación   </br>Servicio | Inicio de sesión   </br>Web   </br>Aplicación |
| 7. | [&lt;sp_fqdn>/api/v1/tokens/authn](/help/authentication/retrieve-authentication-token.md) | Obtiene metadatos relacionados con token de AuthN | 15 | Primetime  </br>autenticación  </br>Servicio | Dispositivo inteligente |
| 8. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode/  </br>  {registrationCode}](/help/authentication/delete-registration-record.md) | Elimina el registro de código de registro y libera el código de registro para reutilizarlo | 16 | Adobe  </br>Reg Code Service | Autenticación de Primetime |
| 9. | [&lt;sp_fqdn>/api/v1/authorization](/help/authentication/initiate-authorization.md) | Obtiene la respuesta de autorización. | 17 | Primetime  </br>autenticación  </br>Servicio | Dispositivo inteligente |
| 10. | [&lt;sp_fqdn>/api/v1/checkauthn](/help/authentication/check-authentication-token.md) | Indica si el dispositivo tiene un token AuthN no caducado. |  | Primetime  </br>autenticación  </br>Servicio | Dispositivo inteligente |
| 11. | [&lt;sp_fqdn>/api/v1/tokens/authn](/help/authentication/retrieve-authentication-token.md) | Devuelve el token AuthN si se encuentra. |  | Primetime  </br>autenticación  </br>Servicio | Dispositivo inteligente |
| 12. | [&lt;sp_fqdn>/api/v1/tokens/authz](/help/authentication/retrieve-authorization-token.md) | Devuelve el token AuthZ si se encuentra. |  | Primetime  </br>autenticación  </br>Servicio | Dispositivo inteligente |
| 13. | [&lt;sp_fqdn>/api/v1/tokens/media](/help/authentication/obtain-short-media-token.md) | Devuelve el token de contenido corto si se encuentra - igual que /api/v1/mediatoken |  | Primetime  </br>autenticación  </br>Servicio | Dispositivo inteligente |
| 14. | [&lt;sp_fqdn>/api/v1/mediatoken](/help/authentication/obtain-short-media-token.md) | Obtiene un token multimedia corto |  | Primetime  </br>autenticación  </br>Servicio | Dispositivo inteligente |
| 15. | [&lt;sp_fqdn>/api/v1/preauthorization](/help/authentication/retrieve-list-of-preauthorized-resources.md) | Recupera la lista de recursos preautorizados |  | Primetime  </br>autenticación  </br>Servicio | Dispositivo inteligente |
| 16. | [&lt;sp_fqdn>/api/v1/preauthorization/{code}](/help/authentication/retrieve-list-of-preauthorized-resources-by-second-screen-web-app.md) | Recupera la lista de recursos preautorizados |  | Primetime  </br>autenticación  </br>Servicio | Aplicación web de inicio de sesión |
| 17. | [&lt;sp_fqdn>/api/v1/logout](/help/authentication/initiate-logout.md) | Eliminar los tokens de AuthN y AuthZ del almacenamiento |  | Primetime  </br>autenticación   </br>Servicio | Dispositivo inteligente |
| 18. | [&lt;sp_fqdn>/api/v1/tokens/usermetadata](/help/authentication/user-metadata.md) | Obtiene los metadatos del usuario una vez finalizado el flujo de autenticación | N/D | N/D | Dispositivo inteligente |
| 19. | [&lt;sp_fqdn>/api/v1/authentication/freepreview](/help/authentication/free-preview-for-temp-pass-and-promotional-temp-pass.md) | Crear un token de autenticación para Temp Pass o Promotional Temp Pass | N/D | Primetime  </br>autenticación  </br>Servicio | Dispositivo inteligente |


## Seguridad de la API de REST {#security}

Se debe llamar a todas las API sin cliente de autenticación de Primetime mediante el protocolo HTTPS para una comunicación segura. Además, la mayoría de las API llamadas deben contener un token de acceso proporcionado por [Registro de cliente dinámico](/help/authentication/dynamic-client-registration.md).

