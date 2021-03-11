---
title: Implementación de la descripción general del servidor de claves DRM de Primetime
description: Implementación de la descripción general del servidor de claves DRM de Primetime
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 0%

---


# Implementar el servidor de claves DRM de Primetime {#deploy-the-primetime-drm-key-server}

Antes de implementar el Servidor de claves DRM de Primetime, asegúrese de que ha instalado las versiones necesarias de Java y Tomcat. Consulte [Requisitos de servidor clave DRM](../../digital-rights-management/using-the-drm-key-server/requirements.md).

La descarga de Primetime DRM Key Server incluye [!DNL faxsks.war]. Para implementar este archivo WAR, copie el archivo en el directorio [!DNL webapps] de Tomcat. Si ha implementado anteriormente el archivo WAR, es posible que tenga que borrar manualmente el directorio WAR desempaquetado, [!DNL faxsks] en el directorio [!DNL webapps] de Tomcat. Para evitar que Tomcat desempaquete archivos WAR, edite el archivo [!DNL server.xml] en el directorio [!DNL conf] de Tomcat y establezca el atributo `unpackWARs` en `false`.

El servidor de claves de Primetime DRM opcionalmente utiliza una biblioteca específica de la plataforma (`jsafe.dll` en Windows o `libjsafe.so` en Linux) para mejorar el rendimiento. Copie la biblioteca adecuada para su plataforma de `thirdparty/cryptoj/platform` a una ubicación especificada por la variable de entorno `PATH` (o `LD_LIBRARY_PATH` en Linux).

>[!NOTE]
>
>La versión de 64 bits de la biblioteca [!DNL jsafe] solo debe usarse si el sistema operativo y JDK admiten 64 bits; de lo contrario, utilice la versión de 32 bits.

## Configuración SSL {#ssl-configuration}

SSL es necesario para la entrega de claves HTTPS remotas. Las conexiones SSL podrían ser gestionadas por el servidor de aplicaciones (es decir, configurando SSL en Tomcat) o se podrían gestionar en otro servidor (es decir, un equilibrador de carga, un acelerador SSL o Apache). La entrega de claves HTTPS remotas requiere una conexión SSL. El servidor necesita un certificado SSL emitido por una CA de confianza.

Existen varias opciones para configurar SSL. A continuación se muestran ejemplos de configuración de SSL con autenticación de cliente en Apache y Tomcat.

El siguiente ejemplo muestra la configuración de Apache SSL:

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

Cuando se le pida el nombre común, utilice el nombre de dominio completo (FQDN) de su servidor.

Copie [!DNL server.cer] y [!DNL server.key] en el directorio Tomcat. Especifique el siguiente conector en [!DNL conf/server.xml]:

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

Tiene la opción de establecer las dos siguientes propiedades del sistema Java para modificar la ubicación de los archivos de configuración y de registro para el servidor de claves DRM de Primetime:

