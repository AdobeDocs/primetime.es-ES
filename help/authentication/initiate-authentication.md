---
title: Iniciar autenticación
description: Iniciar autenticación
source-git-commit: 0839e9f2eac7eeeadf9bbfafb2bdd76596f4fb06
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Iniciar autenticación {#initiate-authentication}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

## Puntos finales de API de REST {#clientless-endpoints}

&lt;reggie_fqdn>:

* Producción - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Ensayo - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Producción - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Ensayo - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>


## Descripción {#description}

Inicia el proceso de autenticación informando de un evento de selección de MVPD. Crea un registro en la base de datos de autenticación de Primetime, que se concilia cuando se recibe una respuesta correcta del MVPD. 



| Punto final | Llamada  </br>Por | Entrada   </br>Parámetros | HTTP  </br>Método | Respuesta | HTTP  </br>Respuesta |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authentication | Módulo AuthN | 1. requestor_id (obligatorio)</br>2.  mso_id (obligatorio)</br>3.  reg_code (obligatorio)</br>4.  domain_name (obligatorio)</br>5.  noflash=true -  </br>    (obligatorio, parámetro residual)</br>6.  no_iframe=true (obligatorio, parámetro residual)</br>7.  parámetros adicionales (opcional)</br>8.  redirect_url (obligatorio) | GET | La aplicación web de inicio de sesión se redirige a la página de inicio de sesión de MVPD. | 302 para implementaciones de redireccionamiento completas |

{style=&quot;table-layout:auto&quot;}


| Parámetro de entrada | Descripción |
| --- | --- |
| requestor_id | El solicitante del programador para el que esta operación es válida. |
| mso_id | El ID de MVPD para el que es válida esta operación. |
| reg_code | El código de registro generado por el servicio Reggie. |
| domain_name | El dominio de origen. |
| redirect_url | La URL de redireccionamiento de la aplicación web de inicio de sesión tras la finalización de la autenticación. |

{style=&quot;table-layout:auto&quot;}

</br>

>[!IMPORTANT]
> 
>**Importante: Parámetros obligatorios -** Independientemente de la implementación del lado del cliente, todos los parámetros anteriores son obligatorios.
>
>
>Ejemplo:    
>
>
```
>domain_name=loginwebapp.com
>mso_id=sampleMvpdId
>reg_code=RO0885W
>requestor_id=sampleRequestorId
>noflash=true
>redirect_url=http://loginwebapp.com
>```

>[!IMPORTANT]
> 
>**Importante: Parámetros opcionales**
>
>La llamada también puede contener parámetros opcionales que habilitan otras funcionalidades como:
>
> * generic\_data - habilita el uso de [Paso temporal promocional](https://tve.helpdocsonline.com/promotional-temp-pass)
>
>```JSON
>Example:
>   generic_data=("email":"email@domain.com")
>```


### **Notas** {#notes}

* El valor de la variable `domain_name` debe establecerse en uno de los nombres de dominio registrados con la autenticación de Primetime. Para obtener más información, consulte [Registro e inicialización](http://tve.helpdocsonline.com/new-programmer-overview$reg_and_init).

* [Evite utilizar &quot;&amp;&#39;reg\_code&quot; en la solicitud /authenticate (nota técnica)](https://tve.helpdocsonline.com/clientless:-avoid-using-&#39;&amp;&#39;reg_code-in-/authenticate-request)

* La variable `redirect_url` debe ser el último en orden

* El valor de la variable `redirect_url` debe tener codificación de dirección URL

[Volver a la referencia de la API de REST](http://tve.helpdocsonline.com/rest-api-reference)
