---
title: Acerca de las implementaciones de referencia
description: Acerca de las implementaciones de referencia
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---


# Acerca de las implementaciones de referencia{#about-the-reference-implementations}

Esta guía describe la instalación, configuración y operación de las implementaciones de referencia de Adobe Primetime DRM.

>[!NOTE]
>
>Primetime DRM se llamaba anteriormente Acceso al Adobe, y antes de eso, Flash Access.

Las implementaciones de referencia de DRM de Primetime incluyen estos componentes:

* **Herramientas de la línea de comandos** : Estas herramientas se basan en el mismo código SDK de DRM de Primetime utilizado en el servidor de licencias de DRM de Primetime. Puede realizar empaquetamientos, licencias y otras tareas de DRM desde la línea de comandos, y alternar sin problemas entre el uso de las herramientas de la línea de comandos y el servidor de licencias.
* **Servidor de licencias** : un servidor de licencias totalmente funcional y personalizable (descrito a continuación como una de las opciones de su servidor de licencias).

**Opciones del servidor de licencias:**

* **Implementaciones de referencia de DRM de Primetime** : El asunto de esta guía, esta implementación de referencia presenta un servidor de licencias DRM robusto que muestra todas las funciones proporcionadas por el SDK de DRM de Primetime. Esta implementación se entrega con código fuente e instrucciones para crear el código. Esta implementación no está pensada para utilizarse tal cual (aunque se incluye un archivo [!DNL .war] que puede implementar rápidamente). Se ha diseñado principalmente como referencia que puede utilizar para crear su propio servidor de licencias personalizado.

   Características del servidor de licencias:

   * Gestiona las solicitudes de autenticación mediante una base de datos para validar el nombre de usuario y la contraseña.
   * Gestiona las solicitudes de licencia y determina el tipo de licencia que se emite cuando se aplica la encadenación de licencias.
   * Emite licencias para contenido que incluye varias directivas de DRM de Primetime.
   * Problemas con licencias que admiten el envío de claves remotas a clientes de iOS, que requiere Primetime DRM.
   * Problemas con licencias que requieren una búsqueda externa y recuperación de la clave de cifrado de contenido (CEK).
   * Busca en una base de datos para determinar si un usuario está autorizado a ver contenido.
   * Busca listas de actualización de directivas de DRM de Primetime.
   * Busca listas de revocación del equipo.
   * Utiliza un archivo HSM o PKCS12 para almacenar credenciales.
   * Codifica contraseñas especificadas en un archivo de propiedades.
   * Especifica varias credenciales de transporte o servidor de licencias después de renovar las credenciales.

      Las credenciales antiguas se mantienen en el servidor para que los usuarios puedan seguir viendo el contenido existente sin tener que volver a empaquetar.
   * Restringe las versiones de DRM/Runtime a las que se permite realizar solicitudes a un servidor de licencias.
   * Establece las preferencias de la ventana de reloj del cliente.
   * Restringe la diferencia de tiempo permitida entre el tiempo de solicitud y el tiempo del servidor para evitar ataques de repetición.
   * Gestiona las solicitudes de los clientes de FMRMS 1.x

      Por ejemplo, el cliente FMRMS 1.x se activa para actualizar a Primetime DRM 2.0 o posterior.
   * Convierte los metadatos de FMRMS 1.x en metadatos de Primetime DRM según demanda mediante el uso de información de licencia de FMRMS 1.x almacenada en una base de datos.
   * Convierte las políticas de FMRMS 1.x en políticas de Primetime DRM para el código de muestra.
   * Importa información de licencia de FMRMS 1.x desde una base de datos existente para scripts de ejemplo.
   * Obtiene la versión del servidor
   * Registro de dominios
   * Desregistro de dominios
   * Solicitudes de sincronización
   * Regreso de la licencia

* **Servidor Primetime DRM para transmisión protegida** : es un binario listo para usar que puede implementar rápidamente con el mínimo esfuerzo. Es una buena opción para los clientes que desean mostrar rápidamente la Prueba de Concepto, o *podría* ser una opción de producción si sus necesidades de DRM personalizadas son mínimas. Para obtener más información, consulte Información relacionada a continuación.

* **Servicio de DRM de Primetime Cloud** : es un servidor de licencias alojado en Adobe que puede utilizar para el servicio de licencias. (Debe ser licenciatario de Primetime para utilizar este servicio). Este servicio de nube de Adobe le libera del gasto, el mantenimiento y la ingeniería necesarios para crear su propio servicio. Para obtener más información, consulte Información relacionada a continuación.

