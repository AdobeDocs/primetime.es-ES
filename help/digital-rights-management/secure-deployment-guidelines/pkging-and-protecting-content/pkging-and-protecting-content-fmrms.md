---
description: Flash Media Rights Management Server 1.x y Adobe Primetime DRM usan diferentes metadatos para empaquetar contenido y solicitar licencias. Para que Primetime DRM utilice contenido de la versión 1.x de FMRMS, los metadatos deben convertirse.
title: Garantizar la compatibilidad con Flash Media Rights Management Server 1.x
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# Garantizar la compatibilidad con Flash Media Rights Management Server 1.x {#ensuring-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management Server 1.x y Adobe Primetime DRM usan diferentes metadatos para empaquetar contenido y solicitar licencias. Para que Primetime DRM utilice contenido de la versión 1.x de FMRMS, los metadatos deben convertirse.

El SDK de Primetime DRM admite las siguientes opciones para la conversión de metadatos:

* Sin conexión (recomendado)

   Genere los metadatos de DRM de Primetime en un proceso sin conexión y almacene los metadatos hasta que los solicite un cliente. Si los metadatos se generan sin conexión, el servidor de licencias no necesita acceder a los CEK 1.x ni a las credenciales del empaquetador. La conversión sin conexión ofrece un mejor rendimiento porque el servidor de licencias no necesita generar los metadatos en tiempo real.
* Bajo demanda

   Los metadatos de DRM de Primetime se generan cuando un cliente solicita los metadatos. Cuando un cliente de DRM de Primetime descarga contenido de la versión 1.x, el cliente envía los metadatos de DRM al SDK de DRM de Primetime. El SDK convierte los metadatos de DRM al formato actual, cifra e incrusta la clave de cifrado de contenido (CEK) en los metadatos y envía el contenido de nuevo al cliente de DRM de Primetime.

   >[!NOTE]
   >
   >Los metadatos de Primetime DRM 1.x no incluyen el CEK.

   Para convertir los metadatos, el DRM de Primetime requiere acceso a las claves de cifrado de contenido de Primetime DRM 1.x. Cuando migre desde Flash Media Rights Management Server 1.x, puede seguir almacenando las claves de cifrado de contenido en la base de datos de LiveCycle ES o implementar una solución personalizada para almacenar de forma segura las claves de cifrado de contenido en otra ubicación. Si decide almacenar las claves de cifrado de contenido en la base de datos de LiveCycle ES, siga las recomendaciones que se describen en *Protección del acceso al contenido confidencial en la base de datos* en **Endurecimiento y seguridad para LiveCycle® ES2**.

Para obtener más información sobre cómo garantizar la compatibilidad con el contenido empaquetado mediante el uso de Flash Media Rights Management Server 1.x, consulte las API de Adobe Primetime DRM en [Referencias de la API de Adobe Primetime](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).
