---
title: Información general sobre la implementación de los modelos de uso
description: Información general sobre la implementación de los modelos de uso
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# Información general sobre la implementación de modelos de uso {#implementing-the-usage-models-overview}

La implementación de referencia incluye lógica empresarial para demostrar cómo habilitar los siguientes cuatro modelos de uso diferentes para un fragmento de contenido empaquetado:

* Descargar en propiedad (DTO)
* Alquiler/Vídeo bajo demanda (VOD)
* Suscripción (todo lo que se pueda comer)
* Con financiación publicitaria

Para habilitar la demostración del modelo de uso, especifique la propiedad personalizada `RI_UsageModelDemo=true` en el momento del empaquetado. Si empaqueta contenido con la herramienta de línea de comandos de Media Packager, especifique:

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE]
>
>Si no activa el modo de demostración opcional en el momento del empaquetado, el servidor de licencias utiliza la directiva especificada en el momento del empaquetado para emitir una licencia. Si se especificaron varias directivas, el servidor de licencias utiliza la primera directiva válida.

En la demostración, la lógica empresarial del servidor controla los atributos reales de las licencias generadas. En el momento del empaquetado, solo debe incluirse en el contenido una información de política mínima. En concreto, la directiva solo necesita indicar si se requiere autenticación para acceder al contenido. Para habilitar los cuatro modelos de uso, incluya una directiva que permita el acceso anónimo (para el modelo financiado con Ad) y una directiva que requiera autenticación de nombre de usuario/contraseña (para los otros 3 modelos de uso). Al solicitar una licencia, una aplicación cliente puede determinar si se solicita al usuario la autenticación en función de la información de autenticación de las directivas.

Para controlar el modelo de uso en el que se va a expedir una licencia a un usuario en particular, se pueden añadir entradas a la base de datos de Implementación de referencia. La tabla `Customer` contiene nombres de usuario y contraseñas para autenticar usuarios. También indica si el usuario tiene una suscripción. Los usuarios con suscripciones recibirán licencias bajo el modelo de uso *Subscription* . Para conceder acceso a un usuario en los modelos de uso *Download to Own* o *Video on Demand* , se puede agregar una entrada a la tabla `CustomerAuthorization`, que especifica cada parte de contenido a la que el usuario puede acceder y el modelo de uso. Consulte la secuencia de comandos [!DNL PopulateSampleDB.sql] para obtener más información sobre cómo rellenar cada tabla.

Cuando un usuario solicita una licencia, el servidor de implementación de referencia comprueba los metadatos enviados por el cliente para determinar si el contenido se empaquetó con la propiedad `RI_UsageModelDemo` . Si es así, se utilizan las siguientes reglas comerciales:

* Si una de las directivas requiere autenticación:

   * Si la solicitud contiene un token de autenticación válido, busque el usuario en la tabla de la base de datos del cliente. Si se encontró el usuario:

      * Si la propiedad `Customer.IsSubscriber` es `true`, genere una licencia para el modelo de uso *Subscription* y envíela al usuario.

      * Busque un registro en la tabla de la base de datos `CustomerAuthorization` para este usuario y el ID de contenido. Si se encontró un registro:

         * Si `CustomerAuthorization.UsageType` es `DTO`, genere una licencia para el modelo de uso *Download To Own* y envíela al usuario.

         * Si `CustomerAuthorization.UsageType` es `VOD`, genere una licencia para el modelo de uso de *Video On Demand* y envíela al usuario.
   * Si ninguna de las políticas permite el acceso anónimo:

      * Si no hay un token de autenticación válido en la solicitud, devuelva un error de &quot;autenticación requerida&quot;.
      * De lo contrario, devuelve un error &quot;no autorizado&quot;.


* Si una de las políticas permite el acceso anónimo, genere una licencia para el modelo de uso financiado por Ad y envíelo al usuario.

Para que el servidor de implementación de referencia pueda emitir licencias para la demostración del modelo de uso, debe configurarse el servidor para especificar cómo se generan las licencias para cada uno de los cuatro modelos de uso. Esto se hace especificando una directiva para cada modelo de uso. La Implementación de referencia incluye cuatro políticas de muestra ( [!DNL dto-policy.pol], [!DNL vod-policy.pol], [!DNL sub-policy.pol], [!DNL ad-policy.pol]) o puede sustituir sus propias políticas. En [!DNL flashaccess-refimpl.properties], establezca las siguientes propiedades para especificar la directiva que se utilizará para cada modelo de uso y coloque los archivos de directiva en el directorio especificado por la propiedad `config.resourcesDirectory` :

```
# Policy file name for Download To Own usage  
RefImpl.UsageModelDemo.Policy.DTO=dto-policy.pol  
# Policy file name for Rental usage  
RefImpl.UsageModelDemo.Policy.VOD=vod-policy.pol  
# Policy file name for Subscription usage  
RefImpl.UsageModelDemo.Policy.Subscribe=sub-policy.pol  
# Policy file name for Ad Supported (free) usage  
RefImpl.UsageModelDemo.Policy.Free=ad-policy.pol
```

