---
title: Evite utilizar "&'reg_code en la solicitud /authentication
description: Evite utilizar "&'reg_code en la solicitud /authentication
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Evite utilizar &quot;&amp;&#39;reg_code en la solicitud /authentication {#clientless-avoid-using-reg_code-in-authenticate-request}

>[!NOTE]
>
>El contenido de esta página se proporciona únicamente con fines informativos. El uso de esta API requiere una licencia actual de Adobe. No se permite ningún uso no autorizado.

</br>



## Problema

El navegador IE 9 interpreta &#39;\®&#39; como un comando especial y lo convierte a ®. 

## Explicación

Si la variable `/authenticate` se compone de la siguiente manera:

 

```
    <FQDN>authenticate? requestor_id=someRequestor&reg_code=EKAFMFI&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
```
 

...el explorador IE lo interpretará como se muestra a continuación y se enviará a Adobe en este formato:

 

```
    <FQDN>authenticate?requestor_id=someRequestor&reg;_code=EKAFMFI&domain_name=someRequestor.com&noflash=true&mso_id=someMvpd&redirect_url=someRequestor.redirect.url.html
```
 

El solicitante\_id se interpretará como univision®\_code=EKAFIFM, ya que no hay &quot;&amp;&quot; y el Adobe no encontrará `regCode` para asociar el token.  Existe la posibilidad de que el token AuthN no se cree, en cuyo caso `/checkauthn` Las llamadas de no encontrarán tokens.



## Solución

Una de las siguientes opciones debería resolver este problema:

1. Evite utilizar la variable `&reg_code` parámetro entre los demás parámetros de cadena de consulta.  En su lugar, muévala al primer parámetro de cadena de consulta en la dirección URL de la solicitud, por lo que la dirección URL de la solicitud es la siguiente:\
    

       &lt;fqdn>authentication?reg_code =EKAFMI&amp;requestor_id=someRequestor&amp;domain_name=someRequestor.com&amp;noflash=true&amp;mso_id=someMvpd&amp;redirect_url=someRequestor.redirect.url.html
   

   De este modo, la variable `&reg` param no se interpretará incorrectamente.

1. Normalizar `&reg_code` como `&amp;reg_code`.

1. Adobe podría introducir una nueva función para enviar un código de error de vuelta a la segunda pantalla en respuesta a una llamada de autenticación, si la creación del token AuthN falla.

