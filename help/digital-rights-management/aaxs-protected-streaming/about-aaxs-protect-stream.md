---
title: Acerca de Adobe Access Server para Flujo Protegido
description: Acerca de Adobe Access Server para Flujo Protegido
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Acerca de Adobe Access Server para Flujo Protegido{#about-adobe-access-server-for-protected-streaming}

Adobe ® Access™ Server for Protected Streaming es una implementación de servidor de licencias basada en el SDK de acceso a Adobe. Este servidor emite licencias para contenido protegido para clientes de acceso a Adobe.

Adobe Access Server para flujo protegido admite varios inquilinos, lo que significa que un solo servidor se puede alojar en nombre de varios editores de contenido, cada uno con su propia configuración. Además, el servidor admite componentes de autorización personalizados, por lo que la lógica personalizada se puede ejecutar antes de emitir una licencia.

Este servidor está diseñado para utilizarse con flujo HTTP. Como resultado, esta implementación del servidor no admite todas las funcionalidades disponibles en Acceso al Adobe. Por ejemplo, Adobe Access Server para Flujo protegido no admite solicitudes de autenticación de usuario, varias directivas, licencias enlazadas a dominio, encadenamiento de licencias o mensajes de sincronización.
