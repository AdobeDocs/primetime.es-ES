---
description: Para comenzar con Primetime DRM Cloud, con tecnología ExpressPlay, debe configurar las cuentas de Adobe Cert y ExpressPlay con la ayuda de su representante de Adobe.
title: Obtener aprovisionado (cuentas, etc.)
exl-id: 2543d997-3495-4545-9395-072c07431aba
source-git-commit: a0917e128862184ce18050792c2ee2ac265050d2
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# Obtener aprovisionado (cuentas, etc.) {#get-provisioned-accounts-etc}

Para comenzar con Primetime DRM Cloud, con tecnología ExpressPlay, debe configurar las cuentas de Adobe Cert y ExpressPlay con la ayuda de su representante de Adobe.

1. Póngase en contacto con su representante de Adobe y solicite las cuentas de Adobe Cert y ExpressPlay que necesite para implementar Multi-DRM con TVSDK.

   Proporcione a su representante de Adobe la dirección de correo electrónico que utilizará como punto de contacto. A continuación, Adobe crea dos cuentas para usted:

   * ***Cuenta del portal de certificados*** - ( https://certportal.primetime.adobe.com) : La variable *Equipo de administración de inscripciones de certificados DRM de acceso a Adobe/Primetime* envía un correo electrónico a las direcciones que les ha proporcionado. El correo electrónico incluye la dirección URL del portal de certificados de Adobe, junto con un vínculo a la documentación de inscripción de certificados de Adobe (los documentos más recientes están aquí: [Guía de inscripción de certificado](../../../digital-rights-management/certificate-enrollment-guide/about-certs.md)).

   * ***Cuenta de ExpressPlay*** - Adobe le envía un correo electrónico que contiene un vínculo que utiliza para registrarse en su cuenta de administrador de ExpressPlay.

1. Inicie sesión en el portal de certificados de Adobe con su Adobe ID (utilice la misma dirección de correo electrónico que le proporcionó al representante de Adobe). Si todavía no tiene un Adobe ID, puede crearlo rápidamente siguiendo la *Obtener una Adobe ID* enlace desde el portal de cert:

   <!--<a id="fig_mst_gtj_wv"></a>-->

   ![](assets/cert_portal_sign-in-page-web.png)

1. En el portal de certificados de Adobe, solicite un *Prueba* cert.

   Para la prueba Multi-DRM, un certificado de prueba único cubrirá todos estos aspectos de la protección de contenido: embalaje, licencia y transporte. Tendrá que suministrar su propio [CSR](../../../digital-rights-management/certificate-enrollment-guide/request-certs/gen-cert-signing-req.md) para realizar una solicitud de certificado:
   <!--<a id="fig_op1_xwj_wv"></a>-->

   ![](assets/cert_portal_trial_request-web.png)

   Adobe le enviará un correo electrónico que indica la aceptación o el rechazo de su solicitud de certificado. Puede ver el estado de sus solicitudes de certificado en el *Historial de solicitudes* en el portal del certificado:
   <!--<a id="fig_gkl_myj_wv"></a>-->

   ![](assets/cert_portal_request_history-web.png)

1. Cree su cuenta de administrador de ExpressPlay.

   Siga el enlace a ExpressPlay que le proporcionó el Adobe. Esto abre el *Crear una cuenta* en ExpressPlay. Rellene la información requerida y envíe el formulario. Recibirá un correo electrónico de `operations@expressplay.com` que contenga un vínculo de activación válido durante una semana. Después de la activación, configure el servicio ExpressPlay:
   <!--<a id="fig_cjl_ztk_wv"></a>-->

   ![](assets/expressplay_create_service-web.png)

   Cuando haya creado el servicio, se le presentará su propia página de administración. Junto con algunos campos de seguimiento de actividades, verá su Producción y prueba *autenticadores de cliente* (Claves de API) y las URL del servicio de producción y prueba:

   <!--<a id="fig_c5h_xdl_wv"></a>-->

   ![](assets/expressplay_admin_dashboard_2-web.png) ![](assets/expressplay_admin_dashboard-web.png)

1. Si utiliza FairPlay, hay que seguir algunos pasos adicionales (en el sitio para desarrolladores de Apple) para configurarlo con ExpressPlay. Consulte [Habilitar el servicio ExpressPlay para FairPlay](../../multi-drm-workflows/p-l-and-p/fairplay-workflow.md#enable-expressplay-service-for-fairplay) para obtener instrucciones.
