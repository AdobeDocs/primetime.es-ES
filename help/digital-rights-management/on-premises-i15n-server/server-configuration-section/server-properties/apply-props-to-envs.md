---
description: 'Debe configurar las propiedades del servidor para que reflejen su entorno. Puede hacerlo mediante cualquiera de las siguientes acciones '
seo-description: 'Debe configurar las propiedades del servidor para que reflejen su entorno. Puede hacerlo mediante cualquiera de las siguientes acciones '
seo-title: Aplicar propiedades a entornos de servidor
title: Aplicar propiedades a entornos de servidor
uuid: a1ee0d6c-b5e7-4689-b7c8-b155176faf1c
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# Aplicar propiedades a entornos de servidor{#apply-properties-to-server-environments}

Debe configurar las propiedades del servidor para que reflejen su entorno. Puede hacerlo mediante cualquiera de los siguientes métodos:

* [!DNL flashaccess-i15n.properties] - Ejemplos incluidos en cada uno de los  [!DNL .war] archivos

* [!DNL AdobeInitial.properties] - Ejemplo ubicado en la  [!DNL /shared] carpeta del DVD

   Puede utilizar este archivo para anular las propiedades establecidas en el archivo WAR de la siguiente manera:

   1. Configure los valores de propiedad que se sobrescriben en [!DNL AdobeInitial.properties]
   1. Coloque [!DNL AdobeInitial.properties] en la ruta de clases.

   >[!NOTE]
   >
   >Adobe recomienda que utilice el archivo [!DNL AdobeInitial.properties], ya que esto le permite actualizar los archivos WAR de la aplicación sin correr el riesgo de perder cualquier configuración de propiedad anterior que haya realizado en el archivo [!DNL flashaccess-i15n.properties].

* El mecanismo de propiedades del sistema Java.

Puede aplicar propiedades individuales a estos entornos de servidor específicos:

* *Desarrollo*
* *Ensayo*
* *Producción*

Con esta capacidad, puede utilizar el mismo archivo WAR para todos los entornos del servidor. Para aplicar propiedades a entornos específicos, anexe dos caracteres de subrayado (&#39; `__`&#39;) más uno de los siguientes códigos de entorno a la propiedad *name*:

    * `DEV`
    * `STAGE`
    * `PROD

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

Por ejemplo: para establecer el nivel de registro en `INFO` para los servidores de ensayo y producción y en `DEBUG` para el servidor de desarrollo:

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

El servidor emplea este orden de búsqueda para las propiedades:

1. `propertyname_environment` in  [!DNL AdobeInitial.properties]

1. `propertyname_environment` in  [!DNL flashaccess-15n.properties]

1. `propertyname_environment` en propiedades del sistema Java
1. `propertyname` in  [!DNL AdobeInitial.properties]

1. `propertyname` in  [!DNL flashaccess-15n.properties]

1. `propertyname` en propiedades del sistema Java

>[!NOTE]
>
>Debe especificar el nombre de entorno del servidor como una propiedad de sistema Java al iniciar el servidor. Por ejemplo, al iniciar Tomcat con [!DNL catalina.bat], establezca la variable de entorno `CATALINA_OPTS` de la siguiente manera:
>-DENVIRONMENT_NAME=[ DEV | FASE | PROD ]
