---
title: Amazon FireOS SSO mediante la guía de cookies de API sin cliente
description: Amazon FireOS SSO mediante la guía de cookies de API sin cliente
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---


# Amazon FireOS SSO mediante la guía de cookies de API sin cliente {#amazon-fireos-sso-using-clientless-api-cookbook}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>

## Introducción {#Introduction}

Este documento proporciona instrucciones para implementar la versión SSO de Amazon del flujo de autenticación de Adobe Primetime mediante API sin clientes. La primera parte de este documento se centra en la especificidad de la versión Amazon de la arquitectura, para los muchos socios ya familiarizados y experimentados con su implementación.

La segunda parte del documento trata sobre los pasos principales para implementar la API sin cliente de autenticación de Adobe Primetime.

Para obtener una descripción general técnica del funcionamiento de la solución sin cliente, consulte la [Información general de la API de REST](/help/authentication/rest-api-overview.md). Adobe es el contacto preferido para obtener soporte técnico sobre la arquitectura general y las primeras implementaciones.

## SSO sin clientes de Amazon {#AMZ-Clientless-SSO}

### Arquitectura de alto nivel {#High-Level-Arch}

La implementación SSO sin cliente de Amazon es sencilla y, en su mayoría, idéntica a las API sin cliente de autenticación de Adobe Primetime normales.

Deberá utilizar el SDK de Amazon para recuperar una carga útil personalizada y utilizarla al llamar a las API sin cliente de Adobe.

Si la carga útil se reconoce y corresponde a una sesión autenticada, las API sin cliente regresarán inmediatamente con el token de la sesión.

### Cómo compilar la aplicación para utilizar el SDK de Amazon {#Build-entries}

