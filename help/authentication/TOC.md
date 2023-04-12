---
product: adobe primetime
audience: end-user
user-guide-title: Autenticación de Primetime
user-guide-description: null
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---


# Ayuda de autenticación de Primetime {#authentication}

+ [Información general sobre la autenticación de Primetime](home.md)
+ Conceptos de autenticación de Primetime {#authentication-concepts}
   + [Documento técnico](technical-paper.md)
   + [Información general para programadores](programmer-overview.md)
   + [Información general de MVPD](mvpd-overview.md)
+ Guías de inicio rápido {#kickstart-guides}
   + [Guía de inicio rápido del programador](programmer-kickstart-guide.md)
   + [Guía de inicio rápido de MVPD](mvpd-kickstart-guide.md)
+ Guía de integración del programador {#programmer-integration-guide}
   + [Información general sobre la guía de integración del programador](programmer-integration-guide-overview.md)
   + [Flujo de asignación de derechos del programador](entitlement-flow.md)
   + [Casos de uso de programadores](programmer-use-cases.md)
   + [Pasar información del cliente (dispositivo, conexión y aplicación)](passing-client-information-device-connection-and-application.md)
   + API de REST {#restapi}
      + [Información general de la API de REST](rest-api-overview.md)
      + [Guía de la API de REST (servidor a servidor)](rest-api-cookbook-servertoserver.md)
      + [Guía de la API de REST (cliente a servidor)](rest-api-cookbook-clienttoserver.md)
      + Referencia de la API de Rest {#rest-api-reference}
         + [Referencia de API de REST](rest-api-reference.md)
         + [Solicitud de código de registro](registration-code-request.md)
         + [Registro de devoluciones](return-registration-record.md)
         + [Eliminar registro](delete-registration-record.md)
         + [Proporcionar lista MVPD](provide-mvpd-list.md)
         + [Iniciar autenticación](initiate-authentication.md)
         + [Comprobar token de autenticación](check-authentication-token.md)
         + [Recuperar token de autenticación](retrieve-authentication-token.md)
         + [Iniciar autorización](initiate-authorization.md)
         + [Recuperar token de autorización](retrieve-authorization-token.md)
         + [Obtener token de medio corto](obtain-short-media-token.md)
         + [Comprobar el flujo de autenticación por aplicación web de segunda pantalla](check-authentication-flow-by-second-screen-web-app.md)
         + [Recuperar lista de recursos preautorizados](retrieve-list-of-preauthorized-resources.md)
         + [Recuperar lista de recursos preautorizados por aplicación web de segunda pantalla](retrieve-list-of-preauthorized-resources-by-second-screen-web-app.md)
         + [Inicio de sesión](initiate-logout.md)
         + [Metadatos de usuario](user-metadata.md)
         + [Recuperar solicitud de perfil](retrieve-profilerequest.md)
         + [Token Exchange](token-exchange.md)
         + [Vista previa gratuita para pase temporal y pase temporal promocional](free-preview-for-temp-pass-and-promotional-temp-pass.md)
   + SDK de AccessEnabler {#accessenabler-sdk}
      + SDK de JavaScript {#javascriptsdk}
         + [Información general del SDK de JavaScript](javascript-sdk-overview.md)
         + [Guía de SDK para JavaScript](javascript-sdk-cookbook.md)
         + [Referencia de la API del SDK para JavaScript](javascript-sdk-api-reference.md)
         + Directrices {#js-sdk-guidelines}
            + [Inicio de sesión y cierre de sesión sin actualizar](refreshless-login-and-logout.md)
         + API de JavaScript {#js-api}
            + [Preautorizar](js-preauthorize.md)
      + SDK de iOS/tvOS {#ios-sdk}
         + [Información general sobre el SDK de iOS/tvOS](iostvos-sdk-overview.md)
         + [Guía del SDK para iOS/tvOS](iostvos-sdk-cookbook.md)
         + [Referencia de la API del SDK para iOS/tvOS](iostvos-sdk-api-reference.md)
         + Directrices {#ios-tvos-sdk-guidelines}
            + [Registro de aplicaciones de iOS/tvOS](iostvos-application-registration.md)
            + Directrices de migración {#migration-guidelines}
               + [Guía de migración de iOS/tvOS v3.x](iostvos-v3x-migration-guide.md)
         + API de iOS/tvOS {#ios-tvos-api}
            + [Preautorizar](preauthorize.md)
      + SDK para Android {#androidsdk}
         + [Información general del SDK para Android](android-sdk-overview.md)
         + [Guía de SDK para Android](android-sdk-cookbook.md)
         + [Referencia de la API del SDK para Android](android-sdk-api-reference.md)
         + Directrices {#androidguidelines}
            + [Registro de aplicaciones de Android](android-application-registration.md)
            + [SDK para Android con registro de cliente dinámico](android-sdk-with-dynamic-client-registration.md)
         + API de Android{#androidapi}
            + [Preautorizar](preauthorize-android.md)
      + SDK de Amazon FireOS {#fireossdk}
         + [Amazon FireOS SSO: Guía de inicio del programador](amazon-firetv-sso-programmer-kickoff-guide.md)
         + [Amazon FireOS SSO mediante la guía de cookies de API sin cliente](amazon-fireos-sso-using-clientless-api-cookbook.md)
         + [Información general técnica de Amazon FireOS](amazon-fireos-technical-overview.md)
         + [Guía de integración de Amazon FireOS](amazon-fireos-integration-cookbook.md)
         + [Referencia de la API de Amazon FireOS](amazon-fireos-native-client-api-reference.md)
         + [Registro de la aplicación Amazon FireOS](amazon-fireos-application-registration.md)
         + [SDK de FireOS con registro de cliente dinámico](fireos-sdk-with-dynamic-client-registration.md)
   + SSO de plataforma {#platform-sso}
      + Apple SSO {#apple-sso}
         + [Información general de Apple SSO](apple-sso-overview.md)
         + [Guía de Apple SSO (API de REST)](apple-sso-cookbook-rest-api.md)
         + [Guía de Apple SSO (SDK de iOS/tvOS)](apple-sso-cookbook-iostvos-sdk.md)
      + Roku SSO {#roku-sso}
         + [Roku SSO](roku-sso-overview.md)
   + Metadatos de contenido {#content-metadata}
      + [Identificación del recurso protegido](identify-protected-resources.md)
   + Integración del servidor de contenido {#content-serv-int}
      + [Integración del verificador de tokens de medios](media-token-verifier-int.md)
   + Apéndices {#appendices}
      + [Sugerencias de depuración](appendix-b-debugging-tips.md)
+ Guía de integración de MVPD {#mvpd-int-guide}
   + [Funciones de integración](mvpd-integr-features.md)
   + [Autenticación](authn-usecase.md)
   + [Autenticación mediante el protocolo OAuth 2.0](authn-oauth2-protocol.md)
   + [Autorización](authz-usecase.md)
   + [Autorización previa](mvpd-preflight-authz.md)
   + [Cierre de sesión de MVPD](usecase-mvpd-logout.md)
   + [Intercambio de metadatos de contenido](mvpd-content-metadata-exchange.md)
   + [Intercambio de metadatos de usuario](mvpd-user-metadata-exchng.md)
   + [Servicio web Proxy MVPD](proxy-mvpd-webserv.md)
   + [Integración de proxy MVPD SAML](proxy-mvpd-saml-int.md)
   + [Alcance del proveedor de servicios](serv-provider-scoping.md)
   + [MVPD permite direcciones IP](mvpd-listing-ip-addres.md)
+ Funciones de autenticación de Primetime {#auth-features}
   + Integración con Adobe Analytics {#analytics-int}
      + [Integración de datos del servidor de autenticación de Primetime en Adobe Analytics](integrate-authn-servr-data-analytics.md)
      + [Uso del ID de Experience Cloud en la autenticación de Primetime](exp-cloud-id-authn.md)
   + Supervisión del servicio de derechos {#entitlement-service-monitoring}
      + [Resumen de la supervisión del servicio de derechos](entitlement-service-monitoring-overview.md)
      + [API de supervisión del servicio de derechos](entitlement-service-monitoring-api.md)
      + [Métricas del lado del servidor](understanding-serverside-metrics.md)
   + Pase temporal {#temp-pass}
      + [Pase temporal](temp-pass.md)
      + [Paso temporal promocional](promotional-temp-pass.md)
   + Inicio de sesión único {#sso}
      + [Compatibilidad con inicio de sesión único](sso-support.md)
      + [SSO mediante autenticación pasiva](sso-passive-authn.md)
   + Autenticación basada en el hogar {#home-based-auth}
      + [Autenticación basada en el hogar para TV en todas partes](home-based-authn-tve.md)
      + [Estado del HBA para MVPD](hba-status-mvpds.md)
   + Metadatos de usuario {#user-metadat}
      + [Metadatos de usuario](user-metadata-feature.md)
   + [Autorización previa](preflight-authz.md)
   + Informes de errores {#error-reportn}
      + [Informes de errores](error-reporting.md)
      + [Códigos de error mejorados](enhanced-error-codes.md)
   + Registro del cliente {#client-regn}
      + [Registro de cliente dinámico](dynamic-client-registration.md)
      + [API de registro de cliente dinámico](dynamic-client-registration-api.md)
      + [Administración dinámica de registros de clientes](dynamic-client-registration-management.md)
   + Servicio de degradación {#degrn-service}
      + [Información general de la API de degradación](degradation-api-overview.md)
   + Preparación para la privacidad {#privacy-readiness}
      + [Información general sobre la compatibilidad con Privecy](privacy-supp-overview.md)
      + [Cómo realizar una solicitud de privacidad](make-privacy-req.md)
+ Sugerencias y solución de problemas {#tips-troubleshoot}
   + [Permitir MVPD en el cuadro de diálogo de selección](allow-mvpd-selectn-dialog.md)
   + [Impedir que los MVPD aparezcan en el cuadro de diálogo de selección](prevent-mvpd-selectn-dialog.md)
+ Asistencia {#support}
   + [Procedimientos de escalación](escalation-procedures.md)
   + [Monitorización del pase de TV de Adobe de Primetime](monitoring-adobe-pay-tv-pass.md)
   + [Requisitos mínimos del sistema](minimum-system-requirements.md)
+ Notas de la versión {#release-notes}
   + [Notas de la versión de la versión 2.64.1 de la autenticación de Primetime](auth-rn-2641.md)
   + [Notas de la versión de Primetime Authentication 2.64](auth-rn-264.md)
   + [Notas de la versión de Primetime Authentication 2.63](auth-rn-263.md)
   + [Notas de la versión de la autenticación de Primetime iOS/tvOS 3.7.0](authn-rn-ios-tvos-370.md)
+ Notas técnicas {#tech-notes}
   + SDK de autenticación de Primetime {#primetime-authentication-sdks}
      + [Preguntas y respuestas sobre certificados](certificates-qa.md)
      + SDK de JavaScript {#javascript}
         + [Limitaciones del SDK de JS para el explorador Safari](js-sdk-limitations-for-safari-browser.md)
         + [Actualizaciones de cookies: indicadores SameSite y Secure](cookies-updates--samesite-and-secure-flags.md)
      + SDK para Android {#android}
         + [Acceso al inicio de sesión único (SSO) del SDK para Android de Enabler en aplicaciones Android 10](access-enabler-android-sdk-single-signon-sso-on-android-10-devices.md)
         + [Autenticación de Adobe Primetime y el nuevo modelo de permisos &quot;Marshmallow&quot; de Android 6](adobe-primetime-authentication-and-the-android-6-marshmallow-new-permissions-model.md)
      + SDK de iOS/tvOS {#iostvos}
         + [Compatibilidad con WKWebView en el SDK para iOS 3.1+](wkwebview-support-on-ios-sdk-31.md)
         + [Compatibilidad con SFSafariViewController en el SDK para iOS 3.2+](sfsafariviewcontroller-support-on-ios-sdk-32.md)
         + [SSO en iOS al utilizar el activador de acceso de autenticación de Primetime](sso-on-ios-when-using-the-primetime-authentication-access-enabler.md)
         + [Error de autenticación de iOS: no se puede encontrar adobepass.ios.app](ios-authentication-error-adobepassiosapp-cannot-be-found.md)
         + [Restaurar paso temporal en iOS](reset-temp-pass-on-ios.md)
         + [Depuración del SDK de iOS/tvOS de AccessEnabler mediante registros de aplicaciones de consola](debugging-the-accessenabler-iostvos-sdk-using-console-app-logs.md)
         + [Ruta de actualización de AccessEnabler iOS/tvOS 3.7.0](accessenabler-iostvos-370-upgrade-path.md)
   + Entornos de autenticación de Primetime {#primetime-authentication-environments}
      + [Explicación de los entornos de Adobe](understanding-the-adobe-environments.md)
      + [Configuración del entorno y pruebas en Pre-Qual](setting-up-your-environment-and-testing-in-prequal.md)
      + [Cómo probar los flujos de autenticación y autorización mediante el sitio de prueba de la API de Adobe](test-authn-authz-flows-using-adobes-api-test-site.md)
   + API sin cliente {#clientless-api}
      + [Implementación de API sin cliente: códigos de error/mensajes con motivo probable/causa](clientless-api-implementation-error-codes--messages-with-probable-reason--cause.md)
      + [Flujo de API sin cliente en ausencia de ID de dispositivo](clientless-api-flow-in-the-absence-of-device-id.md)
      + [Sin cliente: Evite utilizar &quot;&amp;&#39;reg_code en la solicitud /authentication](clientless-avoid-using-reg-code-in-authenticate-request.md)
      + [Habilitación de los servicios de derecho de Primetime para un programador en Xbox 360 y XboxOne sin clientes](enabling-primetime-entitlement-services-for-a-programmer-on-xbox-360-and-xboxone-clientless-solution.md)
      + [Tipo de dispositivo sin cliente y métricas](benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)
   + Experiencia del usuario {#user-exp}
      + [Cómo migrar la página de inicio de sesión de MVPD de iFrame a elemento emergente](migr-mvpd-login-iframe-popup.md)
      + [Función de comprobación preliminar: Cómo habilitar, solucionar o determinar el problema](preflight-feature.md)
   + Herramientas y utilidades {#tools-and-utilities}
      + [Uso de Charles Proxy](using-charles-proxy.md)
   + Conceptos {#concepts}
      + [Explicación de los ID de usuario](understanding-user-ids.md)
+ [Guía del usuario del TVE Dashboard](tve-dashboard-user-guide.md)
+ [Glosario](glossary.md)
