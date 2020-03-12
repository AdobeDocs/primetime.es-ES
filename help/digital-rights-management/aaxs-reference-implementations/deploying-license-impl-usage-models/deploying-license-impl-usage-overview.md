---
seo-title: Introducción a la implementación de los modelos de uso
title: Introducción a la implementación de los modelos de uso
uuid: 1041bb84-9996-4284-b2a0-d6fc6d4b73d9
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Introducción a la implementación de los modelos de uso {#implementing-the-usage-models-overview}

La implementación de referencia incluye lógica empresarial para demostrar cómo habilitar los cuatro modelos de uso siguientes para un fragmento de contenido empaquetado:

* Descargar en propiedad (DTO)
* Alquiler/Vídeo a petición (VOD)
* Suscripción (todo lo que pueda comer)
* Financiado con publicidad

Para habilitar la demostración del modelo de uso, especifique la propiedad personalizada `RI_UsageModelDemo=true` en el momento del empaquetado. Si va a empaquetar contenido con la herramienta de línea de comandos de Media Packager, especifique:

```
    java -jar AdobeMediaPackager.jar source.flv dest.flv -k RI_UsageModelDemo=true
```

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>Si no activa el modo de demostración opcional en el momento del empaquetado, el servidor de licencias utiliza la directiva especificada en el momento del empaquetado para emitir una licencia. Si se han especificado varias directivas, el servidor de licencias utiliza la primera directiva válida.

En la demostración, la lógica empresarial del servidor controla los atributos reales de las licencias generadas. En el momento del empaquetado, solo se debe incluir en el contenido una información mínima sobre las políticas. Específicamente, la política solo necesita indicar si se requiere autenticación para acceder al contenido. Para habilitar los cuatro modelos de uso, incluya una directiva que permita el acceso anónimo (para el modelo financiado con publicidad) y una directiva que requiera autenticación de nombre de usuario/contraseña (para los otros 3 modelos de uso). Al solicitar una licencia, una aplicación cliente puede determinar si se solicita al usuario la autenticación en función de la información de autenticación de las directivas.

Para controlar el modelo de uso en el que se emitirá una licencia a un usuario determinado, se pueden agregar entradas a la base de datos de implementación de referencia. La `Customer` tabla contiene nombres de usuario y contraseñas para autenticar usuarios. También indica si el usuario tiene una suscripción. A los usuarios con suscripciones se les otorgarán licencias bajo el modelo de uso de *suscripción* . Para conceder acceso a un usuario en los modelos de uso de *Descargar a su propiedad* o *Vídeo a petición* , se puede agregar una entrada a la `CustomerAuthorization` tabla, que especifica cada parte del contenido al que se permite acceder el usuario y el modelo de uso. Consulte la [!DNL PopulateSampleDB.sql] secuencia de comandos para obtener más información sobre cómo rellenar cada tabla.

Cuando un usuario solicita una licencia, el servidor de implementación de referencia comprueba los metadatos enviados por el cliente para determinar si el contenido se empaquetó con la `RI_UsageModelDemo` propiedad . Si es así, se utilizan las siguientes reglas comerciales:

* Si una de las directivas requiere autenticación:

   * Si la solicitud contiene un token de autenticación válido, busque al usuario en la tabla Base de datos de clientes. Si se encontró al usuario:

      * Si la `Customer.IsSubscriber` propiedad es `true`, genere una licencia para el modelo de uso de *suscripción* y envíela al usuario.

      * Busque un registro en la tabla de la `CustomerAuthorization` base de datos para este usuario y el ID de contenido. Si se encontró un registro:

         * Si `CustomerAuthorization.UsageType` es así, `DTO`genere una licencia para el modelo de uso de *Descargar a su propiedad* y envíela al usuario.

         * Si `CustomerAuthorization.UsageType` es así, `VOD`genere una licencia para el modelo de uso de *Video On Demand* y envíela al usuario.
   * Si ninguna de las políticas permite el acceso anónimo:

      * Si no hay un token de autenticación válido en la solicitud, devuelva un error de &quot;autenticación requerida&quot;.
      * De lo contrario, devuelve un error &quot;no autorizado&quot;.


* Si una de las políticas permite el acceso anónimo, genere una licencia para el modelo de uso financiado con publicidad y envíela al usuario.

Antes de que el servidor de implementación de referencia pueda emitir licencias para la demostración del modelo de uso, el servidor debe configurarse para especificar cómo se generan las licencias para cada uno de los cuatro modelos de uso. Esto se realiza especificando una directiva para cada modelo de uso. La implementación de referencia incluye cuatro directivas de muestra ( [!DNL dto-policy.pol], [!DNL vod-policy.pol], [!DNL sub-policy.pol], [!DNL ad-policy.pol]) o puede sustituir sus propias políticas. En [!DNL flashaccess-refimpl.properties], defina las siguientes propiedades para especificar la directiva que se va a utilizar en cada modelo de uso y coloque los archivos de política en el directorio especificado por la `config.resourcesDirectory` propiedad:

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

