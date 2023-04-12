---
title: Integración del verificador de tokens de medios
description: Integración del verificador de tokens de medios
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---


# Integración del verificador de tokens de medios

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Acerca del verificador de tokens de medios {#about-media-token-verifier}

Cuando la autorización se realiza correctamente, la autenticación de Adobe Primetime crea un token de autorización (AuthZ) de larga duración.  El token AuthZ se pasa al lado del cliente o se almacena en el lado del servidor, según la plataforma del cliente.  (Consulte [Explicación de los tokens](/help/authentication/programmer-overview.md#understanding-tokens) para saber cómo se almacenan los tokens en distintos sistemas cliente, junto con otros detalles).


Un token AuthZ autoriza al usuario del sitio a ver un recurso determinado.  Tiene un tiempo de vida típico (TTL) de 6 a 24 horas, tras lo cual caduca el token. **Para obtener acceso de visualización real, la autenticación de Primetime utiliza el token AuthZ para generar un token de medios de corta duración que obtiene y pasa al servidor de medios**. Estos tokens de medios de corta duración tienen un TTL muy breve (normalmente, unos minutos).


En las integraciones de AccessEnabler, obtiene el token de medios de corta duración mediante la variable `setToken()` llamada de retorno. Para integraciones de API sin cliente, obtiene el testigo de contenido multimedia de corta duración con la variable `<SP_FQDN>/api/v1/tokens/media` Llamada de API. El token es una cadena enviada con texto claro, firmada por Adobe, que utiliza protección de tokens basada en PKI (Infraestructura de claves públicas). Con esta protección basada en PKI, el token se firma utilizando una clave asimétrica, emitida para su Adobe por una entidad emisora de certificados.


Dado que no hay validación en el lado del cliente para el token, un usuario malintencionado podría usar herramientas para insertar falsos `setToken()` llamadas a . Por lo tanto, **cannot** simplemente se basa en el hecho de que `setToken()` se ha activado cuando se considera si un usuario está autorizado o no. Debe validar que el token de corta duración en sí es legítimo. La herramienta para llevar a cabo la validación es la biblioteca del verificador de tokens de medios.


>[!TIP]
>
>Debe pasar toda la longitud de la cadena de token devuelta al verificador de tokens de medios para la validación.

## Validación de tokens de corta duración con el verificador de tokens de medios {#validate-short-livedttokens}

Recomendamos que los programadores envíen el token a un servicio web que utilice la biblioteca de verificadores de tokens de medios para validar el token antes de iniciar realmente el flujo de vídeo. El breve TTL de los tokens de medios de corta duración se define para que sea lo suficientemente largo como para permitir problemas de sincronización de reloj entre el servidor que genera el token y el servidor que valida el token, pero ya no.



La variable [Biblioteca de verificador de tokens de medios](https://adobeprimetime.zendesk.com/auth/v2/login/signin?return_to=https%3A%2F%2Ftve.zendesk.com%2Fhc%2Fen-us%2Farticles%2F204963159-Media-Token-Verifier-library&amp;theme=hc&amp;locale=en-us&amp;brand_id=343429&amp;auth_origin=343429%2Cfalse%2Ctrue){target=_blank} está disponible para socios de autenticación de Primetime.



La biblioteca del verificador de tokens de medios está contenida en el archivo Java `mediatoken-verifier-VERSION.jar`. La biblioteca define:

* Una API de verificación de tokens (`ITokenVerifier` ), con documentación de JavaDoc
* La clave pública de Adobe utilizada para comprobar que el token viene de Adobe
* Una implementación de referencia (`com.adobe.entitlement.test.EntitlementVerifierTest.java`) que muestra cómo utilizar la API de Verifier y cómo utilizar la clave pública de Adobe contenida en la biblioteca para comprobar su origen


El archivo contiene todas las dependencias y almacenes de claves de certificado. La contraseña predeterminada para el almacén de claves de certificado incluido es &quot;123456&quot;.

* La biblioteca de verificación requiere la versión 1.5 o superior del JDK.
* Utilice su proveedor JCE preferido para el algoritmo de firma, &quot;SHA256WithRSA&quot;.


**La biblioteca de verificadores debe ser el único medio que se utilice para analizar el contenido del token. Los programadores no deben analizar el token y extraer los datos por sí mismos, ya que el formato del token no está garantizado y está sujeto a cambios futuros.** Solo se garantiza que la API de Verifier funcione correctamente. Analizar la cadena directamente podría funcionar temporalmente, pero podría causar problemas en el futuro cuando el formato cambie. La API del verificador recupera información del token, como:

* ¿Es válido el token (la variable `isValid()` método)?
* El ID de recurso vinculado al token (la variable `getResourceID()` método); esto se puede comparar con (y debe coincidir) el otro parámetro de la variable `setToken()` llamada de retorno de función. Si no coincide, esto podría indicar un comportamiento fraudulento.
* La hora en que se emitió el token (`getTimeIssued()` método).
* El TTL (`getTimeToLive()` método).
* Un GUID de autenticación anonimizado recibido del MVPD (`getUserSessionGUID()` método).
* El ID del distribuidor que autenticó al usuario y, si es así, el proxy-MVPD que proporcionó la autenticación para el distribuidor.

## Uso de la API de Verifier {#using-verifier-api}

La variable `ITokenVerifier` define los métodos que se utilizan para validar la autenticidad de los tokens para un recurso determinado. Utilice la variable `ITokenVerifier` métodos para analizar un token recibido como respuesta a un `setToken()` solicitud.


La variable `isValid()` es el principal medio para validar un token. Toma un argumento, un ID de recurso. Si se pasa un ID de recurso nulo, el método solo valida la autenticidad del token y el periodo de validez.


La variable `isValid()` devuelve uno de estos valores de estado:



| VALID_TOKEN | Todas las validaciones se realizaron correctamente |
|--------------------|-----------------------------------------|
| INVALID_TOKEN_FORMAT | El formato de token no es válido |
| INVALID_SIGNATURE | No se pudo validar la autenticidad del token |
| TOKEN_EXPIRED | El TTL del token no es válido |
| INVALID_RESOURCE_ID | Token no válido para el recurso dado |
| ERROR_UNKNOWN | El token aún no se ha validado |

Los métodos adicionales proporcionan acceso específico al ID de recurso, el tiempo de emisión y el tiempo de vida de un token determinado.

* Uso `getResourceID()` para recuperar el ID de recurso asociado al token y compararlo con el ID devuelto desde la solicitud setToken() .
* Uso `getTimeIssued()` para recuperar la hora en que se emitió el token.
* Uso `getTimeToLive()` para recuperar el TTL.
* Uso `getUserSessionGUID()` para recuperar un GUID anonimizado establecido por el MVPD.
* Uso `getMvpdId()` para recuperar el ID del MVPD que autenticó al usuario.
* Uso `getProxyMvpdId()` para recuperar el ID del MVPD proxy que autenticó al usuario.

## Código de muestra {#sample-code}

El archivo del verificador de tokens de medios contiene una implementación de referencia (`com.adobe.entitlement.test.EntitlementVerifierTest.java`) y un ejemplo de invocación de la API con la clase de prueba. Este ejemplo (`com.adobe.entitlement.text.EntitlementVerifierTest.java`) ilustra la integración de la biblioteca de verificación de tokens en un servidor de medios.


```Java
package com.adobe.entitlement.test; 
import com.adobe.entitlement.verifier.CryptoDataHolder;
import com.adobe.entitlement.verifier.ITokenVerifier;
import com.adobe.entitlement.verifier.ITokenVerifierFactory;
import com.adobe.entitlement.verifier.SimpleTokenPKISignatureVerifierFactory;
import com.adobe.tve.crypto.SignatureVerificationCredential; 
import java.io.InputStream; 

public class EntitlementVerifierTest { 
    String mRequestorID = null;
    String mTokenToVerify = null;
    String mPathToCertificate = null;
    String mKeystoreType = null;
    String mKeystorePasswd = null;
    String mResourceID = null;

    public static void main(String[] args) { 
        if (args == null || args.length < 2 ) {
            System.out.println("Incorrect args: Usage: EntitlementVerifierTest requestorID tokenToVerify [resourceID]");
            return;
        } 
        String requestorID = args[0];
        String tokenToVerify = args[1];
        String pathToCertificate = "media_token_keystore.jks"; // the default keystore provided in the entitlement jar 
        String keystoreType = "jks";
        String keystorePasswd = "123456"; // password for the default keystore 
        if (requestorID == null || tokenToVerify == null) {
            System.out.println("One or more arguments is null");
            return;
        } 
        System.out.println("RequestorID: " + requestorID);
        System.out.println("token: " + tokenToVerify);
        System.out.println("cert: " + pathToCertificate);
        System.out.println("keystoretype: " + keystoreType);
        System.out.println("keystore passwd: " + keystorePasswd);
        String resourceID = null;
        if (args.length > 2) {
            resourceID = args[2];
        }
        System.out.println("Resource ID: " + resourceID);
        EntitlementVerifierTest verifier = new EntitlementVerifierTest(requestorID,
            tokenToVerify, pathToCertificate, keystoreType, keystorePasswd, resourceID);
        verifier.verifyToken();
    } 

    protected EntitlementVerifierTest(String inRequestorID,
                                      String inTokenToVerify,
                                      String inPathToCertificate,
                                      String inKeystoreType,
                                      String inKeystorePasswd, String inResourceID) {
        mRequestorID = inRequestorID;
        mTokenToVerify = inTokenToVerify;
        mPathToCertificate = inPathToCertificate;
        mKeystoreType = inKeystoreType;
        mKeystorePasswd = inKeystorePasswd;
        mResourceID = inResourceID;
    } 

    protected void verifyToken() {
        // It is expected that the SignatureVerificationCredential and 
        // CryptoDataHolder could be created at Init time in a web application 
        // and be reused for all token verifications. 
        CryptoDataHolder cryptoData = createCryptoDataHolder(mPathToCertificate, mKeystoreType, mKeystorePasswd);
        ITokenVerifierFactory tokenVerifierFactory = new SimpleTokenPKISignatureVerifierFactory();
        ITokenVerifier tokenVerifier = tokenVerifierFactory.getInstance(mRequestorID, mTokenToVerify, cryptoData);
        ITokenVerifier.eReturnValue status = tokenVerifier.isValid(mResourceID);
        System.out.println("Is token Valid? : " + status.toString());
        System.out.println("Token User ID: " + tokenVerifier.getUserSessionGUID());
        System.out.println("Token was generated at: " + tokenVerifier.getTimeIssued());

        System.out.println("Token Mvpd ID: " + tokenVerifier.getMvpdId());
        System.out.println("Token Proxy Mvpd ID: " + tokenVerifier.getProxyMvpdId());
    } 
    protected CryptoDataHolder createCryptoDataHolder(String pathToCertificate,
                                                      String keystoreType, String keystorePasswd) {
        SignatureVerificationCredential verificationCredential =
            readShortTokenVerificationCredential(pathToCertificate, keystoreType, keystorePasswd);
        CryptoDataHolder cryptoData = new CryptoDataHolder();
        cryptoData.setCertificateInfo(verificationCredential);
        return cryptoData;
    } 
    protected SignatureVerificationCredential readShortTokenVerificationCredential(String keystoreFile,
                                                                                   String keystoreType,
                                                                                   String keystorePasswd) {
        SignatureVerificationCredential cred = null; 
        if (keystoreFile != null){
            try {
                // load the keystore file 
                ClassLoader loader = EntitlementVerifierTest.class.getClassLoader();
                InputStream certInputStream =  loader.getResourceAsStream(keystoreFile);
                if (certInputStream != null) {
                    cred = new SignatureVerificationCredential(certInputStream, keystorePasswd, keystoreType);          
                }
            }
            catch (Exception e) {
                System.out.println("Error creating short token server credentials: " + e.getMessage());
            }
        }
        if (cred == null) {
            System.out.println("Error creating short token server credentials");
        } 
        return cred;
    } 
}
```
