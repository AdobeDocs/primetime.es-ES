---
title: Información general sobre la implementación del servidor de claves DRM de Primetime
description: Información general sobre la implementación del servidor de claves DRM de Primetime
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 0%

---

# Implementación del servidor de claves DRM de Primetime {#deploy-the-primetime-drm-key-server}

Antes de implementar el servidor de claves DRM de Primetime, asegúrese de que ha instalado las versiones necesarias de Java y Tomcat. Consulte. [Requisitos clave del servidor DRM](../../digital-rights-management/using-the-drm-key-server/requirements.md).

La descarga de Primetime DRM Key Server incluye [!DNL faxsks.war]. Para implementar este archivo WAR, copie el archivo en el de Tomcat [!DNL webapps] directorio. Si ha implementado previamente el archivo WAR, es posible que tenga que eliminar manualmente el directorio WAR desempaquetado, [!DNL faxsks] en Tomcat&#39;s [!DNL webapps] directorio). Para evitar que Tomcat descomprima archivos WAR, edite el [!DNL server.xml] archivo en Tomcat&#39;s [!DNL conf] y establezca el `unpackWARs` atribuir a `false`.

El servidor de claves DRM de Primetime utiliza opcionalmente una biblioteca específica de la plataforma (`jsafe.dll` en Windows o `libjsafe.so` en Linux) para obtener un rendimiento mejorado. Copie la biblioteca adecuada para su plataforma desde `thirdparty/cryptoj/platform` a una ubicación especificada por el `PATH` variable de entorno (o `LD_LIBRARY_PATH` en Linux).

>[!NOTE]
>
>La versión de 64 bits de [!DNL jsafe] La biblioteca de solo debe utilizarse si el sistema operativo y el JDK admiten 64 bits; de lo contrario, utilice la versión de 32 bits.

## Configuración SSL {#ssl-configuration}

Se requiere SSL para la entrega de claves HTTPS remotas. Las conexiones SSL podrían ser gestionadas por el servidor de aplicaciones (es decir, configurando SSL en Tomcat) o podrían ser gestionadas en otro servidor (es decir, un equilibrador de carga, un acelerador SSL o Apache). La entrega de claves HTTPS remotas requiere una conexión SSL. El servidor necesita un certificado SSL emitido por una CA de confianza.

Existen varias opciones para configurar SSL. A continuación se muestran ejemplos para configurar SSL con autenticación de cliente en Apache y Tomcat.

El siguiente ejemplo muestra la configuración SSL de Apache:

```
SSLEngineon 
SSLCertificateFile "certs/server_cert.pem" 
SSLCertificateKeyFile "certs/server_key.pem" 
SSLOptions +StdEnvVars +FakeBasicAuth -ExportCertData +StrictRequire 
SSLRequireSSL 
ProxyRequests Off 
ProxyPass /https://keyserver-name:port/ 
ProxyPassReverse /https://keyserver-name:port/
```

El siguiente ejemplo muestra la configuración SSL de Tomcat. Para generar archivos de certificado y clave:

```
Generate key:  
 openssl genrsa -des3 -out server.key 1024 
Generate CSR: 
 openssl req -new -key server.key -out server.csr 
Generate Certificate: 
 openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.cer
```

Cuando se le pida el nombre común, utilice el nombre de dominio completo (FQDN) del servidor.

Copiar [!DNL server.cer], y [!DNL server.key] en el directorio Tomcat. Especifique el siguiente conector en [!DNL conf/server.xml]:

```
<Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true" 
 maxThreads="150" scheme="https" secure="true" 
 sslProtocol="TLS" 
 SSLCertificateFile="${catalina.base}/server.cer" 
 SSLCertificateKeyFile="${catalina.base}/server.key" 
 SSLPassword="password-for-key-file" 
 SSLVerifyClient="require"/>
```

## Propiedades del sistema Java {#java-system-properties}

