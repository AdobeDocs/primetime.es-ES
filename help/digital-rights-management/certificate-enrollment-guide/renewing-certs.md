---
seo-title: Renovar certificados
title: Renovar certificados
uuid: 12a560b0-966b-424e-bfe5-22e9c10d8667
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5

---


# Renovar certificados{#renew-certificates}

Tenga en cuenta las siguientes restricciones de renovación de certificados basadas en la configuración del SDK de Adobe Primetime DRM:

* SDK de producción de DRM Primetime

   Adobe proporciona el conjunto inicial de certificados gratuitos para el SDK de producción de DRM Primetime cuando compra un contrato de asistencia. Si no tiene un contrato de soporte, puede comprar un conjunto de certificados de renovación válidos durante dos años.
* SDK de evaluación de DRM de Primetime

   El certificado establecido para este SDK es válido durante un año y no se puede renovar.
* SDK de prueba de DRM de Primetime

   El SDK de prueba de DRM de Primetime es válido durante tres meses y Adobe proporciona un conjunto de certificados de renovación gratuitos.

## Implementación de nuevos certificados y uso de certificados antiguos para contenido existente {#section_345C92D1C9794B0BBB9A9B0702EC95FF}

En Primetime DRM, puede permitir que un servidor de licencias emita una licencia para contenido empaquetado con certificados de empaquetador anteriores (o incluso caducados). Para configurar el servidor para que acepte solicitudes de licencia de contenido previamente empaquetado, proporcione el certificado antiguo al servidor y actualice el archivo de configuración del servidor para que el servidor sepa dónde encontrar los certificados antiguos. Para obtener más información, consulte *Gestión de actualizaciones de certificados cuando los certificados emitidos por Adobe caducan* en *Uso del SDK de DRM de Adobe Primetime para la protección de contenido*.

Si la aplicación de servidor se basa en la implementación de referencia de DRM de Primetime, no es necesario actualizar el programa de servidor. En el `flashaccess-refimpl.properties` archivo, hay campos en los que puede especificar certificados de servidor de licencias y transporte adicionales. Si solo tiene un certificado, no tiene que rellenar estas propiedades. Si tiene certificados caducados y desea utilizar estos certificados al emitir respuestas de licencia, debe proporcionar estos certificados al archivo de configuración y reiniciar el servidor.

Para especificar certificados antiguos, utilice las siguientes propiedades:

* `#HandlerConfiguration.AdditionalServerTransportCredential.1=transport.pfx`
* `#HandlerConfiguration.AdditionalServerTransportCredential.1.password=[password]`
* `#AsymmetricKeyRetrieval.ServerCredential.1=license_server.pfx`
* `#AsymmetricKeyRetrieval.ServerCredential.1.password=[password]`

