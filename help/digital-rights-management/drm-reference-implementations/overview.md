---
description: 'null'
seo-description: 'null'
seo-title: Acerca de las implementaciones de referencia
title: Acerca de las implementaciones de referencia
uuid: f08fdb4b-aaa8-4871-bb62-1a21d5abdd8d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Acerca de las implementaciones de referencia{#about-the-reference-implementations}

Esta guía describe la instalación, configuración y funcionamiento de las implementaciones de referencia de Adobe Primetime DRM.

>[!NOTE]
>
>Primetime DRM se llamaba anteriormente Adobe Access y antes de eso, Flash Access.

Las implementaciones de referencia de DRM de Primetime incluyen estos componentes:

* **Herramientas** de línea de comandos: estas herramientas se basan en el mismo código de SDK de DRM de Primetime que se utiliza en el servidor de licencias de DRM de Primetime. Puede realizar tareas de empaquetado, licencias y otras tareas de DRM desde la línea de comandos, y alternar perfectamente entre el uso de las herramientas de la línea de comandos y el servidor de licencias.
* **Servidor** de licencias: servidor de licencias totalmente funcional y personalizable (descrito a continuación como una de las opciones de su servidor de licencias).

**Opciones del servidor de licencias:**

* **Implementaciones** de referencia de DRM de Primetime: el tema de esta guía, esta implementación de referencia, incluye un servidor de licencias de DRM robusto que muestra todas las funciones proporcionadas por el SDK de DRM de Primetime. Esta implementación se entrega con código fuente e instrucciones para la creación del código. Esta implementación no está pensada para utilizarse tal cual (aunque se incluye un [!DNL .war] archivo que puede implementar rápidamente). Se trata principalmente de una referencia que puede utilizar para crear su propio servidor de licencias personalizado.

   Características del servidor de licencias:

   * Gestiona las solicitudes de autenticación mediante una base de datos para validar el nombre de usuario y la contraseña.
   * Gestiona las solicitudes de licencia y determina el tipo de licencia que se emite cuando se aplica la cadena de licencias.
   * Expide licencias para contenido que incluye varias directivas de DRM de Primetime.
   * Expide licencias que admiten el envío de claves remotas a clientes de iOS, lo que requiere Primetime DRM.
   * Expide licencias que requieren una búsqueda externa y la recuperación de la clave de cifrado de contenido (CEK).
   * Busca en una base de datos para determinar si un usuario está autorizado para ver contenido.
   * Busca las listas de actualización de la directiva DRM de Primetime.
   * Busca listas de revocación de máquina.
   * Utiliza un archivo HSM o PKCS12 para almacenar las credenciales.
   * Codifica las contraseñas especificadas en un archivo de propiedades.
   * Especifica varias credenciales de transporte o servidor de licencias después de renovar las credenciales.

      Las credenciales antiguas se mantienen en el servidor para que los usuarios puedan seguir viendo el contenido existente sin tener que volver a empaquetarlo.
   * Restringe las versiones de DRM/Runtime que pueden realizar solicitudes a un servidor de licencias.
   * Establece las preferencias de la ventana del reloj del cliente.
   * Restringe la diferencia horaria permitida entre la hora de solicitud y la hora del servidor para evitar ataques de repetición.
   * Gestiona las solicitudes de los clientes de FMRMS 1.x

      Por ejemplo, el cliente FMRMS 1.x se activa para actualizar a Primetime DRM 2.0 o posterior.
   * Convierte los metadatos de FMRMS 1.x en metadatos DRM Primetime según demanda mediante la información de licencia de FMRMS 1.x almacenada en una base de datos.
   * Convierte las políticas de FMRMS 1.x en políticas de DRM de Primetime para el código de muestra.
   * Importa información de licencia de FMRMS 1.x desde una base de datos existente para secuencias de comandos de ejemplo.
   * Obtiene la versión del servidor
   * Registro de dominios
   * Desregistro de dominios
   * Solicitudes de sincronización
   * Devolución de licencia

* **Servidor Primetime DRM para flujo** protegido: es un binario listo para usar que puede implementar rápidamente con el mínimo esfuerzo. Es una buena opción para los clientes que desean mostrar rápidamente la prueba de concepto o *podría* ser una opción de producción si sus necesidades de DRM personalizadas son mínimas. Para obtener más información, consulte Información relacionada a continuación.

* **El servicio** DRM de Primetime Cloud: es un servidor de licencias alojado por Adobe que puede utilizar para el servicio de licencias. (Debe ser un titular de licencia de Primetime para utilizar este servicio). Este servicio de nube de Adobe le libera de los gastos, el mantenimiento y la ingeniería necesarios para crear su propio servicio. Para obtener más información, consulte Información relacionada a continuación.

