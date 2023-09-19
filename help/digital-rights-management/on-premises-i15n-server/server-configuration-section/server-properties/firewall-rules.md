---
title: Reglas del cortafuegos
description: Reglas del cortafuegos
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# Reglas del cortafuegos{#firewall-rules}

Para proteger el acceso al servidor de individualización, solo es necesario exponer determinadas rutas de aplicación. El servidor de individualización debe aceptar solicitudes de clientes a estas rutas:

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

Rutas de servicio, como [!DNL /flashaccess/admin/*] (es decir, las páginas de estado y administración) solo deben ser accesibles desde el cortafuegos. No se debe acceder a ninguna parte del servidor de generación de claves desde fuera del cortafuegos.
