---
title: Autenticación MVPD
description: Autenticación MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1908'
ht-degree: 0%

---


# Autenticación MVPD {#mvpd-authn}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Información general {#mvpd-authn-overview}

La función de proveedor de servicios (SP) real la tiene un programador, pero la autenticación de Adobe Primetime sirve como proxy de SP para ese programador. El uso de la autenticación de Adobe Primetime como intermediario permite a los MVPD y a los programadores evitar tener que personalizar sus procesos de asignación de derechos caso por caso.

Los pasos siguientes presentan la secuencia de eventos, mediante la autenticación de Adobe Primetime, cuando un programador solicita la autenticación desde un MVPD que admite SAML. Tenga en cuenta que el componente Access Enabler de autenticación de Adobe Primetime está activo en el cliente del usuario/suscriptor. Desde allí, Access Enabler facilita todos los pasos del flujo de autenticación.

1. Cuando el usuario solicita acceso a contenido protegido, Access Enabler inicia la autenticación (AuthN) en nombre del programador (SP).
1. La aplicación del SP presenta un &quot;MVPD Picker&quot; al usuario para obtener su proveedor de televisión de pago (MVPD). A continuación, el SP redirige el navegador del usuario al servicio de proveedor de identidad (IdP) del MVPD seleccionado.  Esto es &quot;**Inicio de sesión iniciado por el programador**&quot;.  El MVPD envía la respuesta del IdP al servicio de consumo de afirmación SAML de Adobe, donde se procesa.
1. Por último, Access Enabler redirige el explorador de nuevo al sitio del SP, informando al SP del estado (éxito/error) de la solicitud de AuthN.

## La solicitud de autenticación {#authn-req}

Como se muestra en los pasos anteriores, durante el flujo AuthN un MVPD debe aceptar una solicitud AuthN basada en SAML y enviar una respuesta SAML AuthN.

