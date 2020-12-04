---
seo-title: Garantizar la compatibilidad con Flash Media Rights Management Server 1.x
title: Garantizar la compatibilidad con Flash Media Rights Management Server 1.x
uuid: 0160ca02-ebe6-4090-bf32-1d1a46088844
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Garantizar la compatibilidad con Flash Media Rights Management Server 1.x{#ensure-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management Server 1.x y Adobe Access utilizan distintos metadatos para empaquetar contenido y solicitar licencias. Para que Adobe Access utilice contenido de la versión 1.x de FMRMS, los metadatos deben convertirse.

El SDK de Adobe Access admite dos opciones para convertir metadatos:

* Sin conexión (recomendado)

   Genere los metadatos de Adobe Access en un proceso sin conexión y guárdelos para utilizarlos cuando un cliente los solicite. Adobe recomienda esta opción. Si los metadatos se generan sin conexión, el servidor de licencias no necesita acceder a los CEK 1.x ni a las credenciales del empaquetador. Además, la conversión de ofertas sin conexión mejora el rendimiento porque el servidor de licencias no necesita generar los metadatos en tiempo real.

* Bajo demanda

   Genere los metadatos de Adobe Access a petición cuando un cliente los solicite. Cuando un cliente de Adobe Access descarga contenido de la versión 1.x, envía los metadatos DRM (también conocidos como el encabezado DRM) al SDK de Adobe Access. El SDK convierte los metadatos DRM al formato actual. El SDK cifra e incrusta la clave de codificación de contenido (CEK) en los metadatos y devuelve el contenido al cliente de Adobe Access. (Los metadatos de Adobe Access 1.x no contienen el CEK).

   Para convertir los metadatos, Adobe Access requiere acceso a las claves de codificación de contenido de Adobe Access 1.x. Cuando migre desde Flash Media Rights Management Server 1.x, puede seguir almacenando las claves de codificación de contenido en la base de datos de LiveCycle ES o puede implementar una solución personalizada para almacenar de forma segura las claves de cifrado de contenido en otros sitios. Si decide continuar almacenando las claves de cifrado de contenido en la base de datos ES de LiveCycle, siga las recomendaciones que se describen en &quot;Protección del acceso a contenido confidencial en la base de datos&quot; en *Endurecimiento y seguridad para LiveCycle ES*.

Para obtener más información sobre cómo garantizar la compatibilidad con contenido empaquetado mediante Flash Media Rights Management Server 1.x, consulte la *Referencia de API de acceso a Adobe*.