* `KeyServer.ConfigRoot` - Este directorio contiene todos los archivos de configuración del Servidor de claves DRM de Primetime. Para obtener más información sobre el contenido de estos archivos, consulte [Archivos de configuración de Key Server](#key-server-configuration-files). Si no se configura, el valor predeterminado es [!DNL CATALINA_BASE/keyserver].

* `KeyServer.LogRoot` : es un directorio de registro que contiene los registros de la aplicación del servidor de claves iOS. Si no se establece, el valor predeterminado es el mismo que `KeyServer.ConfigRoot`

* `XboxKeyServer.LogRoot` - Este es un directorio de registro que contiene los registros de aplicación de Xbox Key Server. Si no se configura, el valor predeterminado es el mismo que `KeyServer.ConfigRoot`.

Si utiliza [!DNL catalina.bat] o [!DNL catalina.sh] para iniciar Tomcat, estas propiedades del sistema se pueden configurar fácilmente mediante la variable de entorno `JAVA_OPTS` . Cualquier opción de Java configurada aquí se utilizará cuando se inicie Tomcat. Por ejemplo, establezca:

```
JAVA_OPTS=-DKeyServer.ConfigRoot=”absolute-path-to-config-folder” 
  -DKeyServer.LogRoot=”absolute-path-to-log-folder”
```

## Credenciales de DRM de Primetime {#primetime-drm-credentials}

Para procesar solicitudes clave de clientes Primetime DRM iOS y Xbox 360, el servidor de claves Primetime DRM debe configurarse con un conjunto de credenciales emitidas por Adobe. Estas credenciales se pueden almacenar en archivos PKCS#12 ( [!DNL .pfx]) o en un HSM.

Los archivos [!DNL .pfx] se pueden ubicar en cualquier lugar, pero para facilitar la configuración, Adobe recomienda colocar los archivos [!DNL .pfx] en el directorio de configuración del inquilino. Para obtener más información, consulte [Archivos de configuración de Key Server](#key-server-configuration-files).

### Configuración de HSM {#section_13A19E3E32934C5FA00AEF621F369877}

Si decide utilizar un HSM para almacenar sus credenciales de servidor, debe cargar las claves privadas y los certificados en el HSM y crear un archivo de configuración *pkcs11.cfg*. Este archivo debe encontrarse en el directorio *KeyServer.ConfigRoot*. Consulte el directorio `<Primetime DRM Key Server>/configs` para ver un archivo de configuración PKCS 11 de ejemplo. Para obtener información sobre el formato de [!DNL pkcs11.cfg], consulte la documentación del proveedor Sun PKCS11.

Para comprobar que los archivos de configuración HSM y Sun PKCS11 están correctamente configurados, puede utilizar el siguiente comando desde el directorio en el que se encuentra el archivo [!DNL pkcs11.cfg] ( [!DNL keytool] está instalado con Java JRE y JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Si ve sus credenciales en la lista, el HSM está configurado correctamente y el servidor de claves podrá acceder a las credenciales.

## Archivos de configuración del servidor clave {#key-server-configuration-files}

El servidor de claves DRM de Primetime requiere dos tipos de archivos de configuración:

* Un archivo de configuración global, [!DNL flashaccess-keyserver-global.xml]
* Un archivo de configuración de inquilino para cada inquilino, [!DNL flashaccess-keyserver-tenant.xml]

Si se realizan cambios en los archivos de configuración, el servidor debe reiniciarse para que los cambios surtan efecto.

Para evitar que las contraseñas estén disponibles en texto claro en los archivos de configuración, todas las contraseñas especificadas en los archivos de configuración global e inquilino deben cifrarse. Para obtener más información sobre el cifrado de contraseñas, consulte [*Contraseña Scrambler* en *Uso del servidor Primetime DRM para transmisión protegida*](../protected-streaming/understanding-deployment/drm-for-protected-streaming-utilities/password-scrambler.md).

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

El archivo de configuración [!DNL flashaccess-keyserver-global.xml] contiene opciones que se aplican a todos los inquilinos del servidor de claves. Este archivo debe estar ubicado en `KeyServer.ConfigRoot`. Consulte el directorio [!DNL configs] para ver un archivo de configuración global de ejemplo. El archivo de configuración global incluye lo siguiente:

* Registro : especifica el nivel de registro y la frecuencia con la que se rompen los archivos de registro.
* Contraseña de HSM: solo es necesaria si se utiliza un HSM para almacenar credenciales de servidor.

Consulte los comentarios en el archivo de configuración global de ejemplo ubicado en `<Primetime DRM Key Server>/configs` para obtener más información.

## Archivos de configuración del inquilino {#tenant-configuration-files}

Los archivos de configuración [!DNL flashaccess-ioskeyserver-tenant.xml] y [!DNL flashaccess-xboxkeyserver-tenant.xml] contienen configuraciones que se aplican a un inquilino específico del Servidor de claves DRM de Primetime. Cada inquilino tiene su propia instancia de estos archivos de configuración ubicados en [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]. Consulte el directorio [!DNL configs/faxsks/tenants/sampletenant] para ver un archivo de configuración de inquilino de ejemplo.

Puede especificar todas las rutas del archivo en el archivo de configuración del inquilino como rutas absolutas o rutas relativas al directorio de configuración del inquilino ( [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]).

Todos los archivos de configuración de inquilino incluyen:

* Credenciales clave del servidor: especifica una o varias credenciales de servidor de claves (certificado y clave privada) emitidas por el Adobe. Se puede especificar como una ruta a un archivo [!DNL .pfx] y una contraseña, o un alias para una credencial almacenada en un HSM. Aquí se pueden especificar varias credenciales de este tipo, como rutas de archivo, alias clave o ambas.

El archivo de configuración del inquilino **iOS** incluye:

* Ventana de entrega de claves : (opcional) especifica la ventana de validez de la marca de tiempo de la solicitud de entrega de claves (en segundos). El valor predeterminado es 500 segundos.

El archivo de configuración de inquilino **Xbox 360** incluye:

* Credencial XSTS: especifica la credencial del desarrollador de la aplicación utilizada para descifrar tokens XSTS
* Certificado de firma XSTS : especifica el certificado utilizado para verificar la firma en los tokens XSTS.
* Lista de permitidos de Packager : certificados de Packager en los que el servidor de claves confía. Si no hay certificados de empaquetador contenidos en la lista, todos los certificados de empaquetador serán de confianza.

## Archivos de registro {#log-files}

Los archivos de registro generados por la aplicación Primetime DRM Key Server ( [!DNL flashaccess-ioskeyserver_*.log] y [!DNL flashaccess-xboxkeyserver_*.log]) se ubicarán en el directorio especificado por `KeyServer.LogRoot`.

Los archivos de registro se distinguen por tipo de cliente. Hay dos registros por tipo de cliente:

* Un *registro de acceso*: solo supervisa las solicitudes y respuestas.
* Un *registro de contexto* : contiene mensajes de error detallados y seguimientos de pila.

## Inicio del servidor de claves {#starting-the-key-server}

Para iniciar el servidor de claves, inicie Tomcat.