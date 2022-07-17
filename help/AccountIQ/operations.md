---
title: Operaciones en IQ de cuenta
description: Las operaciones en Account IQ implican realizar acciones para realizar automatizaciones y operaciones masivas en cuentas de suscriptores y rastrear sus efectos.
source-git-commit: e61cca77bad4f01de871e300dc99d7368c283f2a
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---


# Operaciones {#operations-tab-next-steps}

Una vez que haya comprendido los patrones de uso de sus suscriptores y haya identificado el uso compartido de contraseñas para un segmento seleccionado (mediante el uso de Reports and Analytics en Account IQ), puede realizar acciones dirigidas a un objetivo para mitigar el uso compartido de contraseñas.

La funcionalidad Operaciones de Account IQ ayuda a abordar y administrar de forma eficaz el uso compartido de credenciales mediante procedimientos centrados denominados operaciones. Le ofrece opciones para diseñar acciones objetivas y dirigidas a la medida (basadas en el objetivo) para grupos específicos de cuentas de suscriptor y automatizar su ejecución para una duración futura. A través de la funcionalidad Operaciones, no solo puede crear y ejecutar operaciones, sino también medir su impacto. Por lo tanto, al medir los impactos, puede ajustar su estrategia para optimizar el efecto, ya sea convirtiendo a los prestatarios o mitigando el uso compartido de las credenciales.

Para ver **Operaciones** selección de página **Operaciones** opción bajo **Acciones** en la navegación izquierda de la aplicación Account IQ. La página Operaciones enumera todas las operaciones que ya existen en el sistema de Account IQ, junto con sus detalles.

![](assets/operations-page.png)

*Figura: Lista y detalles de operaciones existentes en Account IQ*

En la página Operaciones puede:

* Ver una lista de operaciones ya existentes en Account IQ

* Ver detalles de la operación, como:

   * estado (programado, en ejecución, finalizado, error o detenido)

   * progreso (en porcentaje de finalización)

   * audiencia de destino (segmento en el que se ejecutará la operación)

   * programación (fecha de inicio y finalización de la operación)

   * creación y fecha de finalización de la operación

* [Crear nueva operación](/help/AccountIQ/operation-affecting-user-segment.md)

* [Ver informes de operaciones](#operation-reports)

<!--* Search from the list of operations using Search field

* Stop an operation.

* Create a duplicate operation.

* [Configure columns of Operations details page](#configure-columns)-->

## Ver informes de operaciones {#operation-reports}

Puede analizar el impacto de una operación consultando su informe. Para ver el informe de una operación:

1. Seleccione el nombre de la operación en la página principal Operaciones.

   El informe se muestra en forma de gráfico de barras apiladas.

   ![](assets/operation-impact-report.png)

   *Figura: Informe Operaciones para ver los impactos de las operaciones*

   El eje x representa el periodo de evaluación y el eje y representa una variable para medir el impacto de la operación.

   Por ejemplo, en la imagen anterior, la variable en el eje y es un número de cuentas. Al mirar el gráfico, puede comparar el número de cuentas que están en el segmento de operaciones con el número de cuentas que están fuera del segmento de operaciones en un momento determinado (como la segunda semana del período de evaluación de operaciones). Por lo tanto, puede analizar cómo durante el periodo de evaluación el número de cuentas varía dentro del segmento de operación y fuera del segmento.

   Por lo tanto, si la operación era enviar correos electrónicos de advertencia a cuentas sospechosas, y las cuentas del segmento de operaciones eran aquellas con probabilidad de compartir más de 90 y que usaban más de 5 dispositivos para transmitir contenido, entonces al principio del periodo de evaluación las cuentas del segmento superan los 7 millones. Este número cambia durante el periodo de evaluación como se muestra en el gráfico, lo que indica el impacto de la operación. En función de la evaluación, puede tomar medidas correctivas en cuentas sospechosas, o continuar con la operación, o ajustar la estrategia para obtener mejores resultados para frenar el uso compartido de credenciales.

2. Para cerrar el informe y volver a la página principal Operaciones, seleccione **Operaciones** opción bajo **Acciones** en la navegación izquierda.

<!--

![](assets/operations-details.png)

*Figure: Operation details*
## Configure columns {#configure-columns}

You can select the icon to **Configure columns** on the top of the operations table.

![](assets/config-columns.png)

*Figure: Configure columns of Operations details page*-->