Tiene la opción de definir las dos propiedades del sistema Java siguientes para modificar la ubicación de los archivos de configuración y registro para el servidor de claves DRM de Primetime:

* `KeyServer.ConfigRoot` : Este directorio contiene todos los archivos de configuración del servidor de claves DRM de Primetime. Para obtener más información sobre el contenido de estos archivos, consulte [Archivos de configuración del servidor clave](#key-server-configuration-files). Si no se configura, el valor predeterminado es [!DNL CATALINA_BASE/keyserver].

* `KeyServer.LogRoot` - Es un directorio de registro que contiene los registros de la aplicación de iOS Key Server. Si no se configura, el valor predeterminado es el mismo que `KeyServer.ConfigRoot`

* `XboxKeyServer.LogRoot` - Este es un directorio de registro que contiene los registros de la aplicación Xbox Key Server. Si no se configura, el valor predeterminado es el mismo que `KeyServer.ConfigRoot`.

Si está utilizando [!DNL catalina.bat] o [!DNL catalina.sh] para iniciar Tomcat, estas propiedades del sistema se pueden configurar fácilmente usando el `JAVA_OPTS` variable de entorno. Cualquier opción de Java establecida aquí se utilizará cuando se inicie Tomcat. Por ejemplo, establezca:

```
JAVA_OPTS=-DKeyServer.ConfigRoot=”absolute-path-to-config-folder” 
  -DKeyServer.LogRoot=”absolute-path-to-log-folder”
```

## Credenciales de DRM de Primetime {#primetime-drm-credentials}

Para procesar solicitudes de clave de clientes de Primetime DRM iOS y Xbox 360, el servidor de claves DRM de Primetime debe estar configurado con un conjunto de credenciales emitidas por Adobe. Estas credenciales se pueden almacenar en PKCS#12 ( [!DNL .pfx]) archivos o en un HSM.

El [!DNL .pfx] Los archivos de se pueden localizar en cualquier lugar, pero para facilitar la configuración, Adobe recomienda colocar el [!DNL .pfx] archivos en el directorio de configuración del inquilino. Para obtener más información, consulte [Archivos de configuración del servidor clave](#key-server-configuration-files).

### Configuración de HSM {#section_13A19E3E32934C5FA00AEF621F369877}

Si decide utilizar un HSM para almacenar las credenciales del servidor, debe cargar las claves privadas y los certificados en el HSM y crear un *pkcs11.cfg* archivo de configuración. Este archivo debe encontrarse en el *KeyServer.ConfigRoot* directorio. Consulte la `<Primetime DRM Key Server>/configs` para un archivo de configuración PKCS 11 de ejemplo. Para obtener información sobre el formato de [!DNL pkcs11.cfg], consulte la documentación del proveedor de Sun PKCS11.

Para comprobar que los archivos de configuración de HSM y Sun PKCS11 están correctamente configurados, puede utilizar el siguiente comando desde el directorio donde se encuentra el [!DNL pkcs11.cfg] el archivo se encuentra en ( [!DNL keytool] se instala con Java (JRE y JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Si ve sus credenciales en la lista, el HSM está configurado correctamente y el servidor de claves podrá acceder a las credenciales.

## Archivos de configuración del servidor clave {#key-server-configuration-files}

El servidor de claves DRM de Primetime requiere dos tipos de archivos de configuración:

* Un archivo de configuración global, [!DNL flashaccess-keyserver-global.xml]
* Un archivo de configuración de usuario para cada usuario, [!DNL flashaccess-keyserver-tenant.xml]

Si se realizan cambios en los archivos de configuración, se debe reiniciar el servidor para que los cambios surtan efecto.

Para evitar que las contraseñas estén disponibles en texto no cifrado en los archivos de configuración, todas las contraseñas especificadas en los archivos de configuración global e inquilino deben estar cifradas. Para obtener más información sobre el cifrado de contraseñas, consulte [*Descodificador de contraseñas* in *Uso del servidor DRM de Primetime para flujo protegido*](../protected-streaming/understanding-deployment/drm-for-protected-streaming-utilities/password-scrambler.md).

## Estructura del directorio de configuración {#configuration-directory-structure}

Los directorios de configuración tienen la siguiente estructura:

```
KeyServer.ConfigRoot/  
--flashaccess-keyserver-global.xml 
--pkcs11.cfg (optional) 
--faxsks/ 
----tenants/ 
------tenantname/
---------flashaccess-keyserver-tenant.xml 
---------credential.pfx (optional) 
```

## Archivo de configuración global {#global-configuration-file}

El [!DNL flashaccess-keyserver-global.xml] El archivo de configuración contiene opciones que se aplican a todos los inquilinos del servidor de claves. Este archivo debe encontrarse en `KeyServer.ConfigRoot`. Consulte la [!DNL configs] para un archivo de configuración global de ejemplo. El archivo de configuración global incluye lo siguiente:

* Registro: especifica el nivel de registro y la frecuencia con la que se acumulan los archivos de registro.
* Contraseña de HSM: necesaria solo si se utiliza un HSM para almacenar las credenciales del servidor.

Consulte los comentarios del archivo de configuración global de ejemplo ubicado en `<Primetime DRM Key Server>/configs` para obtener más información.

## Archivos de configuración de inquilino {#tenant-configuration-files}

El [!DNL flashaccess-ioskeyserver-tenant.xml] y [!DNL flashaccess-xboxkeyserver-tenant.xml] Los archivos de configuración contienen opciones que se aplican a un inquilino específico del servidor de claves DRM de Primetime. Cada inquilino tiene su propia instancia de estos archivos de configuración ubicados en [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]. Consulte la [!DNL configs/faxsks/tenants/sampletenant] para un archivo de configuración de inquilino de ejemplo.

Puede especificar todas las rutas de archivo en el archivo de configuración del inquilino como rutas absolutas o rutas relativas al directorio de configuración del inquilino ( [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]).

Todos los archivos de configuración de inquilino incluyen:

* Credenciales del servidor de claves: especifica una o varias credenciales del servidor de claves (certificado y clave privada) emitidas por la Adobe. Se puede especificar como ruta a un [!DNL .pfx] y una contraseña, o un alias para una credencial almacenada en un HSM. Aquí se pueden especificar varias credenciales de este tipo, como rutas de archivo, alias de clave o ambos.

El **iOS** el archivo de configuración de inquilino incluye:

* Ventana de entrega de claves: (Opcional) especifica la ventana de validez de la marca de tiempo de la solicitud de entrega de claves (en segundos). El valor predeterminado es 500 segundos.

El **Xbox 360** el archivo de configuración de inquilino incluye:

* Credencial XSTS: especifica la credencial del desarrollador de la aplicación utilizada para descifrar tokens XSTS
* Certificado de firma XSTS: especifica el certificado utilizado para verificar la firma en los tokens XSTS.
* Lista de permitidos del empaquetador: certificados del empaquetador en los que confía el servidor de claves. Si no hay certificados de empaquetador contenidos en la lista, se confiará en todos los certificados de empaquetador.

## Archivos de registro {#log-files}

Los archivos de registro generados por la aplicación Primetime DRM Key Server ( [!DNL flashaccess-ioskeyserver_*.log] y [!DNL flashaccess-xboxkeyserver_*.log]) se encuentra en el directorio especificado por `KeyServer.LogRoot`.

Los archivos de registro se distinguen por el tipo de cliente. Hay dos registros por tipo de cliente:

* Un *registro de acceso* - Supervisa las solicitudes y respuestas únicamente.
* A *registro de contexto* : contiene mensajes de error detallados y seguimientos de pila.

## Inicio del servidor de claves {#starting-the-key-server}

Para iniciar el servidor de claves, inicie Tomcat.
