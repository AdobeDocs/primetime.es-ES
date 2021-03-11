---
title: Acerca de los certificados
description: Acerca de los certificados
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Acerca de los certificados {#about-certificates}

El SDK de Adobe Primetime DRM está disponible en las siguientes configuraciones:

* SDK de producción de DRM de Primetime
* SDK de evaluación de DRM de Primetime
* SDK de prueba de DRM de Primetime

Para utilizar el SDK de DRM de Primetime para crear un servidor de licencias, debe obtener certificados digitales del Adobe. Los certificados digitales (también denominados simplemente certificados) vinculan una entidad, como un individuo, una organización o un sistema, a un par de claves pública y privada específico. Los certificados digitales pueden considerarse como credenciales electrónicas que verifican la identidad de un individuo, sistema u organización.

Para permitir la máxima flexibilidad y una seguridad mejorada en las opciones de implementación, el SDK de Primetime DRM requiere cuatro certificados:

* Certificado de servidor de licencias

   El SDK utiliza este certificado para firmar las licencias de contenido emitidas a los clientes.
* Certificado de paquete

   El SDK utiliza este certificado para generar metadatos DRM al empaquetar (encriptar) contenido.
* Certificado de transporte

   El SDK utiliza este certificado para proteger la comunicación entre los clientes y el servidor de licencias.
* Certificado CA de dominio

   Los clientes que desean implementar un servidor de dominio necesitan el certificado de CA de dominio. A diferencia de los demás certificados, el certificado de CA de dominio no se emite por Adobe.

>[!NOTE]
>
>Para el SDK de evaluación y el SDK de prueba, los certificados de servidor de licencias, paquete y transporte se combinan en un único certificado.

