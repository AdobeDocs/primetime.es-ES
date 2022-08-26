---
title: Registro de devoluciones
description: Registro de devoluciones
source-git-commit: 4c3a0dd56b4ef99ac8c57cfde61f792088b0ff4d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# Registro de devoluciones {#return-registration-record}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.


## Puntos finales de API de REST {#clientless-endpoints}

&lt;reggie_fqdn>:

* Producción - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Ensayo - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Producción - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Ensayo - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

 </br>
 

## Descripción {#description}

Devuelve el registro de código de registro que contiene el código de registro UUID, el código de registro y el ID de dispositivo con hash. 

 

<div>


| Punto final | Llamada  </br>Por | Entrada   </br>Parámetros | HTTP  </br>Método | Respuesta | HTTP  </br>Respuesta |
| --- | --- | --- | --- | --- | --- |
| &lt;reggie_fqdn>;/reggie/v1/{requestorId}/regcode/{registrationCode}</br></br>Por ejemplo:</br></br>&lt;reggie_fqdn>/reggie/v1/sampleRequestorId/regcode/TJCFK?format=xml | Aplicación de flujo continuo</br></br>o</br></br>Servicio de programación | 1. requestor  </br>    (Componente Ruta)</br>2.  código de registro  </br>    (Componente Ruta) | GET | XML o JSON que contienen un código de registro e información. Consulte esquema y ejemplo a continuación. | 200 |

{style=&quot;table-layout:auto&quot;}

</br>

| Parámetro de entrada | Descripción |
| --- | --- |
| requestor | El RequestorId del programador para el que esta operación es válida. |
| código de registro | El valor del código de registro que se mostraría en el dispositivo de transmisión (que se introduciría en el flujo de autenticación). |

</br>

## Esquema XML de respuesta {#response-xml-schema}

### Código de registro XSD

```XML
    <?xml version="1.0" encoding="UTF-8"?>
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns="model.mvc.reggie.pass.adobe.com"
            targetNamespace="model.mvc.reggie.pass.adobe.com"
            attributeFormDefault="unqualified"
            elementFormDefault="unqualified">
        <xs:element name="regcode">
            <xs:complexType>
                <xs:all>
                    <xs:element name="id" type="xs:string" />
                    <xs:element name="code" type="xs:string" />
                    <xs:element name="requestor" type="xs:string" minOccurs="1" maxOccurs="1"/>
                    <xs:element name="mvpd" type="xs:string" minOccurs="1" maxOccurs="1"/
                    <xs:element name="generated" type="xs:long" />
                    <xs:element name="expires" type="xs:long" />
                    <xs:element name="info" type="infoType" maxOccurs="1"/>
                </xs:all>
            </xs:complexType>
        </xs:element>
        <xs:complexType name="infoType">
            <xs:all>
                <xs:element name="deviceId" type="xs:base64Binary" minOccurs="1" maxOccurs="1"/>
                <xs:element name="deviceType" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="deviceUser" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="appId" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="appVersion" type="xs:string" minOccurs="0" maxOccurs="1"/>
                <xs:element name="registrationURL" type="xs:anyURI" minOccurs="0" maxOccurs="1"/>
            </xs:all>
        </xs:complexType>
    </xs:schema>
```

| Nombre del elemento | Descripción |
| --- | --- |
| id | UUID generado por el Servicio de códigos de registro |
| code | Código de registro generado por el Servicio de códigos de registro |
| requestor | ID del solicitante |
| mvpd | ID de MVPD |
| generado | Marca de fecha y hora de creación del código de registro (en milisegundos desde el 1 de enero de 1970 GMT) |
| caduca | Marca de tiempo cuando caduca el código de registro (en milisegundos desde el 1 de enero de 1970 GMT) |
| deviceId | ID de dispositivo único (o token XSTS) |
| deviceType | Tipo de dispositivo |
| deviceUser | Usuario que ha iniciado sesión en el dispositivo |
| appId | ID de aplicación |
| appVersion | Versión de la aplicación |
| registrationURL | URL de la aplicación web de inicio de sesión que se mostrará al usuario final |

{style=&quot;table-layout:auto&quot;}

### Respuesta de ejemplo {#sample-response}

```XML
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <ns2:regcode xmlns:ns2="model.mvc.reggie.pass.adobe.com">
        <id>678f9fea-a1cafec8-1ff0-4a26-8564-f6cd020acf13</id>
        <code>TJJCFK</code>
        <requestor>sampleRequestorId</requestor>
        <mvpd>sampleMvpdId</mvpd>
        <generated>1348039846647</generated>
        <expires>1348043446647</expires>
        <info>
            <deviceId>dGhpc0lkQUR1bW15RGV2aWNlSWQ=</deviceId>
            <deviceType>xbox</deviceType>
            <deviceUser>JD</deviceUser>
            <appId>2345</appId>
            <appVersion>2.0</appVersion>
            <registrationURL>http://loginwebapp.com</registrationURL>
        </info>
    </ns2:regcode>
```

[Volver a la referencia de la API de REST](http://tve.helpdocsonline.com/rest-api-reference)