* Descargue y copie la última [Amazon Stub SDK](https://tve.zendesk.com/hc/en-us/article_attachments/360064368131/ottSSOTokenLib_v1.jar) en una carpeta /SSOEnabler paralela al directorio de la aplicación
* Actualice los archivos de manifiesto/gradle para utilizar la biblioteca :

   **Añada la siguiente línea al archivo Manifest :**

   ```Java
   <uses-library android:name="com.amazon.ottssotokenlib" android:required="false"/\>
   ```

   **Entradas del archivo de gradle:**

   En repositorios:

   ```java
   flatDir {
        dirs '../SSOEnabler'
   }
   ```

   En dependencias, agregue:

   ```Java
   provided fileTree(include: \['ottSSOTokenStub.jar'\], dir: '../SSOEnabler')
   ```


* Gestión de la ausencia de la aplicación Companion de Amazon:

   Aunque no es probable que el complemento no esté presente en el dispositivo Amazon que está ejecutando la aplicación, debería encontrar un ClassNotFoundException en tiempo de ejecución en la siguiente clase: `com.amazon.ottssotokenlib.SSOEnabler`.

   Si esto sucede, todo lo que debe hacer es omitir el paso de carga útil y volver al flujo normal de PrimeTime. SSO no se activará, pero el flujo de autenticación regular se producirá normalmente.

</br>

### Cómo obtener la carga útil SSO de Amazon mediante el SDK de Amazon {#UseAmazonSSO}

Durante la inicialización de la aplicación, obtenga una instancia de SSOEnabler. En función de la arquitectura de la aplicación, debe decidir entre una implementación sincrónica o asincrónica.

Si, por cualquier motivo, las llamadas a la API no devuelven una carga útil, utilice el flujo normal que no sea de SSO y póngase en contacto con sus socios de Amazon y Adobe para investigar.

**API asíncrona**

* Obtener instancia de SSO Enabler:

   ```Java
   ssoEnabler = SSOEnabler.getInstance(context);
   SSOEnablerCallback ssoEnablerCallback = new SSOEnablerCallbackImpl();
   ssoEnabler.setSSOTokenCallback(ssoEnablerCallback);
   ```


* Configuración de la rellamada 

   ```java
   public static abstract class SSOEnablerCallback
   {
           public abstract void getSSOTokenSuccess(Bundle result);
           public abstract void getSSOTokenFailure(Bundle result);
   }
   ```

   * El paquete de respuestas de éxito contendrá:
      * Token de SSO como cadena con la clave &quot;SSOToken&quot;
   * El paquete de respuesta de error contiene:
      * código de error como int con la clave &quot;ErrorCode&quot;
      * descripción del error como una cadena con la clave &quot;ErrorDescription&quot;


* Obtener token SSO

   ```JAVA
   Bundle getSSOTokenAsync(Void);
   ```

* Esta API proporciona la respuesta a través de la rellamada configurada durante la visita.

   **Ex**. llamada mediante la instancia singleton creada durante el inicio:

   ```JAVA
   ssoEnabler.getSSOTokenAsync().
   ```


**API sincrónicas**

* Obtenga la instancia de SSO Enabler y establezca la rellamada

   ```JAVA
   ssoEnabler = SSOEnabler.getInstance(context);</span>
   ```

* Obtener token SSO

   ```JAVA
   Bundle getSSOTokenSync(Void);
   ```

   * Esta API bloqueará el subproceso que realiza la llamada y responderá con el paquete de resultados. Como esta es una llamada sincrónica, asegúrese de no usarla en su subproceso principal.

   ```JAVA
   void setSSOTokenTimeout(long);
   ```

   * Valor en milisegundos. si está establecido, anule el valor de tiempo de espera predeterminado de 1 minuto para la API de sincronización.



### Actualización de la API sin cliente de Adobe Primetime para utilizar el registro de cliente dinámico {#clientlessdcr}

Si esta es su primera implementación, consulte la **Información general técnica sin cliente** y póngase en contacto con el Adobe en caso de que necesite asistencia técnica.

La API sin cliente de Adobe requiere que las aplicaciones utilicen el registro de cliente dinámico para realizar llamadas a los servidores de Adobe.

* Para utilizar el registro de cliente dinámico en la aplicación, siga las instrucciones indicadas en [ Dynamic Client Registration Management para registrar la aplicación](/help/authentication/dynamic-client-registration-management.md).

* Para implementar la API de registro de cliente dinámico para realizar solicitudes de autenticación y autorización a los servidores de Adobe Primetime, siga las instrucciones de [API de registro de cliente dinámico](/help/authentication/dynamic-client-registration-api.md) .

### Actualización de la API Adobe Primetime Clientless para utilizar Amazon SSO {#clientlesssso}

La carga útil SSO de Amazon obtenida del SDK de Amazon debe estar presente en las solicitudes realizadas a los extremos de autenticación de Adobe Primetime :

```
      /adobe-services/*
      /reggie/*
      /api/*
```


Todos los extremos de autenticación de Primetime admiten los siguientes métodos para recibir el identificador con ámbitos de dispositivo o el identificador con ámbitos de plataforma (presentes en la carga útil de SSO de Amazon) :

* Como encabezado : &quot;Adobe-Subject-Token&quot;
* Como parámetro de consulta : &quot;ast&quot;
* Como parámetro posterior : &quot;ast&quot;


>[!NOTE]
>
>Si el identificador del ámbito del dispositivo o el identificador del ámbito de la plataforma se envían como parámetro de consulta/publicación, debe incluirse al generar la firma de la solicitud.

>[!NOTE]
>
>Si se utiliza el parámetro de consulta &quot;ast&quot;, toda la dirección URL puede ser muy larga y rechazada. En la llamada /authentication, este parámetro se puede omitir porque se proporcionó en la llamada /regcode.

**Ejemplos:**

**Envío como encabezado personalizado**

```HTTPS
GET /adobe-services/config/requestor HTTP/1.1 Host: sp-preprod.auth.adobe.com

Adobe-Subject-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA
```

**Envío como parámetro de consulta**

```HTTPS
GET /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com
```


**Envío como parámetro posterior**


```HTTPS
POST /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.Jl\_BFhN\_h\_NCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com Content-Type: multipart/form-data;
boundary=---- WebKitFormBoundary7MA4YWxkTrZu0gW
```

>[!NOTE]
>
>Si el SSO de Amazon no está presente o no es válido, la autenticación de Adobe Primetime ignorará el atributo y las llamadas se ejecutarán como si el SSO no estuviera presente.
