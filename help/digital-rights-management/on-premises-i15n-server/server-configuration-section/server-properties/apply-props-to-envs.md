---
description: 'Debe configurar las propiedades del servidor para que reflejen su entorno. Puede hacerlo utilizando cualquiera de los siguientes métodos: '
title: Aplicar propiedades a entornos de servidor
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Aplicar propiedades a entornos de servidor{#apply-properties-to-server-environments}

Debe configurar las propiedades del servidor para que reflejen su entorno. Puede hacerlo mediante cualquiera de las siguientes opciones:

* [!DNL flashaccess-i15n.properties] - Muestras incluidas en cada uno de los  [!DNL .war] archivos

* [!DNL AdobeInitial.properties] - Muestra ubicada en la  [!DNL /shared] carpeta del DVD

   Puede utilizar este archivo para anular las propiedades establecidas en el archivo WAR de la siguiente manera:

   1. Establezca los valores de propiedad principales en [!DNL AdobeInitial.properties]
   1. Coloque [!DNL AdobeInitial.properties] en la ruta de clase.

   >[!NOTE]
   >
   >Adobe recomienda que utilice el archivo [!DNL AdobeInitial.properties], ya que esto le permite actualizar sus archivos WAR de la aplicación sin correr el riesgo de perder ninguna configuración de propiedad anterior que haya hecho en el archivo [!DNL flashaccess-i15n.properties].

* Mecanismo de propiedad del sistema Java.

Puede aplicar propiedades individuales a estos entornos de servidor específicos:

* *Desarrollo*
* *Ensayo*
* *Producción*

Con esta capacidad, puede utilizar el mismo archivo WAR para todos los entornos de servidor. Para aplicar propiedades a entornos específicos, añada dos caracteres de guion bajo (&#39; `__`&#39;) más uno de los siguientes códigos de entorno a la propiedad *name*:

    * `DEV`
    * `STAGE`
    * `PROD`

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

Por ejemplo, para establecer el nivel de registro en `INFO` para los servidores de producción y ensayo y en `DEBUG` para el servidor de desarrollo:

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

El servidor emplea este orden de búsqueda para propiedades:

1. `propertyname_environment` en  [!DNL AdobeInitial.properties]

1. `propertyname_environment` en  [!DNL flashaccess-15n.properties]

1. `propertyname_environment` en propiedades del sistema Java
1. `propertyname` en  [!DNL AdobeInitial.properties]

1. `propertyname` en  [!DNL flashaccess-15n.properties]

1. `propertyname` en propiedades del sistema Java

>[!NOTE]
>
>Debe especificar el nombre de entorno del servidor como una propiedad de sistema Java al iniciar el servidor. Por ejemplo, al iniciar Tomcat con [!DNL catalina.bat], configure la variable de entorno `CATALINA_OPTS` de la siguiente manera:
>-DENVIRONMENT_NAME=[ DEV | STAGE | PROD ]
