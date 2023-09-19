---
title: Reglas de uso
description: Reglas de uso
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# Reglas de uso {#usage-rules}

En los temas siguientes se describen las reglas de uso que se pueden especificar en una directiva DRM de Adobe Primetime.

## Autenticación de usuario {#user-authentication}

La autenticación del usuario especifica si se requiere una credencial, como un nombre de usuario y una contraseña, para adquirir una licencia. Si se especifican licencias autenticadas (basadas en identidad), el servidor ~~_autentica_~~ al usuario antes de emitir una licencia.

Ejemplo de caso de uso: Un servicio de suscripción puede requerir que se introduzca un nombre de usuario y una contraseña antes de emitir una licencia de contenido. Un disco DVD o Blu-ray con copia digital puede proporcionar un código u otro token como prueba de pago, que se puede canjear por una descarga electrónica.
