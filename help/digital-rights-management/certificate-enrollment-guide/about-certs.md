---
title: Acerca de los certificados
description: Acerca de los certificados
copied-description: true
exl-id: 24ca19bb-a71e-461a-9c3c-558d650e2d99
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Acerca de los certificados {#about-certificates}

El SDK de DRM de Adobe Primetime está disponible en las siguientes configuraciones:

* SDK de producción de DRM de Primetime
* SDK de evaluación DRM de Primetime
* SDK de prueba de Primetime DRM

Para utilizar el SDK de DRM de Primetime para crear un servidor de licencias, debe obtener certificados digitales de Adobe. Los certificados digitales (también denominados simplemente certificados) vinculan una entidad, como un individuo, organización o sistema, a un par de claves pública y privada específico. Los certificados digitales se pueden considerar como credenciales electrónicas que verifican la identidad de un individuo, sistema u organización.

Para permitir la máxima flexibilidad y seguridad mejorada en las opciones de implementación, el SDK de DRM de Primetime requiere cuatro certificados:

* Certificado del servidor de licencias

   El SDK utiliza este certificado para firmar las licencias de contenido emitidas a los clientes.
* Certificado de empaquetador

   El SDK utiliza este certificado para generar metadatos DRM al empaquetar contenido (cifrado).
* Certificado de transporte

   El SDK utiliza este certificado para proteger la comunicación entre los clientes y el servidor de licencias.
* Certificado de CA de dominio

   Los clientes que desean implementar un servidor de dominio necesitan el certificado de CA de dominio. A diferencia de otros certificados, el certificado de CA de dominio no se emite por Adobe.

>[!NOTE]
>
>Para el SDK de evaluación y el SDK de prueba, los certificados del servidor de licencias, el empaquetador y el transporte se combinan en un único certificado.
