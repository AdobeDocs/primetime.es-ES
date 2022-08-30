---
title: Operaciones en IQ de cuenta
description: Las operaciones en Account IQ implican realizar acciones para realizar automatizaciones y operaciones masivas en cuentas de suscriptores y rastrear sus efectos.
exl-id: ba6bceca-221c-42db-b207-804e4b9f6d54
source-git-commit: 40239b6715d8eab95bc2564fb19eb6832387ad3e
workflow-type: tm+mt
source-wordcount: '467'
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

   El eje X representa el periodo de evaluación y el eje Y representa el impacto de la operación (en términos del número de cuentas en un segmento durante el periodo de evaluación). Cada bar está dividido en tres partes.

   * Una parte representa el número de cuentas que aún cumplen los criterios del segmento de operación.

   * Otra parte representa el número de cuentas activas para ese periodo que originalmente estaban en el segmento, pero que ya no cumplen los criterios del segmento de operación.

   * La tercera parte representa las cuentas que no estaban activas en ese período.
   >[!NOTE]
   >
   >La primera barra representa el número de cuentas que cumplen las condiciones del segmento de operación al comienzo del periodo de evaluación.

   Con el tiempo, el gráfico muestra el efecto de la acción (a través de la operación) indicando el número de cuentas que han cambiado su comportamiento en relación con los criterios originales (por ejemplo, con una probabilidad de uso compartido superior a 90 y con más de 5 dispositivos) o que se han vuelto inactivas.

<!--For example, in the above image the variable on the y-axis is number of accounts. Looking at the graph you can compare the number of accounts that are in the operations' segment versus the number of accounts that are outside the operations segment at a particular time (such as week 2nd of the operations evaluation period). Therefore, you can analyze how over the evaluation period do number of accounts vary within the operation segment and outside the segment.

So, if your operation was to send out warning emails to suspecting accounts, and accounts in operations segment were those with sharing probability more than 90 and using more than 5 devices to stream content, then in the beginning of the evaluation period accounts in segment are more than 17 thousand. This number changes over the evaluation period as shown in the graph, thereby indicating the impact of operation. Based on the evaluation, you can take remedial measures on suspecting accounts, or continue with the operation, or adjust your strategy for better outcomes to curb credential sharing.-->

1. Para cerrar el informe y volver a la página principal Operaciones, seleccione **Operaciones** opción bajo **Acciones** en la navegación izquierda.

<!--

![](assets/operations-details.png)

*Figure: Operation details*
## Configure columns {#configure-columns}

You can select the icon to **Configure columns** on the top of the operations table.

![](assets/config-columns.png)

*Figure: Configure columns of Operations details page*-->