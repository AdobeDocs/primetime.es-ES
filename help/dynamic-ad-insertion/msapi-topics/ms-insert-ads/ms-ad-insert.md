---
description: Todas las solicitudes de inserción de publicidad utilizan la misma estructura URL y los mismos parámetros de consulta básicos. Los parámetros de consulta adicionales permiten que el servidor de manifiesto funcione con una variedad de clientes y situaciones.
seo-description: Todas las solicitudes de inserción de publicidad utilizan la misma estructura URL y los mismos parámetros de consulta básicos. Los parámetros de consulta adicionales permiten que el servidor de manifiesto funcione con una variedad de clientes y situaciones.
seo-title: Solicitudes de inserción de anuncios
title: Solicitudes de inserción de anuncios
uuid: e42b3228-bff7-4202-86ed-7f631f3016ae
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# Solicitudes de inserción de anuncios {#requests-for-ad-insertion}

Todas las solicitudes de inserción de publicidad utilizan la misma estructura URL y los mismos parámetros de consulta básicos. Los parámetros de consulta adicionales permiten que el servidor de manifiesto funcione con una variedad de clientes y situaciones.

| Parámetro | Descripción |
|--- |--- |
| u | El ID de recurso es un hash MD5 de ad_request_id de los metadatos de toma de decisiones de anuncios de Adobe Primetime. Proporcionado por el administrador de cuentas técnico de Adobe. |
| z | Id. de zona del recurso que debe proporcionarse a Auditude. Proporcionado por el administrador de cuentas técnico de Adobe. |
| `__sid__` | ID única que usará el servidor de manifiesto para generar la identificación de sesión. |

>[!NOTE]
>
>El `__sid__` parámetro está rodeado por caracteres de subrayado doble.

El servidor de manifiesto mantiene sesiones para clientes individuales o grupos de clientes para garantizar que las secuencias de interacciones de API para distintos clientes se mantengan separadas. El `__sid__` que el cliente envía en la URL de arranque al servidor de manifiesto debe ser único dentro de su entorno. El servidor de manifiesto lo utiliza para construir un ID único global, que devuelve al cliente.

Los parámetros de consulta restantes corresponden a diferentes clientes y situaciones.