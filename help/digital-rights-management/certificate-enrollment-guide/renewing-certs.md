---
title: Renovar certificados
description: Renovar certificados
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---


# Renovar certificados{#renew-certificates}

Debe tener en cuenta las siguientes restricciones de renovación de certificados basadas en la configuración del SDK de Adobe Primetime DRM:

* SDK de producción de DRM de Primetime

   Adobe proporciona el conjunto inicial de certificados gratuitos para el SDK de producción de DRM de Primetime al adquirir un contrato de asistencia. Si no tiene un contrato de soporte, puede adquirir un conjunto de certificados de renovación válidos durante dos años.
* SDK de evaluación de DRM de Primetime

   El certificado establecido para este SDK es válido durante un año y no se puede renovar.
* SDK de prueba de DRM de Primetime

   El SDK de prueba de DRM de Primetime es válido durante tres meses y Adobe proporciona un conjunto de certificados de renovación gratuitos.

## Implementar nuevos certificados y usar certificados antiguos para contenido existente {#section_345C92D1C9794B0BBB9A9B0702EC95FF}

En Primetime DRM, puede permitir que un servidor de licencias emita una licencia para el contenido que esté empaquetado con certificados de empaquetador anteriores (o incluso caducados). Para configurar el servidor para que acepte solicitudes de licencia de contenido previamente empaquetado, proporcione el certificado antiguo al servidor y actualice el archivo de configuración del servidor para que el servidor sepa dónde encontrar los certificados antiguos. Para obtener más información, consulte *Gestión de actualizaciones de certificados cuando caducan los certificados emitidos por el Adobe* en *Uso del SDK de DRM de Adobe Primetime para la protección de contenido*.

Si la aplicación del servidor se basa en la implementación de referencia de DRM de Primetime, no es necesario actualizar el programa del lado del servidor. En el archivo `flashaccess-refimpl.properties`, hay campos en los que puede especificar certificados adicionales de Transporte y del Servidor de Licencias. Si solo tiene un certificado, no tiene que rellenar esas propiedades. Si tiene certificados caducados y desea utilizarlos al emitir respuestas de licencia, debe proporcionar estos certificados al archivo de configuración y reiniciar el servidor.

Para especificar certificados antiguos, utilice las siguientes propiedades:

* `#HandlerConfiguration.AdditionalServerTransportCredential.1=transport.pfx`
* `#HandlerConfiguration.AdditionalServerTransportCredential.1.password=[password]`
* `#AsymmetricKeyRetrieval.ServerCredential.1=license_server.pfx`
* `#AsymmetricKeyRetrieval.ServerCredential.1.password=[password]`

