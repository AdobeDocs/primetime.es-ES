---
title: Configurar el entorno y realizar pruebas en la calidad previa
description: Configurar el entorno y realizar pruebas en la calidad previa
exl-id: f822c0a1-045a-401f-a44f-742ed25bfcdc
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Configurar el entorno y realizar pruebas en la calidad previa{#setting-up-your-environment-and-testing-in-prequal}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite el uso no autorizado.

El propósito de esta nota técnica es ayudar a nuestros socios a configurar su entorno e iniciar la prueba de una nueva compilación implementada en el entorno de precalificación de Adobe.

Dado que hay dos tipos de compilación: ***producción*** y ***puesta en escena*** Sin embargo, en este documento nos centraremos en la configuración de producción con la mención de que todos los pasos son los mismos para el ensayo, solo que las URL son diferentes.

Los pasos 1 y 2 configuran el entorno de prueba en una de las máquinas de prueba, el paso 3 es una verificación del flujo básico y los pasos 4 y 5 presentan algunas directrices de prueba.

>[!IMPORTANT]
>
> Es muy importante ejecutar los pasos 1 y 2 cada vez que desee cambiar el entorno de prueba (pasando del ensayo al perfil de producción o al contrario)
 

## PASO 1. Resolver el paso del dominio a una dirección IP {#resolving-pass-domain-to-an-ip}

* Para buscar una IP del equilibrador de carga que se pueda usar para la suplantación, ejecute el siguiente comando:

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
>Los dominios excluidos de la respuesta porque no son relevantes y podrían diferir de un usuario a otro.

>[!IMPORTANT]
>
> Estas direcciones IP pueden cambiar en el futuro y es posible que no sean iguales para los usuarios de diferentes regiones geográficas.


## PASO 2.  Suplantación del entorno de precalificación para que sea producción {#spoofing-the-prequalification-environment}

* Edite el *c:\\windows\\System32\\drivers\\etc\\hosts* (en Windows) o */etc/hosts* (en Macintosh/Linux/Android) y agregue lo siguiente:

* Perfil de producción de parodia
   * 52.13.71.11 http://entitlement.auth.adobe.com, http://sp.auth.adobe.com, http://api.auth.adobe.com

**Suplantación en Android:** Para falsificar en Android, debe utilizar un emulador de Android.

* Una vez configurada la suplantación, puede utilizar las direcciones URL normales para los perfiles de producción y ensayo: (es decir, `http://sp.auth-staging.adobe.com` y `http://entitlement.auth-staging.adobe.com` y de hecho le darás a la *entorno/producción de precalificación* de la* nueva compilación.


## PASO 3.  Compruebe que está apuntando al entorno correcto {#Verify-you-are-pointing-to-the-right-environment}

**Este es un paso fácil:**

* cargar [entorno de preigualdad de derechos](https://entitlement-prequal.auth.adobe.com/environment.html) y [derecho](https://entitlement.auth.adobe.com/environment.html). Deberían devolver la misma respuesta.


## PASO 4.  Realice un flujo de autenticación/autorización sencillo utilizando el sitio web del programador {#peform-a-simple-auth-flow}

* Este paso requiere la dirección del sitio web del programador y algunas credenciales de MVPD válidas (un usuario que esté autenticado y autorizado).

## PASO 5.  Realizar pruebas de situación utilizando los sitios web del programador {#perform-scenario-testing-using-programmer-website}

* Después de completar la configuración del entorno y asegurarse de que el flujo básico de autenticación-autorización funciona, puede continuar con la prueba de escenarios más complejos.


## PASO 6.  Realizar pruebas mediante el sitio de prueba de la API {#perform-testing-using-api-testing-site}

* Si desea profundizar en la prueba de la autenticación de Adobe Primetime, le recomendamos que utilice la variable [Sitio de prueba de API](http://entitlement-prequal.auth.adobe.com/apitest/api.html).

Puede encontrar más detalles sobre el sitio de prueba de la API en [Prueba de los flujos de autenticación y autorización mediante el sitio de prueba de la API de Adobe](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).
