---
description: Puede utilizar la autenticación de Adobe Primetime para administrar los derechos de usuario en el reproductor.
title: Información general
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# Información general {#overview}

Puede utilizar la autenticación de Adobe Primetime para administrar los derechos de usuario en el reproductor.

El administrador de funciones que encapsula los flujos de derechos de autenticación de Primetime es el `EntitlementManager`. Esta clase encapsula la lógica de asignación de derechos al delegar el trabajo de interfaz de usuario a otra parte.

Esta implementación de referencia para Android utiliza la biblioteca AccessEnabler de autenticación de Primetime versión 1.7.3. Gran parte de la implementación es muy similar a la aplicación de demostración existente proporcionada con la biblioteca AccessEnabler.

Para obtener información adicional sobre la autenticación de Primetime, consulte la documentación en [Introducción a la integración de programadores](https://tve.helpdocsonline.com/introduction-to-programmer-integration).
