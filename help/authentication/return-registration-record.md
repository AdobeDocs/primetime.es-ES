---
title: Devolver registro de registro
description: Devolver registro de registro
exl-id: 7b9e63a2-59b6-4123-a19b-ee1f021219ea
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Devolver registro de registro {#return-registration-record}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.


## Extremos de API de REST {#clientless-endpoints}

&lt;reggie_fqdn>:

* Producción - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Ensayo - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Producción - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Ensayo - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>


## Descripción {#description}

Devuelve el registro del código de registro que contiene el UUID del código de registro, el código de registro y el ID del dispositivo con hash.



<div>


| Extremo | Llamado  </br>Por | Entrada   </br>Parámetros | HTTP  </br>Método | Respuesta | HTTP  </br>Respuesta |
| --- | --- | --- | --- | --- | --- |
| &lt;reggie_fqdn>;/reggie/v1/{requestorId}/regcode/{registrationCode}</br></br>Por ejemplo:</br></br>&lt;reggie_fqdn>/reggie/v1/sampleRequestorId/regcode/TJCFK?format=xml | Aplicación de streaming</br></br>o</br></br>Servicio de programador | 1. solicitante  </br>    (Componente Ruta)</br>2.  código de registro  </br>    (Componente Ruta) | GET | XML o JSON que contienen un código de registro e información. Consulte esquema y ejemplo a continuación. | 200 |

{style="table-layout:auto"}

</br>

| Parámetro de entrada | Descripción |
| --- | --- |
| solicitante | Identificador de solicitante del programador para el que es válida esta operación. |
| código de registro | El valor del código de registro que se mostrará en el dispositivo de streaming (para introducirlo en el flujo de autenticación). |

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

| Nombre de elemento | Descripción |
| --- | --- |
| id | UUID generado por el servicio de código de registro |
| código | Código de registro generado por el servicio de código de registro |
| solicitante | ID de solicitante |
| mvpd | ID de MVPD |
| generado | Marca de tiempo de creación del código de registro (en milisegundos desde el 1 de enero de 1970 GMT) |
| caduca | Marca de tiempo cuando caduca el código de registro (en milisegundos desde el 1 de enero de 1970 GMT) |
| deviceId | ID de dispositivo único (o token XSTS) |
| deviceType | Tipo de dispositivo |
| deviceUser | El usuario ha iniciado sesión en el dispositivo |
| appId | ID de aplicación |
| appVersion | Versión de aplicación |
| registrationURL | URL de la aplicación web de inicio de sesión que se mostrará al usuario final |

{style="table-layout:auto"}

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
