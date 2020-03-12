---
seo-title: Implementación del servidor de claves DRM Primetime información general
title: Implementación del servidor de claves DRM Primetime información general
uuid: 86630675-c15d-4f32-8212-d7343f4f92e0
translation-type: tm+mt
source-git-commit: 105dedcfe47a5f454a067e66a95827e638290742

---


# Implementar el servidor de claves DRM Primetime {#deploy-the-primetime-drm-key-server}

Antes de implementar Primetime DRM Key Server, asegúrese de haber instalado las versiones necesarias de Java y Tomcat. Consulte Requisitos [del servidor clave](../../digital-rights-management/using-the-drm-key-server/requirements.md)DRM.

La descarga de Primetime DRM Key Server incluye [!DNL faxsks.war]. Para implementar este archivo WAR, copie el archivo en el directorio de Tomcat [!DNL webapps] . Si ya ha implementado el archivo WAR, es posible que tenga que borrar manualmente el directorio WAR desempacado, [!DNL faxsks] en el [!DNL webapps] directorio de Tomcat). Para evitar que Tomcat descomprima archivos WAR, edite el [!DNL server.xml] archivo en el directorio [!DNL conf] de Tomcat y defina el `unpackWARs` atributo en `false`.

El servidor de claves Primetime DRM utiliza opcionalmente una biblioteca específica de la plataforma (`jsafe.dll` en Windows o `libjsafe.so` en Linux) para mejorar el rendimiento. Copie la biblioteca adecuada para su plataforma de `thirdparty/cryptoj/platform` a una ubicación especificada por la variable de `PATH` entorno (o `LD_LIBRARY_PATH` en Linux).

>[!NOTE]
>
>La versión de 64 bits de la [!DNL jsafe] biblioteca solo debe utilizarse si tanto el sistema operativo como JDK admiten 64 bits; de lo contrario, utilice la versión de 32 bits.

## Configuración SSL {#ssl-configuration}

Se requiere SSL para la entrega de claves HTTPS remotas. Las conexiones SSL podrían ser manejadas por el servidor de aplicaciones (es decir, configurando SSL en Tomcat) o pueden ser manejadas por otro servidor (es decir, un equilibrador de carga, un acelerador SSL o Apache). La entrega remota de claves HTTPS requiere una conexión SSL. El servidor necesita un certificado SSL emitido por una CA de confianza.

Existen diversas opciones para configurar SSL. A continuación se muestran ejemplos para configurar SSL con autenticación de cliente en Apache y Tomcat.

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

Cuando se le pida el nombre común, utilice el nombre de dominio completo (FQDN) del servidor.

Copie [!DNL server.cer]y [!DNL server.key] en el directorio Tomcat. Especifique el siguiente conector en [!DNL conf/server.xml]:

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

Tiene la opción de establecer las dos siguientes propiedades del sistema Java para modificar la ubicación de los archivos de configuración y registro para el servidor de claves DRM Primetime:

