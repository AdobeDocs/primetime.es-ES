---
title: Renovación de certificados
description: Renovación de certificados
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Renovación de certificados{#renew-certificates}

Debe tener en cuenta las siguientes restricciones de renovación de certificados basadas en la configuración del SDK de Adobe Primetime DRM:

* SDK de producción de DRM de Primetime

  Adobe proporciona el conjunto inicial de certificados gratuitos para el SDK de producción de DRM de Primetime al adquirir un contrato de soporte. Si no tiene un contrato de soporte, puede adquirir un conjunto de certificados de renovación válidos durante dos años.
* SDK de evaluación DRM de Primetime

  El conjunto de certificados para este SDK es válido durante un año y no se puede renovar.
* SDK de prueba de Primetime DRM

  El SDK de prueba de Primetime DRM es válido durante tres meses y Adobe proporciona un conjunto de certificados de renovación gratuitos.

## Implementar nuevos certificados y utilizar certificados antiguos para el contenido existente {#section_345C92D1C9794B0BBB9A9B0702EC95FF}

En Primetime DRM, puede permitir que un servidor de licencias emita una licencia para contenido que esté empaquetado con certificados de empaquetador anteriores (o incluso caducados). Para configurar el servidor para que acepte solicitudes de licencia de contenido empaquetado anteriormente, proporcione el certificado antiguo al servidor y actualice el archivo de configuración del servidor para que el servidor sepa dónde encontrar los certificados antiguos. Para obtener más información, consulte *Administrar actualizaciones de certificados cuando caducan los certificados emitidos por el Adobe* in *Uso del SDK de DRM de Adobe Primetime para proteger el contenido*.

Si la aplicación de servidor se basa en la Implementación de referencia de DRM de Primetime, no tiene que actualizar el programa del lado del servidor. En el `flashaccess-refimpl.properties` , hay campos en los que se pueden especificar certificados de transporte y de servidor de licencias adicionales. Si solo tiene un certificado, no tiene que rellenar esas propiedades. Si tiene certificados caducados y desea utilizar estos certificados cuando emita respuestas de licencia, debe proporcionar estos certificados al archivo de configuración y reiniciar el servidor.

Para especificar certificados antiguos, utilice las siguientes propiedades:

* `#HandlerConfiguration.AdditionalServerTransportCredential.1=transport.pfx`
* `#HandlerConfiguration.AdditionalServerTransportCredential.1.password=[password]`
* `#AsymmetricKeyRetrieval.ServerCredential.1=license_server.pfx`
* `#AsymmetricKeyRetrieval.ServerCredential.1.password=[password]`
