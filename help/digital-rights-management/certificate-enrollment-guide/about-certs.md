---
seo-title: Acerca de los certificados
title: Acerca de los certificados
uuid: 0b7818b4-bd6a-4f2e-94c2-565e0d735bf8
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Acerca de los certificados {#about-certificates}

El SDK de Adobe Primetime DRM está disponible en las siguientes configuraciones:

* SDK de producción de DRM Primetime
* SDK de evaluación de DRM de Primetime
* SDK de prueba de DRM de Primetime

Para utilizar el SDK de DRM de Primetime para crear un servidor de licencias, debe obtener certificados digitales de Adobe. Los certificados digitales (también denominados simplemente certificados) enlazan una entidad, como un individuo, una organización o un sistema, a un par de claves públicas y privadas específico. Los certificados digitales pueden considerarse credenciales electrónicas que verifican la identidad de un individuo, sistema u organización.

Para permitir la máxima flexibilidad y una seguridad mejorada en las opciones de implementación, el SDK de DRM Primetime requiere cuatro certificados:

* Certificado de servidor de licencias

   El SDK utiliza este certificado para firmar las licencias de contenido emitidas a los clientes.
* Certificado de Packager

   El SDK utiliza este certificado para generar metadatos DRM al empaquetar (codificar) contenido.
* Certificado de transporte

   El SDK utiliza este certificado para asegurar la comunicación entre los clientes y el servidor de licencias.
* Certificado de CA de dominio

   Los clientes que deseen implementar un servidor de dominio necesitan el certificado de CA de dominio. A diferencia de los demás certificados, el certificado de CA de dominio no se emite por Adobe.

>[!NOTE]
>
>Para el SDK de evaluación y el SDK de prueba, los certificados Servidor de licencias, Packager y Transporte se combinan en un único certificado.

