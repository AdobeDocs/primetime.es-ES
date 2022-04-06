---
title: Account IQ introducción a la cuenta IQ, requisitos previos e integración
description: 'Incorporación, requisitos previos e introducción a Account IQ. '
source-git-commit: 258ce10297aa15086a3ed1c1a825af2a30d34d24
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---


# Introducción a Account IQ {#onboarding}

Continúe leyendo para conocer los requisitos previos para utilizar Account IQ y cómo puede su empresa participar para comenzar a observar las puntuaciones de uso compartido de cuentas de los suscriptores.

## Requisitos previos {#prerequisites}

* La organización debe estar registrada en [!DNL Adobe Marketing Cloud] organizaciones.

* Los usuarios de esa organización deben asignarse a TVE Dashboard Read-Write o TVE Dashboard Read-Only.

### Requisitos previos del explorador {#browser-prerequisites}

Account IQ es un servicio web alojado. Es compatible con la versión más reciente de los siguientes navegadores:

* Google Chrome
* Mozilla Firefox
* Versión de Safari

### ¿Cómo incorporar organizaciones en Account IQ? {#steps-to-onboard}


Esto es lo que tenemos en este momento. El plan es deshacerse de la comprobación dma_primetime y tener un perfil dedicado para AIQ. Los usuarios que necesitan tener acceso a la consola necesitarían ese perfil de usuario. Sin embargo, esto no se aplica en este momento.

1. Si su organización se incorpora en Adobe Marketing Cloud @Eric o @Peter, ¿pueden tomar esto?  Creo que ahora se llama &quot;Experience Cloud&quot;, pero eso es menor.  ¿Hay más detalles sobre esto? ¿Está gestionado por otro grupo? En caso afirmativo, ¿proporcionamos un vínculo, un contacto, etc.? Esto también debería contener una advertencia sobre la comprobación de si su organización ya es parte de un Experience Cloud.

2. Tener perfiles de &quot;lectura y escritura del panel de control de Televisión&quot; o &quot;solo lectura del panel de control de Televisión&quot; asignados a sus usuarios en http://adminconsole.adobe.com/.
@Eric, ¿sabes hacer esto?  ¿Hay subpasos?  ¿Podemos explicar a los clientes por qué eligieron la función de lectura y escritura o la de solo lectura?
@Cristina, ¿puedes dar una breve explicación de que este es un enfoque temporal y tal vez cómo funcionará en la próxima versión?

3. Con su id de organización en la lista blanca del lado AIQ @Cristina, ¿hay un proceso que podamos poner en marcha para manejar esto?  Por ejemplo, envíe un correo electrónico a &quot;DL-AdobePass-Eng AdobePass-Eng@adobe.com&quot; con el identificador de organización de la organización, etc.

<!-- these user groups set dma_primetime product context for the user accounts. In AIQ code we’re checking for this product context when providing access. Internally, in the code we have an additional condition: the org id should be whitelisted in order for the users to get access to their data. -->

Al acceder al panel de Adobe de Enterprise, verá los dos grupos de usuarios recién creados en su organización de Adobe Marketing Cloud:

Lectura-escritura del panel de control de Televisión: los miembros de este grupo tienen derechos completos en todas las secciones editables del tablero TVE de solo lectura: los miembros de este grupo solo tienen derechos de visualización en todo el tablero. Agregue su cuenta al grupo de usuarios Lectura-escritura del tablero de TVE, en el tablero de Enterprise de Adobe y, a continuación, inicie sesión en el tablero TVE de Adobe Primetime.  Después, podrá administrar los permisos de usuario en Adobe Enterprise Dashboard agregando y eliminando usuarios de los dos grupos de usuarios enumerados anteriormente.

............

En la documentación que ha proporcionado hay una parte llamada &quot;Introducción al aprovisionamiento de usuarios del panel de control de Televisión de Primetime&quot; que se aplica a la consola de Adobe Pass, pero también debería ser similar para AIQ.
http://tve.helpdocsonline.com/primetime-tve-dashboard-user-guide La organización que está interesada en AIQ debe ser una organización registrada en Adobe Marketing Cloud Orgs. Los usuarios de esa organización deben asignarse a TVE Dashboard Read-Write o TVE Dashboard Read-Only.
Solo para su conocimiento, estos grupos de usuarios establecen el contexto del producto dma_primetime para las cuentas de usuario. En el código AIQ estamos comprobando este contexto de producto al proporcionar acceso. Internamente, en el código tenemos una condición adicional: el id de organización debe incluirse en la lista blanca para que los usuarios puedan acceder a sus datos.
Esto es lo que tenemos en este momento. El plan es deshacerse de la comprobación dma_primetime y tener un perfil dedicado para AIQ. Los usuarios que necesitan tener acceso a la consola necesitarían ese perfil de usuario. Sin embargo, esto no se aplica en este momento.

...........................

1. Incorporación de su organización en Adobe Marketing Cloud
2. Tener perfiles de &quot;lectura y escritura del panel de control de Televisión&quot; o &quot;solo lectura del panel de control de Televisión&quot; asignados a sus usuarios en http://adminconsole.adobe.com/.
3. Tener su id de organización en la lista blanca del lado de AIQ
