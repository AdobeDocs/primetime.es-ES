---
description: Para empezar a utilizar Primetime DRM Cloud, con la tecnología ExpressPlay, debe configurar las cuentas de Adobe Cert y ExpressPlay con la ayuda de su representante de Adobe.
seo-description: Para empezar a utilizar Primetime DRM Cloud, con la tecnología ExpressPlay, debe configurar las cuentas de Adobe Cert y ExpressPlay con la ayuda de su representante de Adobe.
seo-title: Obtener aprovisionamiento (cuentas, etc.)
title: Obtener aprovisionamiento (cuentas, etc.)
uuid: 51b95676-2121-4d8b-8756-9fd097185a13
translation-type: tm+mt
source-git-commit: 9792aff8586c46aabb5bfb70864cfe98c28e602d
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# Obtener aprovisionamiento (cuentas, etc.) {#get-provisioned-accounts-etc}

Para empezar a utilizar Primetime DRM Cloud, con la tecnología ExpressPlay, debe configurar las cuentas de Adobe Cert y ExpressPlay con la ayuda de su representante de Adobe.

1. Póngase en contacto con su representante de Adobe y solicite las cuentas de Adobe Cert y ExpressPlay que necesitará para implementar Multi-DRM con TVSDK.

       Proporcione a su representante de Adobe la dirección de correo electrónico que utilizará como punto de contacto. A continuación, Adobe crea dos cuentas para usted:
   
   * ***Cuenta***  de portal de certificados- ( <span></span>https://certportal.primetime.adobe.com): El  *equipo de gestión de inscripciones de certificados de DRM / Acceso a Adobe* Primetime envía un correo electrónico a las direcciones que les ha proporcionado. El correo electrónico incluye la URL del portal de certificados de Adobe, junto con un vínculo a la documentación de inscripción de certificados de Adobe (los documentos más recientes están aquí: [Guía de inscripción de certificados](../../../digital-rights-management/certificate-enrollment-guide/about-certs.md)).

   * ***Cuenta***  ExpressPlay: Adobe le envía un correo electrónico que contiene un vínculo que utiliza para registrarse en su cuenta de administrador de ExpressPlay.

1. Inicie sesión en el portal de certificados de Adobe con su Adobe ID (utilice la misma dirección de correo electrónico que proporcionó a su representante de Adobe). Si todavía no tiene un Adobe ID, puede crear uno rápidamente siguiendo el vínculo *Obtener un Adobe ID* desde el portal de certificados:

   <!--<a id="fig_mst_gtj_wv"></a>-->

   ![](assets/cert_portal_sign-in-page-web.png)

1. En el portal de certificados de Adobe, solicite un *certificado de prueba*.

   Para la prueba con varios DRM, un certificado de prueba único cubrirá todos estos aspectos de la protección del contenido: embalaje, licencia y transporte. Deberá proporcionar su propio [CSR](../../../digital-rights-management/certificate-enrollment-guide/request-certs/gen-cert-signing-req.md) para realizar una solicitud de certificado:
   <!--<a id="fig_op1_xwj_wv"></a>-->

   ![](assets/cert_portal_trial_request-web.png)

   Adobe le enviará un mensaje de correo electrónico que indica la aceptación o el rechazo de su solicitud de certificado. Puede ver el estado de las solicitudes de certificados en la ficha *Historial de solicitudes* del portal de certificados:
   <!--<a id="fig_gkl_myj_wv"></a>-->

   ![](assets/cert_portal_request_history-web.png)

1. Cree su cuenta de administrador de ExpressPlay.

   Siga el vínculo a ExpressPlay que le proporcionó el Adobe. Se abre la página *Crear una cuenta* en ExpressPlay. Rellene la información requerida y envíe el formulario. Recibirá un mensaje de correo electrónico de `operations@expressplay.com` que contiene un vínculo de activación válido durante una semana. Después de activarlo, configure el servicio ExpressPlay:
   <!--<a id="fig_cjl_ztk_wv"></a>-->

   ![](assets/expressplay_create_service-web.png)

   Cuando haya creado el servicio, se le presentará su propia página de administración. Junto con algunos campos de seguimiento de actividades, verá los *autenticadores de cliente* (claves de API) y las direcciones URL de servicio de producción y prueba:

   <!--<a id="fig_c5h_xdl_wv"></a>-->

   ![](assets/expressplay_admin_dashboard_2-web.png) ![](assets/expressplay_admin_dashboard-web.png)

1. Si utiliza FairPlay, hay que seguir algunos pasos adicionales (en el sitio para desarrolladores de Apple) para configurar ExpressPlay. Consulte [Habilitar el servicio ExpressPlay para FairPlay](../../multi-drm-workflows/p-l-and-p/fairplay-workflow.md#enable-expressplay-service-for-fairplay) para obtener instrucciones.
