---
title: Garantizar la compatibilidad con Flash Media Rights Management Server 1.x
description: Garantizar la compatibilidad con Flash Media Rights Management Server 1.x
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Asegúrese de la compatibilidad con Flash Media Rights Management Server 1.x{#ensure-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management Server 1.x y Adobe Access usan diferentes metadatos para empaquetar contenido y solicitar licencias. Para que Adobe Access utilice contenido de la versión 1.x de FMRMS, los metadatos deben convertirse.

El SDK de acceso a Adobe admite dos opciones para convertir metadatos:

* Sin conexión (recomendado)

   Genere los metadatos de acceso a Adobe en un proceso sin conexión y guárdelos para utilizarlos cuando un cliente lo solicite. Adobe recomienda esta opción. Si los metadatos se generan sin conexión, el servidor de licencias no necesita acceder a los CEK 1.x ni a las credenciales del empaquetador. Además, la conversión sin conexión ofrece un mejor rendimiento, ya que el servidor de licencias no necesita generar los metadatos en tiempo real.

* Bajo demanda

   Genere los metadatos de acceso a Adobe bajo demanda cuando un cliente los solicite. Cuando un cliente de acceso a Adobe descarga contenido de la versión 1.x, envía los metadatos DRM (también conocidos como el encabezado DRM) al SDK de acceso a Adobe. El SDK convierte los metadatos DRM al formato actual. El SDK cifra e incrusta la clave de cifrado de contenido (CEK) en los metadatos y envía el contenido de nuevo al cliente de acceso a Adobe. (Los metadatos de acceso a Adobe 1.x no contienen el CEK).

   Para convertir los metadatos, Adobe Access requiere acceso a las claves de cifrado de contenido de Adobe Access 1.x. Cuando migre desde Flash Media Rights Management Server 1.x, puede seguir almacenando las claves de cifrado de contenido en la base de datos de LiveCycle ES o puede implementar una solución personalizada para almacenar de forma segura las claves de cifrado de contenido en otra parte. Si decide seguir almacenando las claves de cifrado de contenido en la base de datos de LiveCycle ES, siga las recomendaciones que se describen en &quot;Protección del acceso al contenido confidencial de la base de datos&quot; en *Endurecimiento y seguridad del LiveCycle ES*.

Para obtener más información sobre cómo garantizar la compatibilidad con contenido empaquetado mediante Flash Media Rights Management Server 1.x, consulte la *Referencia de API de acceso a Adobe*.
