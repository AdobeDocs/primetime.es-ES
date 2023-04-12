---
title: SSO mediante autenticación pasiva
description: SSO mediante autenticación pasiva
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---


# SSO mediante autenticación pasiva

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.


## Introducción

El ámbito de este documento es describir la implementación del flujo de autenticación pasiva y cómo funciona con nuestro enfoque estándar de inicio de sesión único.

## Usecases

La autenticación de Adobe Primetime habilita el inicio de sesión único (SSO) entre aplicaciones y sitios. Después de que un usuario inicia sesión con sus credenciales de MVPD, la autenticación de Adobe Primetime genera un token seguro que representa la sesión de autenticación de MVPD y vincula dicho token al dispositivo del usuario mediante un ID de dispositivo. La autenticación de Adobe Primetime almacena el token/ID del dispositivo en un servidor o en el dispositivo.

Mientras el token siga siendo válido, los usuarios aparecerán directamente como autenticados. Esto permite a los usuarios introducir sus credenciales con menos frecuencia y mantener las transacciones seguras.



El caso de uso empresarial detallado aquí es un requisito muy específico: que el usuario DEBE estar autenticado al menos una vez por cada sitio visitado. Esto permite que el MVPD aplique reglas comerciales asociadas con la sesión authN que pueden variar por red. Está en conflicto con la promesa TVE actual de que un usuario debe iniciar sesión una sola vez y se autenticará en todos los sitios que forman parte del ecosistema de autenticación de Adobe Primetime.



Para mantener la regla comercial pero también mantener una buena experiencia de usuario, el MVPD NO requiere que un usuario proporcione manualmente información de credenciales. Podemos aprovechar la cookie de sesión establecida anteriormente e intentar realizar una nueva autenticación automática mediante el flujo pasivo; desde la perspectiva del usuario, aparecerá como si hubiera iniciado sesión automáticamente.



Para solucionarlos, implementamos dos características diferentes: autenticación por red y compatibilidad con autenticación pasiva. Los MVPD admitirán SAML passive authN donde simplemente vuelvan a autenticar a un usuario si existe una sesión authN en el IdP, independientemente del sitio en el que se haya creado la sesión.



## Autenticación por red

Esta función garantiza que el MVPD reciba una solicitud de autenticación una vez por cada sitio visitado. Esta funcionalidad significa que un token de autenticación de Adobe Primetime estará enlazado al requestorID, siendo válido solo para la red que lo solicitó. Como resultado, una vez que el usuario se autentique en el sitio &quot;A&quot; y luego visite el sitio &quot;B&quot;, será necesario autenticarse.



Tenga en cuenta que debido al hecho de que en el IdP de MVPD el usuario ya está autenticado, no se le exigirá que proporcione información de inicio de sesión, sino que el navegador simplemente se redirigirá del sitio &quot;B&quot; al IdP de MVPD y, a continuación, de nuevo. El mismo usuario se autenticará en el sitio &quot;A&quot; si regresa.



El siguiente flujo representa la función básica Autenticación por red :





## Autenticación pasiva

El objetivo de esto es hacer que el proceso de reautenticación se produzca en segundo plano sin necesidad de redireccionar el explorador completo y sin mostrar el selector. Como resultado, se autenticará automáticamente al usuario que se mueva del sitio A al sitio B.



Desde la perspectiva de UX no habrá diferencia entre este flujo y un flujo ejecutado con un MVPD normal. Lo que el usuario ve es que después de introducir credenciales como resultado de visitar el sitio A, se autenticará automáticamente en el sitio B.



Para que este flujo sea viable, el MVPD necesitará admitir la autenticación pasiva para que el iframe oculto no se &quot;atasque&quot; en la página de inicio de sesión en caso de que el MVPD ya no tenga una sesión. Esto se realiza mediante el atributo estándar &quot;isPassive&quot;.



En el diagrama siguiente se describe el flujo mejorado y la autenticación pasiva &quot;entre bastidores&quot;:





Ejemplo de solicitud SAML Este es un ejemplo de solicitud SAML para el flujo pasivo authN:


```xml
<saml2p:AuthnRequest xmlns:saml2p="urn:oasis:names:tc:SAML:2.0:protocol"
                     AssertionConsumerServiceURL="https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer"
                     Destination="https://mvpd_idp_url"
                     ForceAuthn="false"
                     ID="_15056686-399c-4528-b21a-4a9542cfc8ec"
                     IsPassive="true"
                     IssueInstant="2014-11-03T14:18:12.394Z"
                     ProtocolBinding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST"
                     Version="2.0"
                     >
    <saml2:Issuer xmlns:saml2="urn:oasis:names:tc:SAML:2.0:assertion">https://saml.sp.auth.adobe.com </saml2:Issuer>
    <saml2p:Extensions>
        <thrpty:RespondTo xmlns:thrpty="urn:oasis:names:tc:SAML:protocol:ext:third-party">https://saml.sp.auth.adobe.com</thrpty:RespondTo>
    </saml2p:Extensions>
    <saml2p:NameIDPolicy AllowCreate="true"
                         Format="urn:oasis:names:tc:SAML:2.0:nameid-format:transient"
                         SPNameQualifier="https://saml.sp.auth.adobe.com"
                         />
</saml2p:AuthnRequest>
```

Las reglas comerciales de los MVPD tienen restricciones específicas del dominio de creación de ámbitos de SSO. Por ejemplo, solo algunos dominios podían ser permitidos por algunos MVPD (SSO para la misma empresa de medios, pero no entre empresas).
Algunos MVPD pueden requerir que se apliquen reglas de autenticación diferentes. Por ejemplo, los MVPD pueden tener TTL de autenticación diferentes para redes diferentes. Además, los MVPD podrían habilitar la autenticación basada en el hogar para algunas redes, pero no para otras (los casos de uso de control parental están muy representados aquí).


Estos requisitos comerciales deben tener en cuenta que el caso de uso principal es que no se debe exigir al usuario que vuelva a iniciar sesión después de iniciar sesión correctamente con su MVPD.

Esto se puede lograr utilizando la autenticación por red con el indicador authN pasivo.



Limitaciones conocidas de iOS : debido a la naturaleza del almacenamiento local de iOS, los flujos SSO no funcionan en iOS para aplicaciones desarrolladas por diferentes proveedores. Para obtener más información sobre SSO en iOS 8 y versiones posteriores, consulte esta nota técnica.


<!--
>[!RELATEDINFORMATION]
>* Single Sign-On on iOS
>* SSO on iOS when using the Primetime authentication Access Enabler
-->