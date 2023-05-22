---
description: Todas las solicitudes de inserción de publicidad utilizan la misma estructura de URL y los mismos parámetros de consulta básicos. Los parámetros de consulta adicionales permiten que el servidor de manifiesto funcione con una variedad de clientes y situaciones.
title: Solicitudes de inserción de publicidad
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Solicitudes de inserción de publicidad {#requests-for-ad-insertion}

Todas las solicitudes de inserción de publicidad utilizan la misma estructura de URL y los mismos parámetros de consulta básicos. Los parámetros de consulta adicionales permiten que el servidor de manifiesto funcione con una variedad de clientes y situaciones.

| Parámetro | Descripción |
|--- |--- |
| u | El ID del recurso es un hash MD5 de ad_request_id de los metadatos de Adobe Primetime ad decisioning. Proporcionado por el administrador técnico de cuentas de Adobe. |
| z | ID de zona del recurso que debe proporcionarse a Auditude. Proporcionado por el administrador técnico de cuentas de Adobe. |
| `__sid__` | ID único que el servidor de manifiesto utilizará para generar el ID de sesión. |

>[!NOTE]
>
>El `__sid__` El parámetro está rodeado de caracteres de subrayado doble.

El servidor de manifiestos mantiene sesiones para clientes individuales o grupos de clientes para garantizar que las secuencias de interacciones de API para diferentes clientes permanezcan separadas. El `__sid__` que el cliente envía en la URL de bootstrap al servidor de manifiesto debe ser único dentro de su entorno. El servidor de manifiestos lo utiliza para construir un ID único global, que devuelve al cliente.

El resto de los parámetros de consulta pertenecen a distintos clientes y situaciones.