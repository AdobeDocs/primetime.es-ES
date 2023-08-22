---
title: Configurar el entorno y realizar pruebas en la calidad previa
description: Configurar el entorno y realizar pruebas en la calidad previa
exl-id: f822c0a1-045a-401f-a44f-742ed25bfcdc
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Configuración del entorno y prueba de antemano{#setting-up-your-environment-and-testing-in-prequal}

>[!NOTE]
>
>La contenido en esta Página se ofrece únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe Systems. No se permite el uso no autorizado.

El objetivo de esta nota técnica es ayudar a nuestros socios a configurar sus entorno y inicio a probar una nueva versión implementada en los entorno Adobe Systems previas a la calificación.

Dado que hay dos tipos de versión: ***producción*** y ***ensayo*** , en este documento se enfocar en la configuración de producción con la mención de que todos los pasos son los mismos para el ensayo, pero solo las direcciones URL son diferentes.

Los pasos 1 y 2 están configurando el prueba entorno en uno de los equipos de prueba, el paso 3 es una verificación del flujo básico y los pasos 4 a 5 de la presentación de algunas pautas de prueba.

>[!IMPORTANT]
>
> Es muy importante que ejecute los pasos 1 y 2 cada vez que desee cambiar la entorno de la prueba (cambio del ensayo a perfil de producción o viceversa)


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
>Los dominios se excluyen de la respuesta porque no son relevantes y pueden diferir de usuario a usuario.

>[!IMPORTANT]
>
> Estas direcciones IP pueden cambiar en el futuro y es posible que no sean las mismas para los usuarios de diferentes regiones geográficas.


## PASO 2.  Suplantación de la entorno previa a la calificación para la producción {#spoofing-the-prequalification-environment}

* Editar el archivo C:\\windows\\System32\\drivers\\etc\\hosts *(en Windows) o* el *archivo/etc/hosts* (en Macintosh/Linux/Android) y agregue lo siguiente:

* perfil de producción falsas
   * 52.13.71.11 http://entitlement.auth.adobe.com, http://sp.auth.adobe.com, http://api.auth.adobe.com

**Suplantación en Android:** Para falsificar en Android, debe utilizar un emulador de Android.

* Una vez configurada la suplantación, puede utilizar las direcciones URL normales para los perfiles de producción y ensayo: (es decir, `http://sp.auth-staging.adobe.com` y `http://entitlement.auth-staging.adobe.com` y de hecho le darás a la *entorno/producción de precalificación* de la* nueva compilación.


## PASO 3.  Compruebe que está apuntando al entorno correcto {#Verify-you-are-pointing-to-the-right-environment}

**Este es un paso fácil:**

* Cargue [ el derecho prequal entorno ](https://entitlement-prequal.auth.adobe.com/environment.html) y [ derecho ](https://entitlement.auth.adobe.com/environment.html) . Deben devolver la misma respuesta.


## PASO 4.  Realización de un flujo simple de autenticación/autorización mediante el sitio web del programador {#peform-a-simple-auth-flow}

* Este paso requiere la dirección del sitio web del programador y algunas credenciales de MVPD válidas (una usuario que está autenticada y autorizada).

## PASO 5.  Realización de pruebas de escenarios con los sitios web del programador {#perform-scenario-testing-using-programmer-website}

* Una vez completada la configuración de entorno y asegurándose de que el flujo básico de autorización de autenticación esté funcionando, puede continuar con la prueba de escenarios más complejos.


## PASO 6.  Realizar pruebas mediante el sitio de prueba de la API {#perform-testing-using-api-testing-site}

* Si desea profundizar en la prueba de la autenticación de Adobe Primetime, le recomendamos que utilice la variable [Sitio de prueba de API](http://entitlement-prequal.auth.adobe.com/apitest/api.html).

Puede encontrar más detalles sobre el sitio de prueba de la API en [Prueba de los flujos de autenticación y autorización mediante el sitio de prueba de la API de Adobe](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).
