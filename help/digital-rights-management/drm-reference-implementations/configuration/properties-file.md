---
title: Archivo de propiedades del servidor de licencias
description: Archivo de propiedades del servidor de licencias
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# Archivo de propiedades del servidor de licencias{#license-server-properties-file}

El servidor de licencias hace referencia a las propiedades establecidas en la variable [!DNL flashaccess-refimpl.properties] archivo. Puede hacer referencia a ese archivo directamente para obtener detalles sobre valores específicos y para obtener información de uso sobre cada propiedad. Se proporciona una muestra completamente funcional en el [!DNL resources] directorio de la implementación de referencia ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`).

**Credenciales** : el archivo de propiedades incluye opciones para la ubicación de las credenciales que le emite el Adobe. Puede especificar estas credenciales en una [!DNL .pfx] con una contraseña, o proporcione un alias y una contraseña para una credencial almacenada en un HSM. Debe configurar al menos las propiedades relacionadas con la credencial de transporte y la credencial del servidor de licencias. Especifique las ubicaciones de los archivos de credenciales en relación con el directorio especificado en la `config.resourcesDirectory` propiedad.

**Servidor de Rights Management de Flash Media** - El `flashaccess-refimpl.properties` Este archivo también incluye varias propiedades relacionadas con el contenido del paquete. Estas propiedades solo se utilizan para la conversión de metadatos de Flash Media Rights Management Server 1.x. Después de modificar los valores de este fichero de propiedades, reinicie el servidor de licencias para que los cambios surtan efecto.
