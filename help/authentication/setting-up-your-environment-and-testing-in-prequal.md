---
title: Configurar el entorno y realizar pruebas en la calidad previa
description: Configurar el entorno y realizar pruebas en la calidad previa
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Configuración del entorno y pruebas en Pre-Qual{#setting-up-your-environment-and-testing-in-prequal}

>[!NOTE]
>
>Los contenido de este Página se proporcionan únicamente con fines informativos. El uso de esta API requiere una licencia vigente de Adobe Systems. No se permite ningún uso no autorizado.

El propósito de esta nota técnica es ayudar a nuestros socios a configurar sus entorno y inicio probar un nuevo versión implementado en el Adobe Systems entorno de precalificación.

Dado que hay dos versión sabores: ***producción y*** puesta en escena, en este documento enfocar en la configuración de producción ***con la mención de que todos los pasos son iguales para la puesta en escena***, solo que las URL son diferentes.

Los pasos 1 y 2 están configurando el prueba entorno en una de las máquinas de prueba, el paso 3 es una verificación del flujo básico y los pasos 4 y 5 presentan algunas pautas de prueba.

>[!IMPORTANT]
>
> Es muy importante ejecutar los pasos 1 y 2 cada vez que desee cambiar su entorno de prueba (cambiar de ensayo a perfil de producción, o al revés)


## PASO 1. Resolver el paso del dominio a una dirección IP {#resolving-pass-domain-to-an-ip}

* Para buscar una IP del equilibrador de carga que se pueda usar para la suplantación, ejecute el siguiente comando:

* **En Windows**

  ```cmd
  C:\>nslookup sp-prequal.auth.adobe.com
  ...
  Addresses:  52.13.71.11
              54.184.208.150
  ```

```Choose any IP from **addresses** section (e.g. `52.13.71.11)```

* **En Linux/Mac**

```sh
    $ dig sp-prequal.auth.adobe.com
    
    ;; ANSWER SECTION:
    ...
    ............ 60 IN A      52.13.71.11
    ............ 60 IN A      54.184.208.150
```

```Choose any IP from **A records (**e.g `52.13.71.11)```

>[!NOTE]
>
>Dominios excluidos de la respuesta, ya que no son relevantes y pueden diferir de un usuario a usuario otro.

>[!IMPORTANT]
>
> Estas direcciones IP pueden cambiar en el futuro y pueden no ser las mismas para los usuarios de diferentes regiones geográficas.


## PASO 2.  Suplantación de la precalificación entorno para ser producción {#spoofing-the-prequalification-environment}

* Editar el archivo c:\\windows\\System32\\drivers\\etc\\hosts (en Windows) o *el* archivo /etc/hosts ** (en Macintosh/Linux/Android) y añada lo siguiente:

* Producción de suplantación de identidad perfil
   * 52.13.71.11 http://entitlement.auth.adobe.com, http://sp.auth.adobe.com http://api.auth.adobe.com

**Suplantación en Android:** Para falsificar en Android, debe utilizar un emulador de Android.

* Una vez configurada la suplantación, puede utilizar las direcciones URL normales para los perfiles de producción y ensayo: (es decir, `http://sp.auth-staging.adobe.com` y `http://entitlement.auth-staging.adobe.com` y de hecho le darás a la *entorno/producción de precalificación* de la* nueva compilación.


## PASO 3.  Compruebe que está apuntando al entorno correcto {#Verify-you-are-pointing-to-the-right-environment}

**Este es un paso fácil:**

* Load [Entitlement prequal entorno](https://entitlement-prequal.auth.adobe.com/environment.html) and [entitlement](https://entitlement.auth.adobe.com/environment.html). Deben devolver la misma respuesta.


## PASO 4.  Realice un flujo simple de autenticación/autorización utilizando el sitio web del programador {#peform-a-simple-auth-flow}

* Este paso requiere la dirección del sitio web del programador y algunas credenciales MVPD válidas (un usuario de que esté autenticado y autorizado).

## PASO 5.  Realizar pruebas de escenarios utilizando los sitios web del programador {#perform-scenario-testing-using-programmer-website}

* Después de completar la configuración entorno y asegurarse de que funciona el flujo básico de autenticación-autorización, puede continuar con las pruebas de escenarios más complejos.


## PASO 6.  Realizar pruebas mediante el sitio de prueba de la API {#perform-testing-using-api-testing-site}

* Si desea profundizar en la prueba de la autenticación de Adobe Primetime, le recomendamos que utilice la variable [Sitio de prueba de API](http://entitlement-prequal.auth.adobe.com/apitest/api.html).

Puede encontrar más detalles sobre el sitio de prueba de la API en [Prueba de los flujos de autenticación y autorización mediante el sitio de prueba de la API de Adobe](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).
