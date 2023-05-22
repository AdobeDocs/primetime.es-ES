---
title: API de informe
description: API del informe de audiencia
exl-id: 50eb4869-3765-4591-8c41-794b29d50044
source-git-commit: 628544e38616715e83e0274ba26cf93302ce0e61
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 1%

---

# API de informe {#report-api}

La interfaz de usuario de ha administrado funciones para clientes y para el equipo de habilitación (Adobe). Los clientes pueden acceder al portal y, a continuación, crear y editar sus configuraciones. También pueden ver los informes de sus impresiones de anuncios en la interfaz de usuario.

Las API trabajan entre bastidores para facilitar a los clientes y administradores la comunicación con la infraestructura back-end.

Para explorar [!DNL Primetime Ad Insertion] API consulte [Puntos finales de API de Ad Insertion en la interfaz de usuario Swaggered](https://adconfigservice-va6.cloud.adobe.io/swagger-ui/index.html#/).

## Extremo de API {#report-api-endpoint}

### Producción {#production}

`https://dai-primetime.adobe.io/report`

### Sandbox {#sandbox}

`https://dai-sandbox1-primetime.adobe.io/report`

## Parámetros de consulta


| Nombre | Importancia | Tipo de valor | ¿Obligatorio? | Valor predeterminado | Restricciones | Ejemplo/ Valores de muestra válidos |
|----------|-----------------------------------------------------------------------------------------------|----------------|----------------|---------------------|------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| endDate | Fecha de finalización de los datos del informe | fecha | Y | NINGUNO | no más reciente que ayer en UTC-8 | ######## |
| filtros | filtrar en una o varias columnas | cadena | N | NINGUNO | ad_config_id , zone_id | ad_config_id=990,900;state=active |
|  |  |  |  |  | Cuando metaData se establece en &quot;true&quot; en la solicitud, también puede filtrar por nombre. |  |
|  |  |  |  |  |  | Las claves de varios filtros se separan con punto y coma. |
|  |  |  |  |  |  | Utilice valores separados por comas para proporcionar una lista de valores para la clave de filtro |
| groupBy | Agrupar por tiempo ( año \| mes \| día) o ad_config_id. Adconfig es sinónimo de AdRule. | cadena | N | NINGUNO | y \| m \| d , ad_config_id | m , ad_config_id |
|  |  |  |  |  |  |  |
|  |  |  |  |  |  | Para groupBy on time, proporcione uno de y, m o d |
|  |  |  |  |  |  |  |



## Encabezados {#headers}

| Nombre | Tipo de valor | Obligatorio | Valor de muestra | Importancia |
|-----------------------|----------------|---------------|-------------------------------------|------------------------------------|
| Aceptar | cadena | Y | text/csv para CSV | Tipo de respuesta esperada de la API |
|  |  |  | application/json o &#39;*/*&#39; para JSON |  |
| Token de autorización | cadena | Y | xyz | token de autorización |
| x-api-key | cadena | Y | xyz | Clave de API |
| x-gw-ims-org-id | cadena | Y | xyz12345 | ID de organización de IMS de su cuenta |

* Puede generar el token de autorización (también conocido como token de acceso) siguiendo los pasos detallados en la página de ayuda de autenticación JWT de Adobe.io.
   >[!NOTE]
   >El token de autorización tiene una caducidad de 24 horas, por lo que si utiliza la API de informes con un script recurrente, asegúrese de generar el token de autenticación antes de su caducidad o cuando reciba un error de OAuth sobre la no validez del token.

* Para establecer los valores correctos en el encabezado de la solicitud y generar el token de autorización (mediante autenticación JWT), necesitará conocer las siguientes configuraciones para su cuenta. Póngase en contacto con el equipo de asistencia de Primetime para obtener estos valores.
ID de cuenta técnica

   * ID de organización
   * Api_key
   * Client_secret

## Output {#output}

El resultado de la consulta de la API de informes de forma predeterminada está en formato JSON, que especifica impresiones con los diferentes valores de las dimensiones (parámetro groupby) solicitadas. A continuación se muestra un ejemplo de salida:

```JSON
[
    {
        "dates": "07-2020",
        "total_impressions": 213007041
    },
    {
        "dates": "08-2020",
        "total_impressions": 174711626
    },
    {
        "dates": "09-2020",
        "total_impressions": 102863153
    }
]
```

## Códigos de error y cadenas {#error-codes-strings}

### Formato de respuesta de error {#error-response-format}

Error al procesar la macro &quot;code&quot;: valor no válido especificado para el parámetro `com.atlassian.confluence.ext.code.render.InvalidValueException`

```Shell
{
"error_code": "<ERROR_CODE>",
"message": "<ERROR_MESSAGE>"
}
```

En la tabla siguiente se enumeran los códigos de error y los mensajes que API de informe puede devolver. Para errores relacionados con la capa de autorización, consulte la [documentación de código de error](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#errors-and-troubleshooting) de Adobe.io.

| Código de error | Mensaje de error |
|-----------------------|------------------------------------------|
| 4001007 | Detalles de usuario no válidos. |
| 4001008 | Todas las zonas no son de la misma cuenta. |
| 5001010 | Se ha producido un error interno. |
| 4001011 | Las fechas no se envían en el formato requerido. |
| 4001012 | Las fechas están fuera del intervalo. |
| 4001013 | Falta el parámetro obligatorio. |
| 4001014 | La lista de zonas está vacía para la cuenta. |
| 4001015 | Claves de filtro no válidas en la solicitud. |
| 4001016 | Opción GroupBy no válida en la solicitud. |
| 4001017 | Se ha proporcionado un ID no válido en la solicitud |

## Llamadas de muestra y resultados esperados {#sample-calls-expected-results}

A continuación se muestra el comando curl para obtener recuentos de impresiones mensuales entre 2020-07-01 y 2021-06-30 mediante el token de acceso:

**Ejemplo de llamada API de informes**

```shell
curl --location --request GET 'https://dai-sandbox1-primetime.adobe.io/report?startDate=2020-07-01&endDate=2021-06-30&groupBy=m&unpaged=true' \
--header 'x-api-key: <API_KEY>' \
--header 'x-gw-ims-org-id: <ORG_ID>' \
--header 'Authorization: Bearer <ACCESS_TOKEN_STRING>' \
--header 'Accept: application/json'
```

| Ejemplo de llamada/caso de uso | Resultado esperado |
|---|---|
| Recuperar informe con GET de fechas de inicio y finalización: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2021-01-01 header : Accept = application/json. o */* | Json con los siguientes parámetros con todos los anuncios que pertenecen a esta cuenta total_impressions |
| Recuperar informe con GroupBy = d \| m \| y GET: [API_ENDPOINT]//report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d \| m \| y header : Accept = application/json. o */* | Json con los parámetros siguientes y todos los anuncios que pertenecen a estas fechas de cuenta (dd-mm-aaaa \| mm-aaaa \| formato aaaa) total_impressions |
| Recuperar informe con GroupBy = ad_config_id GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=ad_config_id header : Accept = application/json. o */* | Json con los siguientes parámetros con todos los anuncios que pertenecen a esta cuenta ad_config_id_total_impressions |
| Recuperar informe con GroupBy = d \| m \| y ad_config_id GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d,ad_config_id encabezado : Accept = application/json. o */* | Json con los siguientes parámetros con todos los anuncios que pertenecen a esta cuenta ad_config_id fechas (formato mm-dd-aaaa \| mm-aaaa \| aaaa formato) total_impressions |
| Recuperar informe con metaData=true y groupBy=d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=ad_config_id header : Accept = application/json. o */* | Json con los siguientes parámetros con todos los anuncios que pertenecen a esta cuenta nombre ad_config_id total_impressions |
| Recuperar informe con groupBy=d \| m \| y ad_config_id GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=d \| m \| y,ad_config_id header : Accept = application/json. o */* | Json con los parámetros siguientes y todos los anuncios que pertenecen a esta cuenta nombre ad_config_id total_impressions fechas (dd-mm-yyyy \| mm-yyyy \| formato yyyy) |
| Recupere el informe para obtener todas las filas de un intervalo de fechas determinado (con GET unpaged = true): [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;groupBy=d&amp;unpaged=true | 31 entradas en la matriz Json devuelta |
| Recuperar informe con parámetros de consulta de página válidos GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;page=0&amp;size=5&amp;groupBy=d | 5 entradas en la matriz devuelta |
| Recuperar informe, con GET de formato csv: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10 encabezado : Accept = text/csv | Se devuelve la cadena CSV con el encabezado: total_impressions |
| Recuperar informe, con formato csv y groupBy = d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;groupBy=d\|m\|y encabezado : Accept = text/csv | Se devuelve la cadena CSV con el encabezado: total_impressions_dates (formato mm-dd-aaaa \| mm-aaaa \| aaaa) |
| Recuperar informe, con formato csv y metadatos = GET verdadera: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true header : Accept = text/csv | Se devuelve la cadena CSV con el encabezado: total_impressions |
| Recuperar informe, con formato csv , metadatos = true y groupBy = d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true&amp;groupBy=d\|m\|y encabezado : Accept = text/csv | Se devuelve la cadena CSV con el encabezado: total_impressions_dates (formato mm-dd-aaaa \| mm-aaaa \| aaaa) |


## Política de limitación de API de informe {#report-api-throttling-policy}

* Se permiten 5 solicitudes de API durante una ventana de 5 segundos para cada usuario.
* Si un usuario supera el límite, la respuesta se retrasa 5 segundos.
* Si un usuario realiza más de 10 llamadas en un intervalo de 5 segundos, comenzará a rechazarse con la respuesta &quot;429 Demasiadas solicitudes&quot;.
