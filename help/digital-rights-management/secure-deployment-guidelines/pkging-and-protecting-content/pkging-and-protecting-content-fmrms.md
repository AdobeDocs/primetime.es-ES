---
description: Flash Media Rights Management Server 1.x y Adobe Primetime DRM utilizan metadatos diferentes para empaquetar contenido y solicitar licencias. Para que Primetime DRM utilice contenido de la versión 1.x de FMRMS, los metadatos deben convertirse.
title: Garantía de compatibilidad con Flash Media Rights Management Server 1.x
exl-id: 737c853f-4e27-47e6-9248-857c7800795a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Garantía de compatibilidad con Flash Media Rights Management Server 1.x {#ensuring-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management Server 1.x y Adobe Primetime DRM utilizan metadatos diferentes para empaquetar contenido y solicitar licencias. Para que Primetime DRM utilice contenido de la versión 1.x de FMRMS, los metadatos deben convertirse.

El SDK de DRM de Primetime admite las siguientes opciones para la conversión de metadatos:

* Sin conexión (recomendado)

   Genere los metadatos DRM de Primetime en un proceso sin conexión y almacénelos hasta que un cliente los solicite. Si los metadatos se generan sin conexión, el servidor de licencias no necesita tener acceso a las CEK 1.x ni a las credenciales del empaquetador. La conversión sin conexión ofrece un mejor rendimiento porque el servidor de licencias no necesita generar los metadatos en tiempo real.
* Bajo demanda

   Los metadatos DRM de Primetime se generan cuando un cliente solicita los metadatos. Cuando un cliente DRM de Primetime descarga contenido de la versión 1.x, el cliente envía los metadatos DRM al SDK de DRM de Primetime. El SDK convierte los metadatos de DRM al formato actual, cifra e incrusta la clave de codificación de contenido (CEK) en los metadatos y devuelve el contenido al cliente de DRM de Primetime.

   >[!NOTE]
   >
   >Los metadatos de Primetime DRM 1.x no incluyen el CEK.

   Para convertir los metadatos, Primetime DRM requiere acceso a las claves de cifrado de contenido de Primetime DRM 1.x. Cuando migre de Flash Media Rights Management Server 1.x, puede seguir almacenando las claves de cifrado de contenido en la base de datos de LiveCycle ES o implementar una solución personalizada para almacenar de forma segura las claves de cifrado de contenido en otra ubicación. Si decide almacenar las claves de cifrado de contenido en la base de datos de LiveCycle ES, siga las recomendaciones que se describen en *Protección del acceso al contenido confidencial en la base de datos* in **Protección y seguridad para LiveCycle® ES2**.

Para obtener más información sobre cómo garantizar la compatibilidad con el contenido empaquetado mediante Flash Media Rights Management Server 1.x, consulte las API de DRM de Adobe Primetime en [Referencias de API de Adobe Primetime](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).
