<p align="center">
  <img src="https://user-images.githubusercontent.com/126183973/233773172-cf7eefea-4a55-47ac-981f-17d0ebf2f5a8.jpg" />
</p>

### AWS-ResourceMonitoringAutomation 

**Objetivo:**

Automatizar el monitoreo de recursos de AWS y la configuración de servicios de registro utilizando AWS CloudFormation.

**Servicios de AWS involucrados:**

  - Amazon **CloudWatch**: para monitorear y recolectar métricas de tus recursos de AWS.
  - Amazon **CloudWatch Alarms**: para crear alarmas que te notifiquen o realicen acciones automáticas basadas en las métricas que estés monitoreando.
  - AWS **CloudTrail**: para habilitar el registro de eventos y actividades de la API de AWS en tu cuenta.
  - AWS **Config**: para evaluar y auditar la configuración de tus recursos de AWS.
  - Amazon **SNS** (Simple Notification Service): para enviar notificaciones en caso de que se dispare una alarma.


**Archivos y código a crear:**

  :one:. Un archivo de plantilla de AWS CloudFormation (en YAML o JSON) que incluya:

   - La configuración de Amazon **CloudWatch Alarms** para recursos específicos y métricas (por ejemplo, CPUUtilization para una instancia EC2).
   - La configuración de AWS **CloudTrail** para habilitar el registro de eventos y actividades de la API en tu cuenta.
   - La configuración de AWS **Config** para evaluar y auditar la configuración de tus recursos de AWS.
   - La configuración de Amazon **SNS** para enviar notificaciones cuando se disparen las alarmas.
    
  :two:. Un archivo README.md con instrucciones:

   - Objetivos del proyecto.
   - Cómo desplegar y configurar el proyecto utilizando AWS CloudFormation.
   - Cómo personalizar y ampliar el proyecto para monitorear diferentes recursos y métricas.
    
**Resultado esperado:**

Al finalizar el proyecto tendremos una solución de **monitoreo y registro de recursos de AWS** automatizada que podremos desplegar fácilmente mediante AWS CloudFormation. La solución incluirá alarmas personalizadas basadas en métricas específicas, registro de eventos y actividades de la API, y configuración de auditoría de recursos.

***

### Paso 1: Diseño de la infraestructura

**AWS CloudTrail:**
  - Crearemos un nuevo trail en CloudTrail.
  - El trail estará habilitado para todas las regiones.
  - Los eventos de administración y datos se registrarán.
  - Los registros se guardarán en un bucket de Amazon S3.
  - Configurar el cifrado y la retención de registros.

**AWS Config:**
  - Habilitaremos AWS Config en todas las regiones de la cuenta de AWS.
  - Configuraremos un bucket de S3 para almacenar los datos de configuración de los recursos.
  - Agregaremos reglas de AWS Config para verificar el cumplimiento de políticas específicas.

**Amazon CloudWatch:**
  - Crearemos alarmas de CloudWatch para métricas específicas de los recursos de AWS.
  - Alarmas como la de monitorear el uso de CPU de las instancias EC2 o el número de errores en una cola de mensajes SQS.
  - Configuraremos las acciones que se realizarán cuando se disparen las alarmas, como enviar notificaciones a través de Amazon SNS.

**Amazon SNS:**
  - Crearemos un nuevo tema de SNS para enviar notificaciones cuando se disparen las alarmas de CloudWatch.
  - Los suscriptores pueden recibir notificaciones por correo electrónico, SMS u otros.

### Paso 2: Creación de la plantilla de AWS CloudFormation

Archivo YAML de CloudFormation que cubre los servicios AWS CloudTrail, AWS Config, Amazon CloudWatch y Amazon SNS

