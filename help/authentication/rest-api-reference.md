---
title: Referencia de API de REST
description: Referencia de la api de Rest
source-git-commit: 4c3a0dd56b4ef99ac8c57cfde61f792088b0ff4d
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 3%

---


# Referencia de API de REST {#rest-api-reference}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Formatos de respuesta {#response-formats}


>[!NOTE]
>
> Las API proporcionadas en estos servicios pueden devolver respuestas en XML o JSON (para API que devuelven una respuesta). Existen tres formas diferentes de especificar el formato de respuesta en la solicitud:
>* Configure HTTP Accept Header en &quot;application/xml</code>&quot; o &quot;application/json</code>&quot;
>* En la carga útil de la solicitud, especifique el parámetro &quot;format=xml&quot;</code>&quot; o &quot;format=json</code>&quot;</li>
>* Llame al extremo del servicio web con la extensión .xml</code> o .json</code>. Por ejemplo, &quot;/regcode.xml</code>&quot; o &quot;/regcode.json&quot;</code>&quot;
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


| Sr | Punto final del servicio web | Descripción | [Diag.  </br>Ref](http://tve.helpdocsonline.com/api-reference-v2-test#illustration). | Alojado en | Llamado por |
| --- | --- | --- | --- | --- | --- |
| 1. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode](http://tve.helpdocsonline.com/registration-code-request) | Devuelve el código de registro generado aleatoriamente y el URI de página de inicio de sesión | 2 | Adobe  </br>Reg Code Service | Dispositivo inteligente |
| 2. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode/  </br>  {registrationCode}](http://tve.helpdocsonline.com/return-registration-record) | Devuelve el registro de código de registro que contiene el código de registro UUID, el código de registro y el ID de dispositivo con hash | 8 | Adobe  </br>Reg Code Service | Autenticación de Primetime |
| 3. | [&lt;sp_fqdn>/api/v1/config/  </br>  {requestorId}](http://tve.helpdocsonline.com/provide-mvpd-list) | Devuelve la lista de MVPD configurados para el solicitante | 5 | Adobe  </br>Primetime  </br>autenticación  </br>Servicio | Inicio de sesión  </br>Web  </br>Aplicación |
| 4. | [&lt;sp_fqdn>/api/v1/authentication](http://tve.helpdocsonline.com/initiate-authentication) | Inicia el proceso AuthN informando del evento de selección de MVPD. Crea un registro en la base de datos de autenticación, que se concilia cuando se recibe una respuesta correcta de MVPD (paso 13) | 7 | Adobe  </br>Primetime  </br>autenticación  </br>Servicio | Inicio de sesión  </br>Web  </br>Aplicación |
| 5. | Consumidor de aserción SAML | Flujo de trabajo SAML existente entre la autenticación Primetime y MVPD | 13 | Primetime  </br>autenticación  </br>Servicio | Autenticación de Primetime |
| 6. | [&lt;sp_fqdn>/api/v1/checkauthn/  </br>  {registrationCode}](http://tve.helpdocsonline.com/check-authentication-flow-by-second-screen-web-app) | La aplicación web de inicio de sesión puede comprobar si el flujo de inicio de sesión intentado se ha realizado correctamente |  | Primetime  </br>autenticación   </br>Servicio | Inicio de sesión   </br>Web   </br>Aplicación |
| 7. | [&lt;sp_fqdn>/api/v1/tokens/authn](http://tve.helpdocsonline.com/rest-api-retrieve-authentication-token) | Obtiene metadatos relacionados con token de AuthN | 15 | Primetime  </br>autenticación  </br>Servicio | Dispositivo inteligente |
| 8. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestorId}/regcode/  </br>  {registrationCode}](http://tve.helpdocsonline.com/delete-registration-record) | Elimina el registro de código de registro y libera el código de registro para reutilizarlo | 16 | Adobe  </br>Reg Code Service | Autenticación de Primetime |
| 9. | [&lt;sp_fqdn>/api/v1/authorization](http://tve.helpdocsonline.com/initiate-authorization) | Obtiene la respuesta de autorización. | 17 | Primetime  </br>autenticación  </br>Servicio | Dispositivo inteligente |
| 10. | [&lt;sp_fqdn>/api/v1/checkauthn](http://tve.helpdocsonline.com/check-authentication-token) | Indica si el dispositivo tiene un token AuthN no caducado. |  | Primetime  </br>autenticación  </br>Servicio | Dispositivo inteligente |
| 11. | [&lt;sp_fqdn>/api/v1/tokens/authn](http://tve.helpdocsonline.com/rest-api-retrieve-authentication-token) | Devuelve el token AuthN si se encuentra. |  | Primetime  </br>autenticación  </br>Servicio | Dispositivo inteligente |
| 12. | [&lt;sp_fqdn>/api/v1/tokens/authz](http://tve.helpdocsonline.com/retrieve-authorization-token) | Devuelve el token AuthZ si se encuentra. |  | Primetime  </br>autenticación  </br>Servicio | Dispositivo inteligente |
| 13. | [&lt;sp_fqdn>/api/v1/tokens/media](http://tve.helpdocsonline.com/obtain-short-media-token) | Devuelve el token de contenido corto si se encuentra - igual que /api/v1/mediatoken |  | Primetime  </br>autenticación  </br>Servicio | Dispositivo inteligente |
| 14. | [&lt;sp_fqdn>/api/v1/mediatoken](http://tve.helpdocsonline.com/obtain-short-media-token) | Obtiene un token multimedia corto |  | Primetime  </br>autenticación  </br>Servicio | Dispositivo inteligente |
| 15. | [&lt;sp_fqdn>/api/v1/preauthorization](http://tve.helpdocsonline.com/retrieve-list-of-preauthorized-resources) | Recupera la lista de recursos preautorizados |  | Primetime  </br>autenticación  </br>Servicio | Dispositivo inteligente |
| 16. | [&lt;sp_fqdn>/api/v1/preauthorization/{code}](http://tve.helpdocsonline.com/retrieve-list-of-preauthorized-resources-by-way-of-web-app) | Recupera la lista de recursos preautorizados |  | Primetime  </br>autenticación  </br>Servicio | Aplicación web de inicio de sesión |
| 17. | [&lt;sp_fqdn>/api/v1/logout](http://tve.helpdocsonline.com/logout) | Eliminar los tokens de AuthN y AuthZ del almacenamiento |  | Primetime  </br>autenticación   </br>Servicio | Dispositivo inteligente |
| 18. | [&lt;sp_fqdn>/api/v1/tokens/usermetadata](http://tve.helpdocsonline.com/user-metadata-call) | Obtiene los metadatos del usuario una vez finalizado el flujo de autenticación | N/D | N/D | Dispositivo inteligente |
| 19. | [&lt;sp_fqdn>/api/v1/authentication/freepreview](http://tve.helpdocsonline.com/free-preview-for-temp-pass-and-promotional-temp-pass) | Crear un token de autenticación para Temp Pass o Promotional Temp Pass | N/D | Primetime  </br>autenticación  </br>Servicio | Dispositivo inteligente |

{style=&quot;table-layout:auto&quot;}

## Seguridad de la API de REST {#security}

Se debe llamar a todas las API sin cliente de autenticación de Primetime mediante el protocolo HTTPS para una comunicación segura. Además, la mayoría de las API llamadas deben contener un token de acceso proporcionado por [Registro de cliente dinámico](http://tve.helpdocsonline.com/dynamic-client-registration).


## Información relacionada {#related}

* [Información general de la API de REST](http://tve.helpdocsonline.com/reset-api-overview)
* [Guía de servidor a servidor](http://tve.helpdocsonline.com/server-to-server-cookbook)
* [Guía de cliente a servidor](http://tve.helpdocsonline.com/client-to-server)
* [Evite utilizar &quot;&amp;&#39;reg\_code&quot; en la solicitud /authenticate (nota técnica)](https://tve.zendesk.com/entries/23648011-Clientless-Avoid-using-reg-code-in-authenticate-request)
