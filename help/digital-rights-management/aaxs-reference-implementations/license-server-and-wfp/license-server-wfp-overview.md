---
title: Información general sobre el servidor de licencias y el empaquetador de carpetas inspeccionadas
description: Información general sobre el servidor de licencias y el empaquetador de carpetas inspeccionadas
copied-description: true
exl-id: 1a355068-7ad6-4cc2-8447-49251dae3ff8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# Información general sobre el servidor de licencias y el empaquetador de carpetas inspeccionadas {#license-server-and-watched-folder-packager-overview}

El servidor de implementación de referencia puede ayudarle a crear un servidor de licencias mediante el SDK de acceso a Adobe. En esta implementación, los usuarios se autentican en función de las entradas de usuario de una base de datos. El servidor incluye lógica empresarial de demostración para la emisión de licencias. También se implementa compatibilidad con Flash Media Rights Management Server 1.0 y 1.5.

El servidor de implementación de referencia también incluye una implementación de carpeta vigilada del empaquetador. Este componente se puede implementar junto con el servidor de licencias o en un equipo independiente. Con esta implementación de empaquetador, se pueden crear varias carpetas vigiladas. Cuando se coloca contenido en la carpeta inspeccionada, el empaquetador empaqueta automáticamente el contenido.

El servidor de licencias y el empaquetador se implementan como archivos WAR independientes, por lo que puede elegir si desea ejecutarlos en servidores independientes o en una sola instancia de Apache Tomcat®. El servidor de licencias se encuentra en [!DNL flashaccess.war] y el empaquetador está en [!DNL flashaccess-packager.war]. El opcional [!DNL edcws.war] contiene compatibilidad con solicitudes de licencia de clientes de FMRMS 1.x.

El código de ejemplo Implementación de referencia muestra las siguientes funciones:

* Servidor de licencias:

   * Administrar solicitudes de autenticación mediante una base de datos para validar el nombre de usuario y la contraseña
   * Administrar solicitudes de licencia y determinar qué tipo de licencia emitir cuando se utiliza el encadenamiento de licencias.
   * Emisión de licencias para contenido que contiene varias directivas
   * Emitir licencias compatibles con la entrega de claves remotas a clientes de iOS (requiere Adobe Primetime)
   * Emisión de licencias que requieren una búsqueda/recuperación externa de la clave de cifrado de contenido (CEK)
   * Uso de la base de datos para determinar si el usuario tiene autorización para ver contenido
   * Uso de listas de actualización de directivas
   * Usar listas de revocación automáticas
   * Usar un archivo HSM o PKCS12 para almacenar credenciales
   * Cifrado de contraseñas especificadas en el archivo de propiedades
   * Especificación de varias credenciales de transporte o servidor de licencias (una vez renovadas las credenciales, las credenciales antiguas se mantienen en el servidor para que el contenido existente se pueda consumir sin necesidad de volver a empaquetarlo)
   * Restricción de las versiones de DRM/Runtime permitidas para realizar solicitudes al servidor de licencias
   * Estableciendo preferencias de devanado de reloj de cliente
   * Restricción de la diferencia horaria permitida entre el tiempo de la solicitud y el tiempo del servidor (para evitar ataques de reproducción)
   * Gestión de solicitudes de clientes de FMRMS 1.x (déclencheur al cliente de FMRMS 1.x para actualizar a Adobe Access 2.0 o posterior)
   * Convertir metadatos de FMRMS 1.x a metadatos de acceso de Adobe sobre la marcha, utilizando la información de licencia de FMRMS 1.x almacenada en una base de datos
   * Código de ejemplo para convertir directivas de FMRMS 1.x en directivas de acceso a Adobe
   * Scripts de ejemplo para importar información de licencia de FMRMS 1.x desde una base de datos existente
   * Obtener versión del servidor
   * Registro de dominios
   * Anulación del registro de dominio
   * Solicitudes de sincronización
   * Devolución de licencia

* Servidor de empaquetador:

   * Implementación de una implementación de empaquetador que empaqueta automáticamente el contenido agregado a una carpeta inspeccionada
   * Usar un archivo HSM o PKCS12 para almacenar credenciales
   * Cifrado de contraseñas especificadas en el archivo de propiedades
   * Configuración del empaquetador, creación de directivas y creación de listas de actualización de directivas mediante una aplicación de AIR
