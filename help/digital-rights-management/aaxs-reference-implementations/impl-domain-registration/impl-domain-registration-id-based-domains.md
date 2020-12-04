---
seo-title: Dominios basados en identidad
title: Dominios basados en identidad
uuid: 34cad19b-1adb-4e0c-ac59-50632f6988f7
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---


# Dominios basados en identidad {#identity-based-domains}

En este caso de uso, cada usuario autenticado tiene su propio dominio y se permite que un determinado número de dispositivos se unan al dominio. Para utilizar este tipo de dominio con la implementación de referencia, cree una directiva que especifique el registro de dominio que se requiere. Especifique el host y el puerto del servidor para la URL del servidor de dominio y especifique que se requiere autenticación de nombre de usuario y contraseña.

La implementación de referencia implementa la siguiente lógica para el registro de dominios:

1. Determine el nombre de dominio que se va a asignar a este usuario. El nombre de dominio se extraerá * `namequalifier:username`* del token de autenticación. Si no hay ningún token de autenticación, devuelva el error DOM_AUTHENTICATION_REQUIRED (503).
1. Busque el nombre de dominio en la tabla `DomainServerInfo`. Si no se encuentra una entrada, inserte una entrada en la tabla (los valores predeterminados son autenticación obligatoria, la pertenencia máxima al dominio=5).
1. Compruebe si el dispositivo ya se ha registrado en el dominio:

   1. Busque el nombre de dominio en la tabla `UserDomainMembership`. Para cada ID de equipo encontrado, compare con el ID de equipo de la solicitud. Si se trata de una máquina nueva, agregue una entrada a la tabla `UserDomainMembership`. A continuación, busque los registros coincidentes en la tabla `UserDomainRefCount`. Si no existe una entrada para este GUID de equipo, agregue un registro.

   1. Si se trata de un dispositivo nuevo y ya se ha alcanzado la pertenencia máxima, se mostrará el error DOM_LIMIT_REACHED (502).

1. Busque todas las claves de dominio de este dominio en la tabla DomainKeys.

   1. Si `DomainServerInfo` indica que es necesario pasar el ratón por encima de las claves, genere un nuevo par de claves, guárdelo en la tabla `DomainKeys` (con la versión clave uno más alta que la clave existente más alta) y restablezca el indicador &quot;Se requiere rollover clave&quot; en `DomainServerInfo`.

   1. Para cada clave de dominio, genere una credencial de dominio.

La implementación de referencia implementa la siguiente lógica para la anulación del registro de dominios:

1. Determine el nombre de dominio que se va a asignar a este usuario. El nombre de dominio será *nombrecalificador:nombre de usuario* extraído del autentificador de autenticación. Si no hay ningún token de autenticación, devuelva el error DOM_AUTHENTICATION_REQUIRED (503).
1. Busque el nombre de dominio solicitado en la tabla `DomainServerInfo`.
1. Busque el nombre de dominio en la tabla `UserDomainMembership`. Para cada ID de equipo encontrado, compare con el ID de equipo de la solicitud. Busque la entrada correspondiente en la tabla `UserDomainRefCount`. Si no se encuentra una entrada coincidente, se devuelve el error DEREG_DENIED (401).

1. Si no se trata de una solicitud de previsualización, elimine la entrada de la tabla `UserDomainRefCount`. Si no hay más entradas en esa tabla para el equipo, elimine la entrada de `UserDomainMembership` y defina el indicador &quot;Se requiere rollover clave&quot; en `DomainServerInfo`.

En este caso de uso, se permite a cada usuario registrar un pequeño número de máquinas, por lo que podemos utilizar el identificador completo del equipo y el método `matches()` para contar con precisión las máquinas. Sin embargo, dado que el usuario puede registrarse varias veces en este equipo (a través de varias aplicaciones de AIR o reproductores en diferentes navegadores), el servidor también necesita mantener un recuento de referencia, de modo que la anulación del registro se pueda contar con precisión. La anulación del registro no puede considerarse completa hasta que se entreguen todos los tokens de dominio del equipo.
