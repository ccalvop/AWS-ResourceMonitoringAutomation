# AWS-ResourceMonitoringAutomation

Abril 2023

**Objetivo:**

Automatizar el monitoreo de recursos de AWS y la configuración de servicios de registro utilizando AWS CloudFormation o Terraform.

**Servicios de AWS involucrados:**

  - Amazon **CloudWatch**: para monitorear y recolectar métricas de tus recursos de AWS.
  - Amazon **CloudWatch Alarms**: para crear alarmas que te notifiquen o realicen acciones automáticas basadas en las métricas que estés monitoreando.
  - AWS **CloudTrail**: para habilitar el registro de eventos y actividades de la API de AWS en tu cuenta.
  - AWS **Config**: para evaluar y auditar la configuración de tus recursos de AWS.
  - Amazon **SNS** (Simple Notification Service): para enviar notificaciones en caso de que se dispare una alarma.


**Archivos y código a crear:**

  1. Un archivo de plantilla de AWS CloudFormation (en YAML o JSON) o un archivo de configuración de Terraform (en HCL) que incluya:

    - La configuración de Amazon **CloudWatch Alarms** para recursos específicos y métricas (por ejemplo, CPUUtilization para una instancia EC2).
    - La configuración de AWS **CloudTrail** para habilitar el registro de eventos y actividades de la API en tu cuenta.
    - La configuración de AWS **Config** para evaluar y auditar la configuración de tus recursos de AWS.
    - La configuración de Amazon **SNS** para enviar notificaciones cuando se disparen las alarmas.
    
  2. Un archivo README.md que explique:

    - El propósito y los objetivos del proyecto.
    - Cómo desplegar y configurar el proyecto utilizando AWS CloudFormation o Terraform.
    - Cómo personalizar y ampliar el proyecto para monitorear diferentes recursos y métricas.
    
**Resultado esperado:**

Al finalizar el proyecto tendremos una solución de **monitoreo y registro de recursos de AWS** automatizada que podremos desplegar fácilmente mediante AWS CloudFormation o Terraform. La solución incluirá alarmas personalizadas basadas en métricas específicas, registro de eventos y actividades de la API, y configuración de auditoría de recursos.
