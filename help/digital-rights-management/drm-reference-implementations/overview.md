---
title: Acerca de las implementaciones de referencia
description: Acerca de las implementaciones de referencia
copied-description: true
exl-id: fe387330-9449-4977-be15-069c814354bf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# Acerca de las implementaciones de referencia{#about-the-reference-implementations}

Esta guía describe la instalación, configuración y funcionamiento de las implementaciones de referencia de DRM de Adobe Primetime.

>[!NOTE]
>
>Anteriormente, Primetime DRM se denominaba Acceso de Adobe y, antes, Flash Access.

Las implementaciones de referencia de DRM de Primetime incluyen estos componentes:

* **Herramientas de línea de comandos** : estas herramientas se basan en el mismo código SDK de DRM de Primetime utilizado en el servidor de licencias de DRM de Primetime. Puede realizar tareas de empaquetado, licencias y otras tareas de DRM desde la línea de comandos, y alternar sin problemas entre el uso de las herramientas de la línea de comandos y el servidor de licencias.
* **Servidor de licencias** - Un servidor de licencias totalmente funcional y personalizable (descrito a continuación como una de las opciones del servidor de licencias).

**Opciones del servidor de licencias:**

* **Implementaciones de referencia de DRM de Primetime** : Esta guía trata sobre la implementación de referencia con un servidor de licencias DRM robusto que muestra todas las funciones proporcionadas por el SDK de DRM de Primetime. Esta implementación se entrega con el código fuente y las instrucciones para crearlo. Esta implementación no está pensada para utilizarse tal cual (aunque un [!DNL .war] que se puede implementar rápidamente). Está diseñada principalmente como referencia que puede utilizar para crear su propio servidor de licencias personalizado.

   Características del servidor de licencias:

   * Administra las solicitudes de autenticación mediante una base de datos para validar el nombre de usuario y la contraseña.
   * Administra las solicitudes de licencia y determina el tipo de licencia que se emite al aplicar el encadenamiento de licencias.
   * Emite licencias para contenido que incluye varias políticas DRM de Primetime.
   * Emite licencias compatibles con la entrega de claves remotas a clientes de iOS, lo que requiere DRM de Primetime.
   * Emite licencias que requieren una búsqueda externa y la recuperación de la clave de cifrado de contenido (CEK).
   * Busca en una base de datos para determinar si un usuario está autorizado para ver contenido.
   * Busca listas de actualización de directivas DRM de Primetime.
   * Busca listas de revocación de equipos.
   * Utiliza un archivo HSM o PKCS12 para almacenar credenciales.
   * Cifra las contraseñas especificadas en un archivo de propiedades.
   * Especifica varias credenciales de transporte o servidor de licencias después de renovar las credenciales.

      Las credenciales antiguas se mantienen en el servidor para que los usuarios puedan seguir viendo el contenido existente sin tener que volver a empaquetar.
   * Restringe las versiones de DRM/Runtime permitidas para realizar solicitudes a un servidor de licencias.
   * Establece las preferencias de devanado de reloj de cliente.
   * Restringe la diferencia horaria que se permite entre el tiempo de la solicitud y el tiempo del servidor para evitar ataques de reproducción.
   * Administra solicitudes de clientes de FMRMS 1.x

      Por ejemplo, el cliente FMRMS 1.x se activa para actualizar a Primetime DRM 2.0 o posterior.
   * Convierte los metadatos de FMRMS 1.x en metadatos de DRM de Primetime bajo demanda mediante el uso de la información de licencia de FMRMS 1.x almacenada en una base de datos.
   * Convierte las directivas de FMRMS 1.x en directivas de DRM de Primetime para el código de ejemplo.
   * Importa información de licencia de FMRMS 1.x de una base de datos existente para scripts de ejemplo.
   * Obtiene la versión del servidor
   * Registro de dominios
   * Anulación del registro de dominio
   * Solicitudes de sincronización
   * Devolución de licencia

* **Servidor DRM de Primetime para flujo protegido** - Este es un binario listo para usar que puede implementar rápidamente con un esfuerzo mínimo. Es una buena opción para los clientes que desean mostrar rápidamente una prueba de concepto o *podría* ser una opción de producción si las necesidades de DRM personalizadas son mínimas. Para obtener más información, consulte Información relacionada a continuación.

* **El servicio DRM de Primetime Cloud** : es un servidor de licencias alojado en el Adobe que puede utilizar para el servicio de licencias. (Debe ser titular de una licencia de Primetime para utilizar este servicio). Este servicio en la nube de Adobe le libera de los gastos, el mantenimiento y la ingeniería necesarios para crear su propio servicio. Para obtener más información, consulte Información relacionada a continuación.
