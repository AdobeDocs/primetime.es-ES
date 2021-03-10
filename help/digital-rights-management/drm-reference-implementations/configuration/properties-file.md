---
title: Archivo de propiedades del servidor de licencias
description: Archivo de propiedades del servidor de licencias
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# Archivo de propiedades del servidor de licencias{#license-server-properties-file}

El servidor de licencias hace referencia a las propiedades establecidas en el archivo [!DNL flashaccess-refimpl.properties]. Puede consultar ese archivo directamente para obtener detalles sobre valores específicos y para obtener información sobre el uso de cada propiedad. Se proporciona una muestra completamente funcional en el directorio [!DNL resources] de la implementación de referencia ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`).

**Credenciales** : el archivo de propiedades incluye la configuración de la ubicación de las credenciales que le emite el Adobe. Puede especificar estas credenciales en un archivo [!DNL .pfx] con contraseña o proporcionar un alias y una contraseña para una credencial almacenada en un HSM. Debe configurar al menos las propiedades relacionadas con la credencial de transporte y la credencial del servidor de licencias. Especifique las ubicaciones de los archivos de credenciales en relación con el directorio que especifique en la propiedad `config.resourcesDirectory`.

**Flash Media Rights Management Server** : el  `flashaccess-refimpl.properties` archivo también incluye varias propiedades relacionadas con el empaquetado de contenido. Estas propiedades solo se utilizan para la conversión de metadatos de Flash Media Rights Management Server 1.x. Después de modificar los valores de este archivo de propiedad, para que los cambios surtan efecto, reinicie el servidor de licencias.