[monitoring_resources.yml](https://github.com/ccalvop/AWS-ResourceMonitoringAutomation/blob/main/monitoring_resources.yml)

**Instrucciones para usar la plantilla de CloudFormation:**
  - En AWS **CloudFormation**, botón "Crear pila" en la esquina superior derecha.
  - Seleccionar "Cargar una plantilla de archivo" y hacer clic en "Seleccionar archivo". Selecciona el archivo `monitoring_resources.yml` 
  - Nombrar la pila, configurar etiquetas y permisos (usar usuario adecuado), click `crear recursos con roles personalizados en tu nombre`

**Revertir los cambios de la plantilla de CloudFormation:**

Para revertir los cambios realizados por la plantilla de CloudFormation, se puede eliminar la pila de CloudFormation que se creó a partir de la plantilla. Esto eliminará todos los recursos creados por la plantilla, como el trail de CloudTrail, el registro de configuración y las alarmas de CloudWatch, pero hemos establecido la política de eliminación del bucket S3 a "Retain", lo que significa que el bucket de S3 no se eliminará automáticamente.

***

### Personalizar y ampliar el proyecto para monitorear diferentes recursos y métricas

Para personalizar y ampliar el proyecto, se pueden agregar, modificar o eliminar recursos y métricas en el archivo [monitoring_resources.yml](https://github.com/ccalvop/AWS-ResourceMonitoringAutomation/blob/main/monitoring_resources.yml)

  - Agregar o modificar alarmas de CloudWatch: Actualmente, se han definido alarmas de CloudWatch para monitorear la utilización de CPU y el número de conexiones de red en las instancias EC2. Si deseas agregar nuevas alarmas o modificar las existentes, puedes hacerlo en la sección Resources del archivo monitoring_resources.yml. Por ejemplo, podrías agregar una alarma para monitorear la utilización de memoria de las instancias EC2 o modificar los umbrales de las alarmas existentes.

  ![1CloudWatch_](https://user-images.githubusercontent.com/126183973/233782052-ba5017d3-2c0f-4159-a686-ed81f7273932.png)

  _Modificar el umbral de la alarma(cambia Threshold a otro valor)._

  - Monitorear otros recursos de AWS: Si deseas monitorear otros recursos de AWS, como RDS, Lambda o ELB, puedes agregar nuevas alarmas de CloudWatch en la sección Resources del archivo monitoring_resources.yml. Por ejemplo, podrías agregar una alarma para monitorear el espacio libre en disco de una instancia RDS.

  ![FreeStorageSpaceAlarm](https://user-images.githubusercontent.com/126183973/233782106-c8cdcce5-834e-4cd1-bd89-0be205fc4c71.png)

  - Agregar métricas personalizadas: Si tienes métricas personalizadas que deseas monitorear, puedes agregarlas a CloudWatch utilizando la CLI de AWS. Luego, puedes crear alarmas de CloudWatch en el archivo monitoring_resources.yml para monitorear estas métricas personalizadas.

  Métrica personalizada: `MyCustomMetric`
  
  en **CLI** de AWS: 
  
  `aws cloudwatch put-metric-data --namespace MyNamespace --metric-name MyCustomMetric --value 42 --unit Count`
  
  _Agregar una alarma de CloudWatch para monitorear esta métrica_
  
  ![MyCustomMetricAlarm](https://user-images.githubusercontent.com/126183973/233782227-598aad40-fb1d-4d89-9f50-63716b3f94b0.png)

  - Configurar la retención de registros en CloudWatch Logs: Si deseas modificar la política de retención de registros en CloudWatch Logs, puedes hacerlo en la sección Resources del archivo monitoring_resources.yml. Por ejemplo, podrías modificar el valor del atributo RetentionInDays del recurso LogGroup para ajustar la cantidad de días que se retienen los registros.

  ![MyLogGroup](https://user-images.githubusercontent.com/126183973/233782845-1a077b8d-9c05-4dad-988c-d099556e0009.png)

  _Al agregar este fragmento de código a la sección "Resources", se creará un log group en CloudWatch Logs con una retención de registros de 14 días._

  - Configurar AWS Config: Si deseas agregar o modificar las reglas de AWS Config para evaluar la conformidad de tus recursos de AWS, puedes hacerlo en la sección Resources del archivo monitoring_resources.yml. Por ejemplo, podrías agregar una regla para verificar que las instancias EC2 no están utilizando un tipo de instancia específico o que todos los recursos tienen una etiqueta "Owner".

  _Agregar una regla de AWS Config para verificar que las instancias EC2 no están utilizando un tipo de instancia específico (por ejemplo, t2.micro):_

  ![EC2InstanceTypeRule](https://user-images.githubusercontent.com/126183973/233782315-ff39881a-63f6-4f5d-820a-4d559f74c5f6.png)

  _Agregar una regla de AWS Config para verificar cada 24h que todos los recursos tengan una etiqueta "Owner"_

  ![ResourceOwnerTagRule](https://user-images.githubusercontent.com/126183973/233782916-a36dd7f5-de3a-41c8-abaa-b391c8f483db.png)

  _Se puede agregar este fragmento de código a la sección "Resources" del archivo monitoring_resources.yml_
