---
description: Todas las solicitudes de inserción de publicidad utilizan la misma estructura de URL y los mismos parámetros de consulta básicos. Los parámetros de consulta adicionales permiten que el servidor de manifiesto funcione con una variedad de clientes y situaciones.
title: Solicitudes de inserción de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Solicitudes de inserción de publicidad {#requests-for-ad-insertion}

Todas las solicitudes de inserción de publicidad utilizan la misma estructura de URL y los mismos parámetros de consulta básicos. Los parámetros de consulta adicionales permiten que el servidor de manifiesto funcione con una variedad de clientes y situaciones.

| Parámetro | Descripción |
|--- |--- |
| u | El ID de recurso es un hash MD5 del ad_request_id de los metadatos de Adobe Primetime ad decisioning. Proporcionado por el administrador técnico de cuentas de Adobe. |
| z | El id de zona del recurso que debe proporcionarse a Auditude. Proporcionado por el administrador técnico de cuentas de Adobe. |
| `__sid__` | ID exclusivo que utilizará el servidor de manifiesto para generar el ID de sesión. |

>[!NOTE]
>
>El parámetro `__sid__` está rodeado de caracteres de subrayado dobles.

El servidor de manifiesto mantiene sesiones para clientes individuales o grupos de clientes para garantizar que las secuencias de interacciones de API para distintos clientes se mantengan separadas. El `__sid__` que el cliente envía en la URL de arranque al servidor de manifiesto debe ser único dentro de su entorno. El servidor de manifiesto lo utiliza para construir un ID único global, que devuelve al cliente.

Los parámetros de consulta restantes pertenecen a diferentes clientes y situaciones.