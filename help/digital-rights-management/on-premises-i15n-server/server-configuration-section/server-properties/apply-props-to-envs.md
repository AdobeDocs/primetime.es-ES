---
description: Debe configurar las propiedades del servidor para que reflejen su entorno. Puede hacerlo mediante cualquiera de las siguientes opciones
title: Aplicar propiedades a entornos de servidor
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Aplicar propiedades a entornos de servidor{#apply-properties-to-server-environments}

Debe configurar las propiedades del servidor para que reflejen su entorno. Puede hacerlo mediante cualquiera de las siguientes opciones:

* [!DNL flashaccess-i15n.properties] - Muestras incluidas en cada una de las [!DNL .war] archivos

* [!DNL AdobeInitial.properties] - Muestra ubicada en el [!DNL /shared] carpeta en el DVD

  Puede utilizar este archivo para anular las propiedades establecidas en el archivo WAR de la siguiente manera:

   1. Establezca los valores de propiedad de anulación en [!DNL AdobeInitial.properties]
   1. Lugar [!DNL AdobeInitial.properties] en la ruta de clase.

  >[!NOTE]
  >
  >El Adobe recomienda que utilice el [!DNL AdobeInitial.properties] , ya que esto le permite actualizar los archivos WAR de la aplicación sin correr el riesgo de perder ninguna configuración de propiedad anterior que haya realizado en el [!DNL flashaccess-i15n.properties] archivo.

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

Por ejemplo, para establecer el nivel de registro en `INFO` para los servidores de producción y ensayo, y para `DEBUG` para su servidor de desarrollo:

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

El servidor emplea este orden de búsqueda para las propiedades:

1. `propertyname_environment` in [!DNL AdobeInitial.properties]

1. `propertyname_environment` in [!DNL flashaccess-15n.properties]

1. `propertyname_environment` en propiedades del sistema Java
1. `propertyname` in [!DNL AdobeInitial.properties]

1. `propertyname` in [!DNL flashaccess-15n.properties]

1. `propertyname` en propiedades del sistema Java

>[!NOTE]
>
>Debe especificar el nombre de entorno del servidor como una propiedad del sistema Java al iniciar el servidor. Por ejemplo, al iniciar Tomcat con [!DNL catalina.bat], configure el `CATALINA_OPTS` como se indica a continuación:
>-DENVIRONMENT_NAME=[DEV | FASE | PROD]
