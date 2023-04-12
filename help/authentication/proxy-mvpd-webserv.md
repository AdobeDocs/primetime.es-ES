---
title: Servicio web proxy MVPD
description: Servicio web proxy MVPD
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---


# Servicio web Proxy MVPD {#proxy-mvpd-wbservice}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Información general {#overview-proxy-mvpd-webserv}

Un &quot;MVPD proxy&quot; es un MVPD que, además de administrar su propia integración con la autenticación de Adobe Primetime, también gestiona el proceso de asignación de derechos en nombre de un grupo de &quot;MVPD Proxied&quot; asociados. Este arreglo es transparente para los programadores.

Para implementar la función ProxyMVPD, la autenticación de Adobe Primetime proporciona servicios web RESTful, con los que los ProxyMVPD pueden enviar y recuperar listas de ProxiedMVPD. El protocolo utilizado para esta API pública es REST HTTP, con los siguientes supuestos:

* El MVPD de proxy utiliza el método de GET HTTP para recuperar la lista de los MVPD integrados actuales.
* El MVPD de proxy utiliza el método de POST HTTP para actualizar la lista de los MVPD admitidos.

## Servicios MVPD de proxy {#proxy-mvpd-services}

* [Recuperar MVPD proxy](#retriev-proxied-mvpds)
* [Envío de MVPD procesados como proxy](#submit-proxied-mvpds)

### Recuperar MVPD proxy {#retriev-proxied-mvpds}

Recupera la lista actual de MVPD Proxied para el ProxyMVPD identificado por el parámetro apikey.

| Punto final | Llamado por | Solicitar encabezados | Método HTTP | Respuesta HTTP |
|---|---|---|---|---|
| &lt;fqdn>/control/v1/proxyMvpds | ProxyMVPD | apikey (obligatorio) | GET | <ul><li> 200 (ok) - La solicitud se procesó correctamente, y la respuesta contiene una lista de ProxiedMVPD en formato XML</li><li>401 (no autorizado) - Se requiere autenticación de usuario o no se concede autorización para las credenciales proporcionadas.  Indica una de las siguientes opciones:<ul><li>El token apikey no está presente en el encabezado de la solicitud</li><li>La solicitud proviene de una dirección IP que no está presente en la lista de permitidos</li><li>El token no es válido</li></ul></li><li>403 (prohibido) : indica que la operación no es compatible con los parámetros proporcionados, o que el MVPD proxy no está configurado como proxy o que falta</li><li>405 (método no permitido): se ha utilizado un método HTTP que no sea GET o POST. Normalmente, el método HTTP no es compatible o no lo es para este extremo específico.</li><li>500 (error interno del servidor): Se ha producido un error en el servidor durante el proceso de solicitud.</li></ul> |

Ejemplo de curl:

`curl -X GET -H "apikey: ???provided-by-adobe???" "https://mgmt-prequal.auth-staging.adobe.com/control/v1/proxiedMvpds"`


Ejemplo de respuesta XML:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<proxiedMvpds>
    <proxiedMvpd>
        <id>oneMvpdId</id>
        <displayName>MVPD Name</displayName>
        <logoURL></logoURL>
    </proxiedMvpd>
    <proxiedMvpd>
        <id ProviderID="ProviderID_Value_Sent_On_IdPEntry">mvpdPickerId</id>
        <displayName>MVPD Name Two</displayName>
        <logoURL></logoURL>
        <requestorIds>
            <requestorId>TheRequestorId_IntegratedWith</requestorId>
        </requestorIds>
    </proxiedMvpd>
    <proxiedMvpd>
        <id>anotherMvpdId</id>
        <displayName>Another MVPD</displayName>
        <logoURL></logoURL>
        <iframeSize>
            <iframeHeight>400</iframeHeight>
            <iframeWidth>340</iframeWidth>
        </iframeSize>
        <requestorIds>
            <requestorId>FirstIntegratedRequestorId</requestorId>
            <requestorId>SecondIntegratedRequestorId</requestorId>
        </requestorIds>
    </proxiedMvpd>
</proxiedMvpds>
```

### Envío de MVPD procesados como proxy {#submit-proxied-mvpds}

Inserta una matriz de MVPD integrados con el MVPD de Proxy identificado por el parámetro apikey.

| Punto final | Llamado por | Solicitar encabezados | Método HTTP | Respuesta HTTP |
|:------------------------------:|:---------:|:--------------------------------------------:|:-----------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| &lt;fqdn>/control/v1/proxyMvpds | ProxyMVPD | apikey (obligatorio) proxy-mvpds (obligatorio) | POST | <ul><li>201 (creado): La notificación push se procesó correctamente</li><li>400 (solicitud incorrecta): El servidor no sabe cómo procesar la solicitud:<ul><li>El XML entrante no se adhiere al esquema publicado en esta especificación</li><li>Los mvpds procesados como proxy no tienen id únicos</li><li>Los requestorIds insertados no existen Otros motivos del contenedor Servlet para el código de respuesta 400</li></ul><li>401 (no autorizado) - El apikey no es válido o la IP del llamador no está en la lista de permitidos</li><li>403 (prohibido) : indica que la operación no es compatible con los parámetros proporcionados, o que el MVPD proxy no está configurado como proxy o que falta</li><li>405 (método no permitido): se ha utilizado un método HTTP que no sea GET o POST. Normalmente, el método HTTP no es compatible o no lo es para este extremo específico.</li><li>500 (error interno del servidor): Se ha producido un error en el servidor durante el proceso de solicitud.</li></ul> |

Ejemplo de curl:

`curl -X POST -H "apikey: <API_KEY>" "https://mgmt-prequal.auth.adobe.com/control/v1/proxiedMvpds" -d "proxied-mvpds=%3CproxiedMvpds%3E%3CproxiedMvpd%3E%3CdisplayName%3EFirst%20MVPD%20Name%3C%2FdisplayName%3E%3Cid%3EfirstMVPDId%3C%2Fid%3E%3ClogoURL%3E%3C%2FlogoURL%3E%3C%2FproxiedMvpd%3E%3CproxiedMvpd%3E%3Cid%20ProviderID%3D%22ProviderID_Value_Sent_On_IdPEntry%22%3EmvpdPickerId%3C%2Fid%3E%3CdisplayName%3EMVPD%20Name%20Two%3C%2FdisplayName%3E%3ClogoURL%3E%3C%2FlogoURL%3E%3CrequestorIds%3E%3CrequestorId%3ETHE_REQUESTOR_ID%3C%2FrequestorId%3E%3C%2FrequestorIds%3E%3C%2FproxiedMvpd%3E%3C%2FproxiedMvpds%3E"`



Ejemplo XML:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<proxiedMvpds>
    <proxiedMvpd>
        <id>oneMvpdId</id>
        <displayName>MVPD Name</displayName>
        <logoURL></logoURL>
    </proxiedMvpd>
    <proxiedMvpd>
        <id ProviderID="ProviderID_Value_Sent_On_IdPEntry">mvpdPickerId</id>
        <displayName>MVPD Name Two</displayName>
        <logoURL></logoURL>
        <requestorIds>
            <requestorId>TheRequestorId_IntegratedWith</requestorId>
        </requestorIds>
    </proxiedMvpd>
    <proxiedMvpd>
        <id>anotherMvpdId</id>
        <displayName>Another MVPD</displayName>
        <logoURL></logoURL>
        <iframeSize>
            <iframeHeight>400</iframeHeight>
            <iframeWidth>340</iframeWidth>
        </iframeSize>
        <requestorIds>
            <requestorId>FirstIntegratedRequestorId</requestorId>
            <requestorId>SecondIntegratedRequestorId</requestorId>
        </requestorIds>
    </proxiedMvpd>
</proxiedMvpds>
```


### Frecuencia de contabilización {#posting-frequency}

La autenticación de Adobe Primetime recomienda que los ProxyMVPD inserten su lista de ProxiedMVPD solo cuando haya un cambio con respecto a la notificación push anterior.

### Eliminación de MVPD Proxied {#delete-proxied-freqency}

Si ProxyMVPD inserta un registro XML con una lista ProxiedMVPD vacía, esa lista vacía se almacenará en nuestro sistema como cualquier lista, eliminando así efectivamente la lista anterior.



## Formato XSD {#xsd-format}

Adobe ha definido el siguiente formato aceptado para publicar/recuperar MVPD proxy desde/hacia nuestro servicio web público:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
           xmlns:pxm="http://tve.adobe.com/data/proxiedmvpd"
           targetNamespace="http://tve.adobe.com/data/proxiedmvpd"
           elementFormDefault="qualified"
           version="1.0">
    <xs:complexType name="iframeSize">
        <xs:all>
            <xs:element name="iframeHeight" type="xs:int" minOccurs="1" maxOccurs="1" nillable="false"/>
            <xs:element name="iframeWidth" type="xs:int" minOccurs="1" maxOccurs="1" nillable="false"/>
        </xs:all>
    </xs:complexType>
    <xs:complexType name="requestorIds">
        <xs:annotation>
            <xs:documentation>List of requestors/programmers integrated with the proxied MVPD</xs:documentation>
        </xs:annotation>
        <xs:sequence>
            <xs:element name="requestorId" type="xs:string" minOccurs="1" maxOccurs="unbounded" nillable="false">
                <xs:annotation>
                    <xs:documentation>The requestor/programmer identifier recognized by Adobe</xs:documentation>
                </xs:annotation>
            </xs:element>
        </xs:sequence>
    </xs:complexType>
    <xs:complexType name="proxiedMvpd">
        <xs:all>
            <xs:element name="id" minOccurs="1" maxOccurs="1" nillable="false">
                <xs:annotation>
                    <xs:documentation>The id must conform to the regular expression: ([a-zA-Z0-9]+((\-)|[_])*)</xs:documentation>
                </xs:annotation>
                <xs:complexType>
                    <xs:simpleContent>
                        <xs:extension base="xs:string">
                            <xs:attribute name="ProviderID">
                                <xs:simpleType>
                                    <xs:restriction base="xs:string">
                                        <xs:minLength value="1"/>
                                        <xs:maxLength value="128"/>
                                    </xs:restriction>
                                </xs:simpleType>
                            </xs:attribute>
                        </xs:extension>
                    </xs:simpleContent>
                </xs:complexType>
            </xs:element>
            <xs:element name="displayName" type="xs:string" minOccurs="1" maxOccurs="1" nillable="false"/>
            <xs:element name="logoURL" type="xs:anyURI" minOccurs="1" maxOccurs="1" nillable="false"/>
            <xs:element name="iframeSize" type="pxm:iframeSize" minOccurs="0" maxOccurs="1"/>
            <xs:element name="requestorIds" type="pxm:requestorIds" minOccurs="0" maxOccurs="1"/>
        </xs:all>
    </xs:complexType>
    <xs:element name="proxiedMvpds">
        <xs:annotation>
            <xs:documentation>List of Proxied MVPD</xs:documentation>
        </xs:annotation>
        <xs:complexType>
            <xs:sequence>
                <xs:element name="proxiedMvpd" type="pxm:proxiedMvpd" minOccurs="0" maxOccurs="unbounded"/>
            </xs:sequence>
        </xs:complexType>
    </xs:element>
</xs:schema>
```

**Notas sobre los elementos:**

* `id` (obligatorio): El ID de MVPD Proxied debe ser una cadena relevante para el nombre del MVPD, utilizando cualquiera de los siguientes caracteres (ya que se expondrá a los programadores con fines de seguimiento):
   * Cualquier carácter alfanumérico, guión bajo (&quot;_&quot;) y guión (&quot;-&quot;).
   * El idID debe cumplir la siguiente expresión regular:
      `(a-zA-Z0-9((-)|_)*)`

      Por lo tanto, debe tener al menos un carácter, comenzar con una letra y continuar con cualquier letra, dígito, guión o guión bajo.

* `iframeSize` (opcional): El elemento iframeSize es opcional y define el tamaño del iFrame si la página de autenticación de MVPD se supone que está en un iFrame. De lo contrario, si el elemento iframeSize no está presente, la autenticación se producirá en una página de redirección completa del explorador.
* `requestorIds` (opcional) - El Adobe proporcionará los valores requestorIds. Un requisito es que un MVPD procesado como proxy se integre con al menos un requestorId. Si la etiqueta &quot;requestorIds&quot; no está presente en el elemento MVPD proxy, ese MVPD reenviado se integrará con todos los solicitantes disponibles integrados en el MVPD proxy.
* `ProviderID` (opcional) - Cuando el atributo ProviderID está presente en el elemento id, el valor de ProviderID se enviará en la solicitud de autenticación SAML al MVPD proxy como el ID MVPD/SubMVPD Proxied (en lugar del valor id). En este caso, el valor de id se utilizará únicamente en el selector de MVPD presentado en la página Programador e internamente mediante la autenticación de Adobe Primetime. La longitud del atributo ProviderID debe estar entre 1 y 128 caracteres.

## Seguridad {#security}

Para que una solicitud se considere válida, debe respetar las siguientes reglas:

* El encabezado de la solicitud debe contener el parámetro de clave de seguridad api. (Se trata de una clave de aplicación que identificará de forma exclusiva las llamadas de MVPD del proxy).
* La solicitud debe proceder de una dirección IP específica permitida.
* La solicitud debe enviarse a través del protocolo SSL.

Adobe proporcionará el valor (estático) del token. Este valor se utiliza en el proceso de autenticación y autorización.  Se ignorará cualquier parámetro presente en el encabezado de la solicitud que no aparezca en la lista anterior.

Ejemplo de curl:

`curl -X GET -H "apikey: ???provided-by-adobe???" "https://mgmt-prequal.auth-staging.adobe.com/control/v1/proxiedMvpds"`

## Puntos finales del servicio web MVPD de proxy para los entornos de autenticación de Adobe Primetime {#proxy-mvpd-wevserv-endpoints}

* **URL de producción:** https://mgmt.auth.adobe.com/control/v1/proxiedMvpds
* **Dirección URL de ensayo:** https://mgmt.auth-staging.adobe.com/control/v1/proxiedMvpds
* **URL de preproducción:** https://mgmt-prequal.auth.adobe.com/control/v1/proxiedMvpds
* **URL de PreQual-Staging:** https://mgmt-prequal.auth-staging.adobe.com/control/v1/proxiedMvpds

<!--
>[!RELATEDINFORMATION]
>* [Proxy MVPD SAML integration](/help/authentication/proxy-mvpd-saml-int.md)
>* [User metadata exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Technical paper](/help/authentication/technical-paper.md)
>* [Adobe Primetime Authentication glossary](/help/authentication/glossary.md)
-->
