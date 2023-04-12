---
title: Autorización de comprobación preliminar de MVPD
description: Autorización de comprobación preliminar de MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---


# Autorización de comprobación preliminar de MVPD

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Introducción {#mvpd-preflight-authz-intro}

&quot;Autorización de comprobación previa&quot; es una comprobación de autorización ligera para varios recursos. Los programadores lo utilizan principalmente para decorar sus IU (por ejemplo, indicar el estado de acceso con los iconos de bloqueo y desbloqueo).

Actualmente, la autenticación de Adobe Primetime puede admitir la autorización previa de dos maneras para los MVPD, ya sea a través de atributos de respuesta AuthN o a través de una solicitud multicanal AuthZ.  Los siguientes escenarios describen el coste/beneficio de las diferentes maneras de implementar la autorización de comprobación previa:

* **Ejemplo de mejor situación** - El MVPD proporciona la lista de recursos preautorizados durante la fase de autorización (Multi-channel AuthZ).
* **Caso peor** - Si un MVPD no admite ninguna forma de autorización de varios recursos, el servidor de autenticación de Adobe Primetime realiza una llamada de autorización al MVPD para cada recurso de la lista de recursos. Este escenario tiene un impacto (proporcional al número de recursos) en el tiempo de respuesta de la solicitud de autorización de comprobación previa. Puede aumentar la carga en los servidores Adobe y MVPD, lo que provoca problemas de rendimiento. Además, generará solicitudes de autorización/eventos de respuesta sin la necesidad real de una obra.
* **Obsoleto** - El MVPD proporciona la lista de recursos preautorizados durante la fase de autenticación, por lo que no se necesitarán llamadas de red, ni siquiera la solicitud de comprobación previa, ya que la lista se almacena en caché en el cliente.

Aunque los MVPD no tienen que admitir la autorización de comprobación previa, las siguientes secciones describen algunos métodos de autorización de comprobación previa que la autenticación de Adobe Primetime puede admitir, antes de volver al peor de los casos descrito anteriormente.

## Comprobación previa en AuthN {#preflight-authn}

Este escenario de comprobación previa es compatible con OLCA (Cableabs). La sección 7.5.2 de Especificación de la Interfaz de Autenticación y Autorización 1.0, titulada &quot;Declaración de atributos dentro de la aserción de autenticación&quot;, describe cómo una respuesta de autenticación SAML puede contener una lista de recursos preautorizados. Si un IdP lo admite, el servidor de autenticación de Adobe Primetime podrá generar la lista de recursos predicha en el momento de la autenticación y almacenarla en la caché del cliente junto con el token de autenticación. Este método también logra el mejor escenario, y no se realizarán llamadas de red cuando el programador llama a checkPreauthorizedResources(), ya que todo ya está en el cliente.

### Lista de recursos personalizada en la instrucción de atributo SAML {#custom-res-saml-attr}

La respuesta de autenticación SAML del IdP incluirá una AttributeStatement que contiene nombres de recursos que AdobePass debe autorizar.  Algunos MVPD lo proporcionan en el siguiente formato:

```XML
<saml:AttributeStatement>
  <saml:Attribute Name="authorized_resources">
    <saml:AttributeValue>MMOD</saml:AttributeValue>
    <saml:AttributeValue>Olympics2012</saml:AttributeValue>
  </saml:Attribute>
</saml:AttributeStatement>
```

El ejemplo anterior presenta una lista que contiene dos recursos preautorizados: &quot;MMOD&quot; y &quot;Olimpíadas 2012&quot;.

De este modo, se consigue el mejor escenario posible y no se realizarán llamadas de red cuando el programador llama a checkPreauthorizedResources(), ya que todo ya está en el cliente.

## Comprobación preliminar multicanal en AuthZ {#preflight-multich-authz}

Esta implementación de comprobación previa también es compatible con OLCA (Cablelabs).  La especificación de la interfaz de autenticación y autorización 1.0 (secciones 7.5.3 y 7.5.4) describe los métodos para solicitar información de autorización a un MVPD mediante Aserciones SAML o XACML. Esta es la forma recomendada de consultar el estado de autorización de los MVPD que no lo admiten como parte del flujo de autenticación. La autenticación de Adobe Primetime emite una sola llamada de red al MVPD para recuperar la lista de recursos autorizados.


La autenticación de Adobe Primetime recibe la lista de recursos de la aplicación del programador. La integración MVPD de la autenticación de Adobe Primetime puede realizar una llamada a AuthZ que incluya todos esos recursos y, a continuación, analizar la respuesta y extraer las múltiples decisiones de permitir/denegar.  El flujo para la comprobación previa con el escenario AuthZ de varios canales funciona de la siguiente manera:

1. La aplicación del programador envía una lista de recursos separados por coma a través de la API del cliente de comprobación previa, por ejemplo: &quot;TestChannel1,TestChannel2,TestChannel3&quot;.
1. La llamada de solicitud AuthZ de comprobación preliminar de MVPD contiene varios recursos y tiene la siguiente estructura:

```XML
<?xml version="1.0" encoding="UTF-8"?><soap11:Envelope xmlns:soap11="http://schemas.xmlsoap.org/soap/envelope/"> 
<soap11:Header/> 
<soap11:Body> 
  <xacml-samlp:XACMLAuthzDecisionQuery xmlns:xacml-samlp="urn:oasis:names:tc:xacml:2.0:profile:saml2.0:v2:schema:protocol" 
                                       CombinePolicies="false" Destination="https://login.idpexmaple.net/" ID="_3576604f382455d6495f342d9e07b69c" 
                                       IssueInstant="2013-02-07T10:31:40.333Z" Version="2.0"> 
  <saml2:Issuer xmlns:saml2="urn:oasis:names:tc:SAML:2.0:assertion">https://saml.sp.auth-staging.adobe.com/on-behalf-of/TestDistributors</saml2:Issuer> 
  <xacml-context:Request xmlns:xacml-context="urn:oasis:names:tc:xacml:2.0:context:schema:os"> 
  <xacml-context:Subject SubjectCategory="urn:oasis:names:tc:xacml:1.0:subject-category:access-subject"> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:subject:subject-id" DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">VFZTAQEAABQCe[...]</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Subject> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">TestChannel1</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">TestChannel2</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                                xsi:type="xacml-context:AttributeValueType">TestChannel3</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Action> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:action:action-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">VIEW</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Action> 
  <xacml-context:Environment> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:subject:authn-locality:ip-address" 
                           DataType="urn:oasis:names:tc:xacml:2.0:data-type:ipAddress"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">127.0.0.1</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Environment> 
  </xacml-context:Request> 
  </xacml-samlp:XACMLAuthzDecisionQuery> 
</soap11:Body> 
</soap11:Envelope>
```

## Autorización Personalizada Para Varios Recursos {#custom-authz}

Algunos MVPD tienen extremos de autorización que admiten la autorización de varios recursos en una solicitud, pero no entran dentro del escenario descrito en Multi-channel AuthZ. Estos MVPD específicos requieren un trabajo personalizado.

Adobe también puede admitir la autorización de varios canales sin realizar cambios en la implementación existente.  Es necesario revisar este enfoque entre el Adobe y el equipo técnico de MVPD para asegurarse de que funciona según lo esperado.

## MVPD que admiten autorización de comprobación previa {#mvpds-supp-preflight-authz}

La siguiente tabla enumera los MVPD que admiten la autorización de comprobación previa, junto con el tipo de comprobación previa que admiten y las limitaciones conocidas:

| Enfoque de comprobación previa | MVPD | Notas |
|:-------------------------------:|:--------------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------:|
| AuthZ de varios canales | Comcast AT&amp;T Proxy Clearleap Charter_Direct Proxy GLDS Rogers Verizon OSN Bell Sasktel Optimum AlticeOne |  |
| Vinculación de canales en metadatos de usuario | Suddenlink HTC | Todas las integraciones directas de Synacor también pueden admitir este enfoque. |
| Fork y Unirse | Todos los demás no enumerados anteriormente | El número máximo predeterminado de recursos comprobados = 5. |

<!--
![RelatedInformation]
>* [Logout](/help/authentication/usecase-mvpd-logout.md)
>* [Authorization](/help/authentication/authz-usecase.md)
>* [MVPD Integration Features](/help/authentication/mvpd-integr-features.md)
>* [MVPD User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Preflight Authorization - Programmer Integration Guide](/help/authentication/preflight-authz.md)
>* [AuthN and AuthZ Interface 1.0 Specification](https://www.cablelabs.com/specifications/CL-SP-AUTH1.0-I04-120621.pdf){target=_blank} 
-->