La variable [Especificación de la Interfaz de Autorización y Autenticación de Acceso a Contenido en Línea (OLCA)](https://www.cablelabs.com/specifications/search?query=&amp;category=&amp;subcat=&amp;doctype=&amp;content=false&amp;archives=false){target=_blanck} presenta una solicitud y una respuesta estándar de AuthN. Aunque la autenticación de Adobe Primetime no requiere que los MVPD basen su mensajería de asignación de derechos en este estándar, consultar la especificación puede proporcionar información sobre los atributos clave necesarios para una transacción AuthN.

>[!NOTE]
>
>La solicitud AuthN que recibe un MVPD con la autenticación de Adobe Primetime contiene una firma digital. Sin embargo, el ejemplo siguiente no muestra una firma por motivos de brevedad. Para ver un ejemplo que muestre una firma digital, consulte el ejemplo en [la respuesta de autenticación](#authn-response) en las secciones siguientes.

Ejemplo de solicitud de autenticación SAML:

```XML
<?xml version="1.0" encoding="UTF-8"?>
<samlp:AuthnRequest  
    AssertionConsumerServiceURL=http://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer          
    Destination=http://idp.com/SSOService
    ForceAuthn="false"
    ID="_c0fc667e-ad12-44d6-9cae-bc7cf04688f8"
    IsPassive="false"
    IssueInstant="2010-08-03T14:14:54.372Z"
    ProtocolBinding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST"
    Version="2.0"
    xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
        http://saml.sp.adobe.adobe.com
    </saml:Issuer>
    <ds:Signature xmlns:ds=_signature_block_goes_here_
    </ds:Signature>
    <samlp:NameIDPolicy
        AllowCreate="true"
        Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"
        SPNameQualifier="http://saml.sp.adobe.adobe.com"/>
</samlp:AuthnRequest> 
```

La tabla siguiente explica los atributos y las etiquetas que deben estar en una solicitud de autenticación, con los valores esperados predeterminados.

**Detalles de la solicitud de autenticación SAML**

| samlp:AuthnRequest | &lt;authnrequest> emitido por el proveedor de servicios al proveedor de identidad. |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AssertionConsumerServiceURL | Este es el punto final del Adobe que se utilizará en la respuesta posterior. Valor predeterminado: **http://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer** |
| Destino | Una referencia URI que indica la dirección a la que se ha enviado esta solicitud. Esto resulta útil para evitar el reenvío malintencionado de solicitudes a destinatarios no deseados, una protección requerida por algunos enlaces de protocolo. Si está presente, el destinatario real DEBE comprobar que la referencia URI identifique la ubicación en la que se recibió el mensaje. Si no es así, la solicitud DEBE descartarse. Algunos enlaces de protocolo pueden requerir el uso de este atributo. |
| ForceAuthn | El atributo ForceAuthn, si está presente con el valor true, obliga al proveedor de identidad a establecer esta identidad de forma reciente, en lugar de basarse en una sesión existente que pueda tener con la entidad de seguridad. |
| ID | Identificador de la solicitud. Consulte [SAML core 2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} para más detalles. |
| IsPassive | Un valor booleano. Si es &quot;true&quot;, el proveedor de identidad y el propio agente de usuario NO DEBEN tomar visiblemente el control de la interfaz de usuario del solicitante e interactuar con él de una manera visible. Si no se proporciona un valor, el valor predeterminado es &quot;false&quot;. |
| IssueInstant | Momento en que se emite la respuesta. El valor de tiempo se codifica en UTC como se describe en [SAML core 2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} Sección 1.3.3. |
| EnlaceDeProtocolo | Una referencia URI que identifica un enlace de protocolo SAML que se va a usar al devolver el &lt;response> mensaje. Consulte [SAMLBind] para obtener más información sobre enlaces de protocolo y referencias de URI definidas para ellos. Valor predeterminado : urn:oasis:name:tc:SAML:2.0:bindings:POST HTTP |
| Versión | Versión de esta solicitud. |
| saml:issuer | Identifica la entidad que generó el mensaje de respuesta. (Para obtener más información sobre este elemento, consulte SAML core 2.0-os Section 2.2.5) |
| ds:Signature | Firma XML que protege la integridad y autentica al emisor de la afirmación, como se describe en la sección 5 de SAML core 2.0-os |
| samlp:NameIDPolicy | Especifica restricciones en el identificador de nombre que se utilizará para representar el asunto solicitado. |
| AllowCreate | Un valor booleano que se utiliza para indicar si el proveedor de identidad está autorizado, durante el cumplimiento de la solicitud, a crear un nuevo identificador para representar la entidad de seguridad. Predeterminado: true |
| Formato | Especifica la referencia URI correspondiente a un formato de identificador de nombre Predeterminado: urn:oasis:name:tc:SAML:2.0:nameid-format:transient Adobe recomienda: urn:oasis:name:tc:SAML:2.0:nameid-format:persistente |
| SPNameQualifier | De forma opcional, especifica que el identificador del sujeto de afirmación se devuelva (o se cree) en el espacio de nombres de un proveedor de servicios que no sea el solicitante. Predeterminado : http://saml.sp.adobe.adobe.com |

## La respuesta de autenticación {#authn-response}

Una vez recibida y gestionada la solicitud de autenticación, el MVPD debe enviar ahora una respuesta de autenticación.

**Ejemplo de respuesta de autenticación SAML**

```XML
<?xml version="1.0" encoding="UTF-8"?> 
<samlp:Response Destination="https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer"
                ID="_0ac3a9dd5dae0ce05de20912af6f4f83a00ce19587"                             
                InResponseTo="_c0fc667e-ad12-44d6-9cae-bc7cf04688f8"
                IssueInstant="2010-08-17T11:17:50Z" Version="2.0"              
                xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion"
                xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"
                xmlns:xs="http://www.w3.org/2001/XMLSchema"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
             http://idp.com/SSOService
    </saml:Issuer>
    <samlp:Status>
       <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
    </samlp:Status>
    <saml:Assertion ID="pfxb0662d76-17a2-a7bd-375f-c11046a86742"
                   IssueInstant="2010-08-17T11:17:50Z"
                   Version="2.0">
        <saml:Issuer>http://idp.com/SSOService</saml:Issuer>
        <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
          <ds:SignedInfo>
            <ds:CanonicalizationMethod
                     Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>
            <ds:SignatureMethod
                     Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>
            <ds:Reference URI="#pfxb0662d76-17a2-a7bd-375f-c11046a86742">
              <ds:Transforms>
                 <ds:Transform
                    Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>        
                 <ds:Transform
                            Algorithm=http://www.w3.org/2001/10/xml-exc-c14n#"/>
              </ds:Transforms>
              <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>
              <ds:DigestValue>LgaPI2ASx/fHsoq0rB15Zk+CRQ0=</ds:DigestValue>
            </ds:Reference>
          </ds:SignedInfo>
          <ds:SignatureValue>
                POw/mCKF__shortened_for_brevity__9xdktDu+iiQqmnTs/NIjV5dw==
          </ds:SignatureValue>
          <ds:KeyInfo>
            <ds:X509Data>
                <ds:X509Certificate>
                 MIIDVDCCAjygAwIBA__shortened_for_brevity_utQ==
                </ds:X509Certificate>
            </ds:X509Data>
          </ds:KeyInfo>
      </ds:Signature>
      <saml:Subject>
        <saml:NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"
                     SPNameQualifier="https://saml.sp.auth.adobe.com">
            _5afe9a437203354aa8480ce772acb703e6bbb8a3ad
        </saml:NameID>
        <saml:SubjectConfirmation
                     Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
            <saml:SubjectConfirmationData
                  InResponseTo="_c0fc667e-ad12-44d6-9cae-bc7cf04688f8"
                  NotOnOrAfter="2010-08-17T11:22:50Z"                                          
                  Recipient="https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer"/>
           </saml:SubjectConfirmation>
       </saml:Subject>
       <saml:Conditions NotBefore="2010-08-17T11:17:20Z"
                        NotOnOrAfter="2010-08-17T19:17:50Z">
           <saml:AudienceRestriction>
              <saml:Audience>https://saml.sp.auth.adobe.com</saml:Audience>
           </saml:AudienceRestriction>
       </saml:Conditions>
       <saml:AuthnStatement AuthnInstant="2010-08-17T11:17:50Z"
                   SessionIndex="_1adc7692e0fffbb1f9b944aeafce62aaa7d770cd9e">
        <saml:AuthnContext>
            <saml:AuthnContextClassRef>
                   urn:oasis:names:tc:SAML:2.0:ac:classes:Password
            </saml:AuthnContextClassRef>
        </saml:AuthnContext>
    </saml:AuthnStatement>
  </saml:Assertion>
</samlp:Response>
```


En el ejemplo anterior, el SP de Adobe espera recuperar el ID de usuario fuera del Subject/NameId. El SP de Adobe se puede configurar para obtener el ID de usuario de un atributo definido personalizado; la respuesta debe contener un elemento como el siguiente:

```XML
<saml:AttributeStatement>
     <saml:Attribute Name="guid" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
         <saml:AttributeValue xsi:type="xs:string">
               71C69B91-F327-F185-F29E-2CE20DC560F5
         </saml:AttributeValue>
    </saml:Attribute>
</saml:AttributeStatement>
```

**Detalles de la respuesta de autenticación SAML**
| samlp:Response | Respuesta recibida por la autenticación de Adobe Primetime.                                                                                                                                                                                                                                                                                                                                                                                                                       | |—|—| | Destino | Una referencia URI que indica la dirección a la que se ha enviado esta solicitud. Esto resulta útil para evitar el reenvío malintencionado de solicitudes a destinatarios no deseados, una protección requerida por algunos enlaces de protocolo. Si está presente, el destinatario real DEBE comprobar que la referencia URI identifique la ubicación en la que se recibió el mensaje. Si no es así, la solicitud DEBE descartarse. Algunos enlaces de protocolo pueden requerir el uso de este atributo. | | ID | Identificador de la solicitud. Es de tipo xs:ID y DEBE seguir los requisitos especificados en la sección 1.3.4 de [SAML core 2.0-os](http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf){target=_blank} para la exclusividad del identificador. Los valores del atributo ID de una solicitud y del atributo InResponseTo de la respuesta correspondiente DEBEN coincidir.                                                                                                                                                                                         | | InResponseTo | El ID de un mensaje de protocolo SAML en respuesta al cual una entidad certificadora puede presentar la afirmación. El valor debe ser igual al del atributo de ID enviado en la solicitud de autenticación. Consulte SAML core 2.0-os | | IssueInstant | El momento en que se emite la solicitud.                                                                                                                                                                                                                                                                                                                                                                                                                                  | | Versión | Versión de la solicitud.                                                                                                                                                                                                                                                                                                                                                                                                                                                | | saml:Emitido | Identifica la entidad que generó el mensaje de solicitud. (Para obtener más información sobre este elemento, consulte Sección 2.2.5. SAML core 2.0-os ) | | samlp:Status | Código que representa el estado de la solicitud correspondiente.                                                                                                                                                                                                                                                                                                                                                                                                               | | ejemplo:StatusCode | Código que representa el estado de la actividad realizada en respuesta a la solicitud correspondiente.                                                                                                                                                                                                                                                                                                                                                                       | | saml:Assertion | Este tipo especifica la información básica común a todas las aserciones.                                                                                                                                                                                                                                                                                                                                                                                                        | | ID | Identificador de esta afirmación.                                                                                                                                                                                                                                                                                                                                                                                                                                         | | Versión | La versión de esta afirmación.                                                                                                                                                                                                                                                                                                                                                                                                                                             | | IssueInstant | El momento en que se emite la solicitud.                                                                                                                                                                                                                                                                                                                                                                                                                                  | | ds:Signature | Firma XML que protege la integridad y autentica al emisor de la afirmación, tal como se describe en la sección 5 de SAML core 2.0-os | | ds:SignedInfo | La estructura de SignedInfo incluye el algoritmo de canonicalización, un algoritmo de firma y una o más referencias. El elemento SignedInfo puede contener un atributo de ID opcional que permitirá que otras firmas y objetos hagan referencia a él. Consulte Sintaxis y procesamiento de firmas XML | | ds:CanonicalizationMethod | CanonicalizationMethod es un elemento obligatorio que especifica el algoritmo de canonicalización aplicado al elemento SignedInfo antes de realizar cálculos de firma. Consulte Sintaxis y procesamiento de firmas XML | | ds:SignatureMethod | SignatureMethod es un elemento obligatorio que especifica el algoritmo utilizado para la generación y validación de firmas. Este algoritmo identifica todas las funciones criptográficas involucradas en la operación de firma (por ejemplo, hash, algoritmos de claves públicas, MAC, relleno, etc.) Consulte Sintaxis y procesamiento de firmas XML | | ds:Reference | La referencia es un elemento que puede producirse una o más veces. Especifica un algoritmo de compendio y un valor de compendio, y opcionalmente un identificador del objeto que se va a firmar, el tipo del objeto y/o una lista de transformaciones que se van a aplicar antes de la compendio. Consulte Sintaxis y procesamiento de firmas XML | | ds:Transforms | El elemento opcional Transforms contiene una lista ordenada de elementos Transform . en estos se describe cómo el firmante obtuvo el objeto de datos que se recopiló. El resultado de cada transformación sirve como entrada para la siguiente transformación. La entrada en la primera transformación es el resultado de hacer referencia al atributo URI del elemento Reference . El resultado de la última transformación es la entrada del algoritmo DigestMethod. Consulte Sintaxis y procesamiento de firmas XML | | ds:DigestMethod | DigestMethod es un elemento obligatorio que identifica el algoritmo de compendio que se aplicará al objeto firmado. Consulte Sintaxis y procesamiento de firmas XML | | ds:DigestValue | DigestValue es un elemento que contiene el valor codificado del compendio. El compendio siempre se codifica usando base64. Consulte Sintaxis y procesamiento de firmas XML | | ds:SignatureValue | El elemento SignatureValue contiene el valor real de la firma digital; siempre se codifica usando base64. Consulte Sintaxis y procesamiento de firmas XML | | ds:KeyInfo | KeyInfo es un elemento opcional que permite a los destinatarios obtener la clave necesaria para validar la firma. Consulte Sintaxis y procesamiento de firmas XML | | ds:X509Data | Un elemento de datos X509dentro de KeyInfo contiene uno o más identificadores de claves o certificados X509. Consulte Sintaxis y procesamiento de firmas XML | | ds: Certificado X509 | El elemento X509Certificate, que contiene una codificación base64 [X509v3] certificate | | saml:Subject | El objeto de la declaración o declaraciones de la afirmación.                                                                                                                                                                                                                                                                                                                                                                                                                          | | saml:NameID | El &lt;nameid> El elemento es de tipo NameIDType (ver sección 2.2.2 en SAML core 2.0-os) y se utiliza en varias construcciones de afirmación SAML como la &lt;subject> y &lt;subjectconfirmation> y en varios mensajes de protocolo.                                                                                                                                                                                                                                           | | Formato | Una referencia URI que representa la clasificación de la información de identificador basada en cadenas.                                                                                                                                                                                                                                                                                                                                                                                    | | SPNameQualifier | Además, califica un nombre con el nombre de un proveedor de servicios o afiliación de proveedores. Este atributo proporciona un medio adicional para federar nombres en función de la parte o partes que confían en él.                                                                                                                                                                                                                                                                      | | saml:SubjectConfirmation | Información que permite confirmar el asunto. Si se proporciona más de una confirmación de sujeto, entonces la satisfacción de cualquiera de ellos es suficiente para confirmar el sujeto a los efectos de la aplicación de la afirmación.                                                                                                                                                                                                                                                    | | saml:SubjectConfirmationData | Información de confirmación adicional que se utilizará con un método de confirmación específico. Por ejemplo, el contenido típico de este elemento puede ser un <!--<ds:KeyInfo>--> tal como se define en la especificación de Sintaxis de firma XML y Procesamiento | | NotOnOrAfter | Un momento en el que el sujeto ya no puede ser confirmado.                                                                                                                                                                                                                                                                                                                                                                                                            | | Destinatario | Un URI que especifica la entidad o la ubicación a la que una entidad certificadora puede presentar la afirmación. Por ejemplo, este atributo podría indicar que la afirmación debe entregarse a un punto final de red específico para evitar que un intermediario la redirija a otro lugar.                                                                                                                                                                                   | | saml:Conditions | El &lt;condition> sirve como punto de extensión para nuevas condiciones.                                                                                                                                                                                                                                                                                                                                                                                                   | | NotBefore | El atributo NotBefore especifica el momento en que comienza el intervalo de validez.                                                                                                                                                                                                                                                                                                                                                                                  | | saml:AudienceRestriction | El &lt;audiencerestriction> element especifica que la afirmación está dirigida a una o más audiencias específicas identificadas por &lt;audience> elementos.                                                                                                                                                                                                                                                                                                                           | | saml:Audience | Una referencia URI que identifica una audiencia objetivo.                                                                                                                                                                                                                                                                                                                                                                                                                      | | saml:AuthnStatement | Una instrucción de autenticación.                                                                                                                                                                                                                                                                                                                                                                                                                                               | | AuthnInstant | Especifica la hora a la que se realizó la autenticación.                                                                                                                                                                                                                                                                                                                                                                                                                 | | SessionIndex | Especifica el índice de una sesión determinada entre el principal identificado por el sujeto y la autoridad autenticadora.                                                                                                                                                                                                                                                                                                                                              | | saml:AuthnContext | El contexto utilizado por la autoridad autenticadora hasta el evento de autenticación que produjo esta instrucción, incluido el que lo produjo.                                                                                                                                                                                                                                                                                                                                                 | | saml:AuthnContextClassRef | Una referencia URI que identifica una clase de contexto de autenticación que describe la declaración de contexto de autenticación que sigue. |