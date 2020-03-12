---
seo-title: Opciones de implementación del servidor de licencias
title: Opciones de implementación del servidor de licencias
uuid: 297c587f-23e2-4bb5-911b-72d7b82370f4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Opciones de implementación del servidor de licencias{#license-server-deployment-options}

El servidor de licencias se puede implementar mediante una de las siguientes opciones:

* **Servidor de Adobe Access para flujo continuo** protegido: este servidor de licencias está optimizado para flujo continuo. Por ejemplo, puede configurar el servidor para el flujo dinámico HTTP de Adobe con Adobe Access. Este servidor se puede implementar fácilmente con muy poca configuración necesaria y admitirá varios inquilinos, y puede lograr un alto nivel de escalabilidad. Sin embargo, como esta implementación está optimizada para la transmisión por flujo continuo, no admite todas las funciones de Adobe Access. Por ejemplo, no se admiten la autenticación de nombre de usuario/contraseña, dominios y encadenamiento de licencias. Las reglas de uso de las licencias emitidas por este servidor se controlan mediante un archivo de configuración de servidor, que anula la directiva utilizada en el empaquetado. Consulte la Guía *de flujo protegido de* Adobe Access Server para obtener más información sobre las reglas de uso admitidas por este servidor.
* **Servidor** de licencias de implementación de referencia: utilice esta configuración como punto de partida para una implementación de servidor personalizada. Se trata de un ejemplo de implementación de servidor de licencias, incluido el código fuente, que muestra cómo utilizar las API en el SDK de Adobe Access para gestionar todos los tipos de solicitudes y cómo implementar la lógica empresarial personalizada respaldada por una base de datos. Las reglas de uso de las licencias emitidas por este servidor se controlan mediante la directiva asociada al contenido en el momento del empaquetado.
* **Implementación** de servidor personalizado: también puede implementar su propio servidor de licencias mediante el SDK. La información de este capítulo describe las API utilizadas para implementar un servidor de licencias.

