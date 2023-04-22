<p align="center">
  <img src="https://user-images.githubusercontent.com/126183973/233773172-cf7eefea-4a55-47ac-981f-17d0ebf2f5a8.jpg" />
</p>

### AWS-ResourceMonitoringAutomation - Abril 2023

**Objetivo:**

Automatizar el monitoreo de recursos de AWS y la configuración de servicios de registro utilizando AWS CloudFormation o Terraform.

**Servicios de AWS involucrados:**

  - Amazon **CloudWatch**: para monitorear y recolectar métricas de tus recursos de AWS.
  - Amazon **CloudWatch Alarms**: para crear alarmas que te notifiquen o realicen acciones automáticas basadas en las métricas que estés monitoreando.
  - AWS **CloudTrail**: para habilitar el registro de eventos y actividades de la API de AWS en tu cuenta.
  - AWS **Config**: para evaluar y auditar la configuración de tus recursos de AWS.
  - Amazon **SNS** (Simple Notification Service): para enviar notificaciones en caso de que se dispare una alarma.


**Archivos y código a crear:**

  :one:. Un archivo de plantilla de AWS CloudFormation (en YAML o JSON) o un archivo de configuración de Terraform (en HCL) que incluya:

   - La configuración de Amazon **CloudWatch Alarms** para recursos específicos y métricas (por ejemplo, CPUUtilization para una instancia EC2).
   - La configuración de AWS **CloudTrail** para habilitar el registro de eventos y actividades de la API en tu cuenta.
   - La configuración de AWS **Config** para evaluar y auditar la configuración de tus recursos de AWS.
   - La configuración de Amazon **SNS** para enviar notificaciones cuando se disparen las alarmas.
    
  :two:. Un archivo README.md que explique:

   - El propósito y los objetivos del proyecto.
   - Cómo desplegar y configurar el proyecto utilizando AWS CloudFormation o Terraform.
   - Cómo personalizar y ampliar el proyecto para monitorear diferentes recursos y métricas.
    
**Resultado esperado:**

Al finalizar el proyecto tendremos una solución de **monitoreo y registro de recursos de AWS** automatizada que podremos desplegar fácilmente mediante AWS CloudFormation o Terraform. La solución incluirá alarmas personalizadas basadas en métricas específicas, registro de eventos y actividades de la API, y configuración de auditoría de recursos.

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
