---
description: Flash Media Rights Management Server 1.x y Adobe Primetime DRM utilizan distintos metadatos para empaquetar contenido y solicitar licencias. Para que Primetime DRM utilice contenido de la versión 1.x de FMRMS, los metadatos deben convertirse.
seo-description: Flash Media Rights Management Server 1.x y Adobe Primetime DRM utilizan distintos metadatos para empaquetar contenido y solicitar licencias. Para que Primetime DRM utilice contenido de la versión 1.x de FMRMS, los metadatos deben convertirse.
seo-title: Garantía de compatibilidad con Flash Media Rights Management Server 1.x
title: Garantía de compatibilidad con Flash Media Rights Management Server 1.x
uuid: dd70941e-9015-4fb0-b265-557b6252e051
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Garantía de compatibilidad con Flash Media Rights Management Server 1.x {#ensuring-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management Server 1.x y Adobe Primetime DRM utilizan distintos metadatos para empaquetar contenido y solicitar licencias. Para que Primetime DRM utilice contenido de la versión 1.x de FMRMS, los metadatos deben convertirse.

El SDK de DRM de Primetime admite las siguientes opciones para la conversión de metadatos:

* Sin conexión (recomendado)

   Genere los metadatos de DRM de Primetime en un proceso sin conexión y almacene los metadatos hasta que los solicite un cliente. Si los metadatos se generan sin conexión, el servidor de licencias no necesita acceder a los CEK 1.x ni a las credenciales del empaquetador. La conversión sin conexión ofrece un mejor rendimiento porque el servidor de licencias no necesita generar los metadatos en tiempo real.
* Bajo demanda

   Los metadatos de DRM de Primetime se generan cuando un cliente solicita los metadatos. Cuando un cliente DRM de Primetime descarga contenido de la versión 1.x, el cliente envía los metadatos DRM al SDK de DRM de Primetime. El SDK convierte los metadatos DRM al formato actual, codifica e incrusta la clave de codificación de contenido (CEK) en los metadatos y devuelve el contenido al cliente Primetime DRM.

   >[!NOTE]
   >
   >Los metadatos Primetime DRM 1.x no incluyen el CEK.

   Para convertir los metadatos, Primetime DRM requiere acceso a las claves de codificación de contenido de Primetime DRM 1.x. Al migrar desde Flash Media Rights Management Server 1.x, puede seguir almacenando las claves de codificación de contenido en la base de datos de LiveCycle ES o implementar una solución personalizada para almacenar de forma segura las claves de codificación de contenido en otra ubicación. Si decide almacenar las claves de codificación de contenido en la base de datos de LiveCycle ES, siga las recomendaciones que se describen en *Protección del acceso a contenido confidencial en la base de datos* en **Endurecimiento y seguridad para LiveCycle® ES2**.

Para obtener más información sobre cómo garantizar la compatibilidad con el contenido empaquetado mediante Flash Media Rights Management Server 1.x, consulte las API de DRM de Adobe Primetime en las referencias [de API de](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References)Adobe Primetime.
