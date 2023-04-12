---
title: Configuración del entorno y pruebas en Pre-Qual
description: Configuración del entorno y pruebas en Pre-Qual
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---


# Configuración del entorno y pruebas en Pre-Qual{#setting-up-your-environment-and-testing-in-prequal}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

El propósito de esta nota técnica es ayudar a nuestros socios a configurar su entorno y comenzar a probar una nueva compilación implementada en el entorno de precalificación de Adobe.

Ya que hay dos sabores de construcción: ***producción*** y ***ensayo***, en este documento nos centraremos en la configuración de producción con la mención de que todos los pasos son los mismos para el ensayo, solo las direcciones URL son diferentes.

Los pasos 1 y 2 están configurando el entorno de prueba en una de las máquinas de prueba, el paso 3 es una verificación del flujo básico y los pasos 4 y 5 presentan algunas directrices de prueba.

>[!IMPORTANT]
>
> Es muy importante ejecutar los pasos 1 y 2 cada vez que desee cambiar el entorno de prueba (pasando del ensayo al perfil de producción o al revés)
 

## PASO 1. Resolución de Pasar dominio a una IP {#resolving-pass-domain-to-an-ip}

* Para buscar una IP de equilibrador de carga que pueda utilizarse para la simulación, ejecute el siguiente comando:

* **En Windows**

   ```cmd
   C:\>nslookup sp-prequal.auth.adobe.com
   ...
   Addresses:  52.13.71.11
               54.184.208.150
   ```

```Choose any IP from **addresses** section (e.g. `52.13.71.11)```

* **En Linux/Mac**

```sh
    $ dig sp-prequal.auth.adobe.com
    
    ;; ANSWER SECTION:
    ...
    ............ 60 IN A      52.13.71.11
    ............ 60 IN A      54.184.208.150
```

```Choose any IP from **A records (**e.g `52.13.71.11)```

>[!NOTE]
>
>Los dominios excluidos de la respuesta ya que no son relevantes y podrían diferir de un usuario a otro.

>[!IMPORTANT]
>
> Estas direcciones IP pueden cambiar en el futuro y es posible que no sean las mismas para los usuarios de diferentes regiones geográficas.


## PASO 2.  Creación de suplantación del entorno de precalificación para la producción {#spoofing-the-prequalification-environment}

* Edite el *c:\\windows\\System32\\drivers\\etc\\hosts* archivo (en Windows) o */etc/hosts* (en Macintosh/Linux/Android) y añada lo siguiente:

* Perfil de producción de parodia
   * 52.13.71.11 http://entitlement.auth.adobe.com, http://sp.auth.adobe.com, http://api.auth.adobe.com

**Parpadeo en Android:** Para parpadear en Android, debe utilizar un emulador de Android.

* Una vez que se haya realizado la simulación, simplemente puede utilizar las direcciones URL normales para los perfiles de producción y ensayo: (es decir, `http://sp.auth-staging.adobe.com` y `http://entitlement.auth-staging.adobe.com` y en realidad llegará al *entorno/producción de precalificación* de la* nueva compilación.


## PASO 3.  Compruebe que está señalando al entorno adecuado {#Verify-you-are-pointing-to-the-right-environment}

**Este es un paso fácil:**

* load [entorno de preigualdad de derechos](https://entitlement-prequal.auth.adobe.com/environment.html) y [secundario](https://entitlement.auth.adobe.com/environment.html). Deben devolver la misma respuesta.


## PASO 4.  Realizar un flujo simple de autenticación/autorización utilizando el sitio web del programador {#peform-a-simple-auth-flow}

* Este paso requiere la dirección del sitio web del programador y algunas credenciales de MVPD válidas (un usuario que está autenticado y autorizado).

## PASO 5.  Realizar pruebas de escenario utilizando los sitios web del programador {#perform-scenario-testing-using-programmer-website}

* Después de completar la configuración del entorno y garantizar que el flujo básico de autorización de autenticación funcione, puede continuar con la prueba de escenarios más complejos.


## PASO 6.  Realizar pruebas mediante el sitio de prueba de la API {#perform-testing-using-api-testing-site}

* Si desea profundizar en la prueba de la autenticación de Adobe Primetime, le recomendamos que utilice el [Sitio de prueba de API](http://entitlement-prequal.auth.adobe.com/apitest/api.html).

Puede encontrar más información en el sitio de prueba de la API en [Cómo probar los flujos de autenticación y autorización mediante el sitio de prueba de la API de Adobe](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).

