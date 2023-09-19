---
title: Información general sobre la implementación de modelos de uso
description: Información general sobre la implementación de modelos de uso
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# Información general sobre la implementación de modelos de uso {#implementing-the-usage-models-overview}

La implementación de referencia incluye lógica empresarial para mostrar cómo habilitar los siguientes cuatro modelos de uso diferentes para un fragmento de contenido empaquetado:

* Descarga para su propiedad (DTO)
* Alquiler/vídeo bajo demanda (VOD)
* Suscripción (todo lo que puedas comer)
* Financiado por publicidad

Para habilitar la demostración del modelo de uso, especifique la propiedad personalizada `RI_UsageModelDemo=true` en el momento del embalaje. Si va a empaquetar contenido mediante la herramienta de línea de comandos del empaquetador de medios, especifique:

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE]
>
>Si no activa el modo de demostración opcional en el momento del empaquetado, el servidor de licencias utilizará la directiva especificada en el momento del empaquetado para emitir una licencia. Si se especifican varias directivas, el servidor de licencias utiliza la primera directiva válida.

En la demostración, la lógica empresarial del servidor controla los atributos reales de las licencias generadas. En el momento del empaquetado, solo se debe incluir información mínima sobre las políticas en el contenido. En concreto, la directiva solo necesita indicar si se requiere autenticación para acceder al contenido. Para habilitar los cuatro modelos de uso, incluya una política que permita el acceso anónimo (para el modelo financiado con publicidad) y una política que requiera la autenticación de nombre de usuario/contraseña (para los otros 3 modelos de uso). Al solicitar una licencia, una aplicación cliente puede determinar si se debe solicitar la autenticación al usuario basándose en la información de autenticación de las directivas.

Para controlar el modelo de uso en el que se va a otorgar una licencia a un usuario en particular, se pueden añadir entradas a la base de datos de implementación de referencia. El `Customer` contiene los nombres de usuario y contraseñas para autenticar a los usuarios. También indica si el usuario tiene una suscripción. Los usuarios con suscripciones recibirán licencias con el *Suscripción* modelo de uso. Para otorgar acceso a un usuario en *Descargar para uso propio* o *Vídeo bajo demanda* modelos de uso, se puede añadir una entrada al `CustomerAuthorization` , que especifica cada fragmento de contenido al que el usuario puede acceder y el modelo de uso. Consulte la [!DNL PopulateSampleDB.sql] para obtener detalles sobre cómo rellenar cada tabla.

Cuando un usuario solicita una licencia, el servidor de implementación de referencia comprueba los metadatos enviados por el cliente para determinar si el contenido se empaquetó utilizando `RI_UsageModelDemo` propiedad. Si es así, se utilizan las siguientes reglas empresariales:

* Si una de las directivas requiere autenticación:

   * Si la solicitud contiene un token de autenticación válido, busque el usuario en la tabla de la base de datos de clientes. Si se encontró el usuario:

      * Si la variable `Customer.IsSubscriber` la propiedad es `true`, genere una licencia para *Suscripción* modelo de uso y enviarlo al usuario.

      * Busque un registro en la `CustomerAuthorization` tabla de base de datos para este usuario y el ID de contenido. Si se encontró un registro:

         * If `CustomerAuthorization.UsageType` es `DTO`, genere una licencia para *Descargar Para Poseer* modelo de uso y enviarlo al usuario.

         * If `CustomerAuthorization.UsageType` es `VOD`, genere una licencia para *Vídeo bajo demanda* modelo de uso y enviarlo al usuario.

   * Si ninguna de las directivas permite el acceso anónimo:

      * Si no hay un token de autenticación válido en la solicitud, devuelva el error &quot;se requiere autenticación&quot;.
      * De lo contrario, devuelve el error &quot;no autorizado&quot;.

* Si una de las políticas permite el acceso anónimo, genere una licencia para el modelo de uso financiado con publicidad y envíela al usuario.

Antes de que el servidor de implementación de referencia pueda emitir licencias para la demostración del modelo de uso, el servidor debe configurarse para especificar cómo se generan las licencias para cada uno de los cuatro modelos de uso. Esto se hace especificando una directiva para cada modelo de uso. La Implementación de referencia incluye cuatro directivas de ejemplo ( [!DNL dto-policy.pol], [!DNL vod-policy.pol], [!DNL sub-policy.pol], [!DNL ad-policy.pol]) o puede sustituir sus propias directivas. Entrada [!DNL flashaccess-refimpl.properties], establezca las siguientes propiedades para especificar la directiva que se utilizará para cada modelo de uso y coloque los archivos de directiva en el directorio especificado por `config.resourcesDirectory` propiedad:

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