* `KeyServer.ConfigRoot` - Este directorio contiene todos los archivos de configuración para el servidor de claves Primetime DRM. Para obtener más información sobre el contenido de estos archivos, consulte Archivos [de configuración de](#key-server-configuration-files)Key Server. Si no se establece, el valor predeterminado es [!DNL CATALINA_BASE/keyserver].

* `KeyServer.LogRoot` - Es un directorio de registro que contiene los registros de la aplicación iOS Key Server. Si no se establece, el valor predeterminado es el mismo que `KeyServer.ConfigRoot`

* `XboxKeyServer.LogRoot` - Este es un directorio de registro que contiene los registros de la aplicación Xbox Key Server. Si no se establece, el valor predeterminado es el mismo que `KeyServer.ConfigRoot`.

Si utiliza [!DNL catalina.bat] o [!DNL catalina.sh] para iniciar Tomcat, estas propiedades del sistema se pueden establecer fácilmente con la variable `JAVA_OPTS` environment. Cualquier opción de Java configurada aquí se utilizará cuando se inicie Tomcat. Por ejemplo, set:

```
JAVA_OPTS=-DKeyServer.ConfigRoot=”absolute-path-to-config-folder” 
  -DKeyServer.LogRoot=”absolute-path-to-log-folder”
```

## Credenciales de DRM de Primetime {#primetime-drm-credentials}

Para procesar solicitudes clave de clientes Primetime DRM iOS y Xbox 360, el servidor de claves Primetime DRM debe configurarse con un conjunto de credenciales emitidas por Adobe. Estas credenciales se pueden almacenar en archivos PKCS#12 ( [!DNL .pfx]) o en un HSM.

Los [!DNL .pfx] archivos se pueden ubicar en cualquier lugar, pero para facilitar la configuración, Adobe recomienda colocar los [!DNL .pfx] archivos en el directorio de configuración del inquilino. Para obtener más información, consulte Archivos [de configuración de](#key-server-configuration-files)Key Server.

### Configuración de HSM {#section_13A19E3E32934C5FA00AEF621F369877}

Si decide utilizar un HSM para almacenar sus credenciales de servidor, debe cargar las claves privadas y los certificados en el HSM y crear un archivo de configuración *pkcs11.cfg* . Este archivo debe encontrarse en el directorio *KeyServer.ConfigRoot* . Consulte la [!DNL <Primetime DRM Key Server>/configs] para un archivo de configuración PKCS 11 de ejemplo. Para obtener información sobre el formato de [!DNL pkcs11.cfg], consulte la documentación del proveedor PKCS11 de Sun.

Para comprobar que los archivos de configuración de HSM y Sun PKCS11 están correctamente configurados, puede utilizar el siguiente comando desde el directorio donde se encuentra el [!DNL pkcs11.cfg] archivo ( [!DNL keytool] se instala con Java JRE y JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Si ve sus credenciales en la lista, el HSM está configurado correctamente y el servidor clave podrá acceder a las credenciales.

## Archivos de configuración de Key Server {#key-server-configuration-files}

Primetime DRM Key Server requiere dos tipos de archivos de configuración:

* Un archivo de configuración global, [!DNL flashaccess-keyserver-global.xml]
* Un archivo de configuración de inquilino para cada inquilino, [!DNL flashaccess-keyserver-tenant.xml]

Si se realizan cambios en los archivos de configuración, se debe reiniciar el servidor para que los cambios surtan efecto.

Para evitar que las contraseñas estén disponibles en texto sin formato en los archivos de configuración, todas las contraseñas especificadas en los archivos de configuración global e inquilino deben estar cifradas. Para obtener más información sobre la codificación de contraseñas, consulte [*Password Scrambler *en* Uso del servidor Primetime DRM para flujo *](../protected-streaming/understanding-deployment/drm-for-protected-streaming-utilities/password-scrambler.md)protegido.

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

El archivo de configuración [!DNL flashaccess-keyserver-global.xml] contiene opciones que se aplican a todos los inquilinos del servidor de claves. Este archivo debe estar ubicado en `KeyServer.ConfigRoot`. Consulte el [!DNL configs] directorio para ver un archivo de configuración global de ejemplo. El archivo de configuración global incluye lo siguiente:

* Registro: especifica el nivel de registro y la frecuencia con la que se desplazan los archivos de registro.
* Contraseña de HSM: solo se requiere si se utiliza un HSM para almacenar las credenciales del servidor.

Consulte los comentarios del archivo de configuración global de ejemplo ubicado en [!DNL <Primetime DRM Key Server>/configs] para obtener más información.

## Archivos de configuración del inquilino {#tenant-configuration-files}

Los archivos [!DNL flashaccess-ioskeyserver-tenant.xml] [!DNL flashaccess-xboxkeyserver-tenant.xml] y de configuración contienen opciones que se aplican a un inquilino específico del servidor de claves DRM Primetime. Cada inquilino tiene su propia instancia de estos archivos de configuración ubicados en [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]. Consulte el [!DNL configs/faxsks/tenants/sampletenant] directorio para ver un archivo de configuración de inquilino de ejemplo.

Puede especificar todas las rutas de archivo del archivo de configuración del inquilino como rutas absolutas o rutas relativas al directorio de configuración del inquilino ( [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]).

Todos los archivos de configuración de inquilinos incluyen:

* Credenciales de servidor clave: especifica una o varias credenciales de servidor clave (certificado y clave privada) emitidas por Adobe. Se puede especificar como una ruta a un [!DNL .pfx] archivo y una contraseña, o como un alias para una credencial almacenada en un HSM. Aquí se pueden especificar varias credenciales de este tipo, ya sea como rutas de archivos, alias de claves o ambas.

El archivo de configuración del inquilino de **iOS** incluye:

* Ventana de entrega de claves: (opcional) especifica la ventana de validez de la marca de hora de la solicitud de entrega de claves (en segundos). El valor predeterminado es 500 segundos.

El archivo de configuración del inquilino de **Xbox 360** incluye:

* Credencial XSTS: especifica la credencial del desarrollador de la aplicación utilizada para descifrar tokens XSTS
* Certificado de firma XSTS: especifica el certificado utilizado para verificar la firma en los tokens XSTS.
* Lista blanca de Packager: certificados de Packager en los que el servidor de claves confía. Si no hay certificados de empaquetador en la lista, todos los certificados de empaquetador serán de confianza.

## Archivos de registro {#log-files}

Los archivos de registro generados por la aplicación Primetime DRM Key Server ( [!DNL flashaccess-ioskeyserver_*.log] y [!DNL flashaccess-xboxkeyserver_*.log]) se ubicarán en el directorio especificado por `KeyServer.LogRoot`.

Los archivos de registro se distinguen por tipo de cliente. Hay dos registros por tipo de cliente:

* Registro *de* acceso: solo supervisa las solicitudes y las respuestas.
* Registro *de* contexto: contiene mensajes de error detallados y trazos de pila.

## Inicio del servidor de claves {#starting-the-key-server}

Para iniciar Key Server, inicie Tomcat.