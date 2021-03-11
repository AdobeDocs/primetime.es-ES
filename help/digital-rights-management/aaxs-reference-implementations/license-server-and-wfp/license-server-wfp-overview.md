---
title: Resumen del servidor de licencias y del paquete de carpetas visto
description: Resumen del servidor de licencias y del paquete de carpetas visto
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# Resumen del servidor de licencias y del paquete de carpetas visto {#license-server-and-watched-folder-packager-overview}

El servidor de implementación de referencia puede ayudarle a crear un servidor de licencias mediante el SDK de acceso a Adobe. En esta implementación, los usuarios se autentican en función de las entradas de usuario en una base de datos. El servidor incluye lógica empresarial de demostración para la emisión de licencias. También implementa compatibilidad con Flash Media Rights Management Server 1.0 y 1.5.

El servidor de implementación de referencia también incluye una implementación de carpeta vigilada del empaquetador. Este componente puede implementarse junto con el servidor de licencias o en un equipo independiente. Con esta implementación del empaquetador, se pueden crear varias carpetas vigiladas. Cuando el contenido se suelta en la carpeta vigilada, el empaquetador empaqueta automáticamente el contenido.

El servidor de licencias y el empaquetador se implementan como archivos WAR separados, por lo que puede elegir si ejecutarlos en servidores separados o en una sola instancia de Apache Tomcat®. El servidor de licencias está en [!DNL flashaccess.war] y el empaquetador en [!DNL flashaccess-packager.war]. El [!DNL edcws.war] opcional contiene soporte para solicitudes de licencia de clientes FMRMS 1.x.

El código de muestra de Implementación de referencia muestra las siguientes funciones:

* Servidor de licencias:

   * Gestión de solicitudes de autenticación, uso de una base de datos para validar el nombre de usuario y la contraseña
   * Gestión de solicitudes de licencia y determinación del tipo de licencia que se va a emitir cuando se utiliza la encadenación de licencias.
   * Emisión de licencias para contenido que contiene varias políticas
   * Emita licencias que admitan el envío de claves remotas a clientes de iOS (requiere Adobe Primetime)
   * Emisión de licencias que requieren una búsqueda/recuperación externa de la clave de cifrado de contenido (CEK)
   * Uso de la base de datos para determinar si el usuario está autorizado a ver el contenido
   * Uso de listas de actualización de directivas
   * Uso de listas de revocación de máquina
   * Uso de un archivo HSM o PKCS12 para almacenar credenciales
   * Codificación de contraseñas especificadas en el archivo de propiedades
   * Especificación de varias credenciales de transporte o servidor de licencias (una vez renovadas las credenciales antiguas se mantienen en el servidor para que el contenido existente se pueda consumir sin necesidad de volver a empaquetar)
   * Restricción de las versiones de DRM/Runtime permitidas para realizar solicitudes al servidor de licencias
   * Configuración de las preferencias de la ventana del reloj del cliente
   * Restricción de la diferencia de tiempo permitida entre la hora de solicitud y la hora del servidor (para evitar ataques de repetición)
   * Gestión de solicitudes de clientes de FMRMS 1.x (cliente de déclencheur FMRMS 1.x para actualizar a Adobe Access 2.0 o posterior)
   * Conversión de metadatos de FMRMS 1.x a metadatos de Adobe Access sobre la marcha, utilizando información de licencia de FMRMS 1.x almacenada en una base de datos
   * Código de ejemplo para convertir las políticas de FMRMS 1.x a las políticas de acceso al Adobe
   * Secuencias de comandos de ejemplo para importar información de licencia de FMRMS 1.x desde una base de datos existente
   * Obtener versión del servidor
   * Registro de dominios
   * Desregistro de dominios
   * Solicitudes de sincronización
   * Regreso de la licencia

* Servidor de Packager:

   * Implementación de una implementación de paquete que agrupa automáticamente el contenido añadido a una carpeta vigilada
   * Uso de un archivo HSM o PKCS12 para almacenar credenciales
   * Codificación de contraseñas especificadas en el archivo de propiedades
   * Configuración del empaquetador, creación de políticas y creación de listas de actualización de directivas mediante una aplicación de AIR

