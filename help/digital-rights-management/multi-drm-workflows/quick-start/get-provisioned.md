---
description: Para empezar a usar Primetime DRM Cloud, con tecnología ExpressPlay, debe configurar las cuentas de certificado de Adobe y ExpressPlay con la ayuda de su representante de Adobe.
title: Aprovisionamiento (cuentas, etc.)
exl-id: 2543d997-3495-4545-9395-072c07431aba
source-git-commit: a0917e128862184ce18050792c2ee2ac265050d2
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# Aprovisionamiento (cuentas, etc.) {#get-provisioned-accounts-etc}

Para empezar a usar Primetime DRM Cloud, con tecnología ExpressPlay, debe configurar las cuentas de certificado de Adobe y ExpressPlay con la ayuda de su representante de Adobe.

1. Póngase en contacto con su representante de Adobe y solicite el certificado de Adobe y las cuentas ExpressPlay que necesitará para implementar Multi-DRM con TVSDK.

   Proporcione a su representante de Adobe la dirección de correo electrónico que utilizará como punto de contacto. A continuación, Adobe crea dos cuentas para usted:

   * ***Cuenta del portal de certificados*** - ( https://certportal.primetime.adobe.com) : La *Acceso de Adobe / Equipo de administración de inscripción de certificados DRM de Primetime* envía un correo electrónico a las direcciones que les proporcionó. El correo electrónico incluye la dirección URL del portal de certificados de Adobe, junto con un vínculo a la documentación de inscripción de certificados de Adobe (los documentos más recientes se encuentran aquí: [Guía de inscripción de certificados](../../../digital-rights-management/certificate-enrollment-guide/about-certs.md)).

   * ***Cuenta de ExpressPlay*** - Adobe te envía un correo electrónico que contiene un enlace que utilizas para registrarte en tu cuenta de administrador de ExpressPlay.

1. Inicie sesión en el portal del certificado de Adobe con su Adobe ID (utilice la misma dirección de correo electrónico que indicó a su representante de Adobe). Si todavía no tiene una Adobe ID, puede crearla rápidamente siguiendo los pasos de *Obtener un Adobe ID* vínculo desde el portal del certificado:

   <!--<a id="fig_mst_gtj_wv"></a>-->

   ![](assets/cert_portal_sign-in-page-web.png)

1. En el portal del certificado de Adobe, solicite una *Prueba* certificado.

   Para la prueba Multi-DRM, un único certificado de prueba cubrirá todos estos aspectos de la protección de contenido: embalaje, licencias y transporte. Tendrá que suministrar los suyos propios [CSR](../../../digital-rights-management/certificate-enrollment-guide/request-certs/gen-cert-signing-req.md) para realizar una solicitud de certificado:
   <!--<a id="fig_op1_xwj_wv"></a>-->

   ![](assets/cert_portal_trial_request-web.png)

   El Adobe le enviará un correo electrónico en el que se indica la aceptación o el rechazo de su solicitud de certificado. Puede ver el estado de las solicitudes de certificado en la *Historial de solicitudes* en el portal del certificado:
   <!--<a id="fig_gkl_myj_wv"></a>-->

   ![](assets/cert_portal_request_history-web.png)

1. Cree su cuenta de administrador de ExpressPlay.

   Siga el enlace a ExpressPlay que el Adobe le proporcionó. Esto abre el *Crear una cuenta* página en ExpressPlay. Rellene la información necesaria y envíe el formulario. Recibirá un correo electrónico de `operations@expressplay.com` que contenga un vínculo de activación válido durante una semana. Después de activar, configure el servicio ExpressPlay:
   <!--<a id="fig_cjl_ztk_wv"></a>-->

   ![](assets/expressplay_create_service-web.png)

   Cuando haya creado el servicio, se le mostrará su propia página de administración. Junto con algunos campos de seguimiento de actividad, verá su Producción y prueba *autenticadores de cliente* (claves de API) y las URL de los servicios de producción y prueba:

   <!--<a id="fig_c5h_xdl_wv"></a>-->

   ![](assets/expressplay_admin_dashboard_2-web.png) ![](assets/expressplay_admin_dashboard-web.png)

1. Si utiliza FairPlay, hay pasos adicionales involucrados (en el sitio para desarrolladores de Apple) para configurar ExpressPlay. Consulte [Habilitar el servicio ExpressPlay para FairPlay](../../multi-drm-workflows/p-l-and-p/fairplay-workflow.md#enable-expressplay-service-for-fairplay) para obtener instrucciones.
