---
title: Autorización de MVPD
description: Autorización de MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---


# Autorización de MVPD

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Información general {#mvpd-authz-overview}

La autorización (AuthZ) se realiza a través de comunicaciones de canal trasero (servidor a servidor) entre un servidor back-end alojado en Adobe y el extremo MVPD AuthZ.

Para las solicitudes AuthZ, el extremo de autorización debe poder procesar al menos los siguientes parámetros:

* **Uid**. El ID de usuario recibido desde el paso de autenticación.

* **ID de recurso**. Cadena que identifica un recurso de contenido determinado. El programador especifica este ID de recurso y el MVPD debe reforzar las reglas comerciales de estos recursos (por ejemplo, comprobando que el usuario está suscrito a un canal determinado).

Además de determinar si el usuario está autorizado, la respuesta debe incluir el tiempo de vida (TTL) de esta autorización, es decir, el momento en que caduca la autorización. Si no se establece el TTL, la solicitud AuthZ fallará.  Por este motivo, **el TTL es una configuración obligatoria en el lado de la autenticación de Adobe Primetime**, para cubrir el caso en el que un MVPD no incluya el TTL en su solicitud.

## La solicitud de autorización {#authz-req}

Una solicitud de AuthZ debe incluir un asunto en cuyo nombre se realiza la solicitud, los recursos a los que el sujeto intenta acceder, la acción que el sujeto intenta realizar en el recurso y el entorno en el que está a punto de realizarse la operación. En el caso concreto de la autenticación Adobe Primetime, estos elementos corresponden a:

| Elemento XACML | Corresponde a |
|---------------|--------------------------------------------------------------------------------------------------------------------------------|
| Asunto | El principal identificado por la sesión autenticada, al que se hace referencia mediante el AttributeValue &quot;subject-token&quot; de la aserción SAML. |
| Recurso | URI del recurso protegido. |
| Acción | VER. |
| Entorno | Incluye la dirección IP del cliente solicitante, tal como lo ve el SP. |



En este punto, el SP debe preparar una consulta de decisión de autorización XACML y enviarla (a través del POST HTTP) al punto de decisión de directiva (previamente acordado) (PDP) para el IdP. A continuación se muestra un ejemplo de una solicitud XACML simple (consulte la especificación principal XACML):

```XML
POST https://authz.site.com/XACML_endpoint
<Request  xmlns="urn:oasis:names:tc:xacm:2.0:context:schema:os"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="urn:oasis:names:tc:xacml:2.0:context:schema:os
http://docs.oasis-open.org/xacml/access_control-xacml-2.0-context-schema-os.xsd">
<Subject>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:subject:subject-token"
        DataType="http://www.w3.org/2001/XMLSchema#base64Binary">
      <AttributeValue>{Base64 Data}</AttributeValue>
   </Attribute>
</Subject>
<Resource>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id"
        DataType="http://www.w3.org/2001/XMLSchema#anyURI">
<AttributeValue>urn:tve:tms:1234</AttributeValue>
   </Attribute>
</Resource>
<Action>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:action:action-id"
        DataType="http://www.w3.org/2001/XMLSchema#string">
       <AttributeValue>VIEW</AttributeValue>
   </Attribute>
</Action>
<Environment>
   <Attribute
       AttributeId="urn:oasis:names:tc:xacml:1.0:subject:authn-locality:ip-address"
       DataType="http://www.w3.org/2001/XMLSchema#string">
      <AttributeValue>1.2.3.4</AttributeValue>
   </Attribute>
</Environment>
</Request>
```


Después de recibir la solicitud AuthZ, el PDP de MVPD evalúa la solicitud y determina si se debe permitir que el sujeto realice la acción solicitada en el recurso. A continuación, el MVPD devuelve una respuesta con una Decisión, un código de estado y un mensaje, tal como se describe en la respuesta de autorización que aparece a continuación.

## La respuesta de autorización {#authz-response}

La respuesta a la solicitud AuthZ se produce después de que el MVPD evalúe la solicitud y aplique las reglas comerciales solicitadas para determinar si el sujeto puede realizar la acción solicitada en el recurso . La respuesta devuelta a la autenticación de Adobe Primetime se expresa de nuevo siguiendo la especificación principal XACML con una Decisión, un código de estado, un mensaje y las obligaciones que el SP tiene como punto de aplicación de políticas (PEP). La siguiente es una respuesta de ejemplo:

```XML
<Response xmlns="urn:oasis:names:tc:xacml:2.0:context:schema:os">
  <Result>
  <Decision>Permit</Decision>
  <Status>
     <StatusCode Value="urn:oasis:names:tc:xacml:1.0:status:ok"/>
     <StatusMessage>ok</StatusMessage>
  </Status>
  <xacml:Obligations     
          xmlns:xacml="urn:oasis:names:tc:xacml:2.0:policy:schema:os">
     <xacml:Obligation    
              ObligationId="urn:cablelabs:olca:1.0:obligations:log"
              FulfillOn="Permit" />
  </xacml:Obligations>
 </Result>
</Response>
```

A continuación se muestra una lista de obligaciones DENY que la autenticación de Adobe Primetime admite y permite a los programadores cumplir:

* **urn:tve:xacml:2.0:obligations:restrict-pc** - El suscriptor ha fallado en una comprobación de control parental y el SP debe tomar las medidas adecuadas para restringir el acceso a este contenido.

* **urn:tve:xacml:2.0:obligations:actualización** - El suscriptor no tiene un nivel de suscripción adecuado.  Debe actualizar la suscripción para acceder al contenido.

La autenticación de Adobe Primetime admite lo siguiente **PERMISO** Obligaciones y permite a los programadores cumplirlas:

* **urn:cablelabs:olca:1.0:obligations:log** - Adobe Pass registra la transacción y puede estar disponible a través del mecanismo de informes acordado.

* **urn:cablelabs:olca:1.0:obligations:reauthz** - La autenticación de Adobe Primetime actualiza la autorización de nuevo en n segundos (especificado como argumento a la Obligación a través de una Asignación de Atributo XACML - consulte la especificación principal XACML , Sección 5.46).

<!--
>![RelatedInformation]
>* [Preflight Authorization](/help/authentication/preflight-authz.md)
>* [Authentication](/help/authentication/authn-usecase.md)
-->