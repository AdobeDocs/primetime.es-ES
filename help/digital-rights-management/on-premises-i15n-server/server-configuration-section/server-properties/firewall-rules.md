---
title: Reglas de firewall
description: Reglas de firewall
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# Reglas de firewall{#firewall-rules}

Para asegurar el acceso al servidor de Individualización, solo es necesario exponer ciertas rutas de aplicación. El servidor de Individualización debe aceptar solicitudes de clientes a estas rutas:

* [!DNL /flashaccess/i15n/*]
* [!DNL /flashaccess/status]
* [!DNL /crossdomain.xml]

Las rutas de servicio, como [!DNL /flashaccess/admin/*] (es decir, las páginas de estado y administración) solo deben ser accesibles desde dentro del firewall. No se debe acceder a ninguna parte del servidor de generación de claves desde fuera del firewall.
