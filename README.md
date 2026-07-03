# Caso de Estudio Final - Implementación de WordPress en AWS para Comercial Nova

## Integrantes y Roles
* **[Tu Nombre / Nombre de tu compañero]**: Consultor de Infraestructura y Redes (VPC, EC2, ALB).
* **[Nombre de tu compañero]**: Consultor de Datos y Seguridad (RDS, S3, IAM, CloudWatch).

## Problema Planteado y Alcance
La empresa "Comercial Nova" requiere migrar su portal web corporativo a la nube para mejorar la disponibilidad, seguridad, escalabilidad y tener un control eficiente de los costos. El alcance de este proyecto es desplegar una arquitectura completa en AWS utilizando WordPress como CMS, implementando alta disponibilidad (Load Balancers), bases de datos administradas, almacenamiento para medios y un sistema de monitoreo.

## Arquitectura Propuesta
Nuestra arquitectura se basa en una VPC personalizada con subredes públicas y privadas para segmentar el tráfico. Utilizamos un Application Load Balancer para distribuir las peticiones a un grupo de instancias EC2 que ejecutan WordPress. La capa de datos está protegida en una subred privada usando Amazon RDS (MySQL), y los archivos multimedia/respaldos se gestionan en Amazon S3.

![Diagrama de Arquitectura](./arquitectura/diagrama.png)

## Servicios Cloud Utilizados
| Servicio AWS | Propósito en la Arquitectura |
| :--- | :--- |
| **Amazon VPC** | Aislamiento de red lógico para proteger los recursos. |
| **Amazon EC2** | Capa de cómputo (servidores web) donde se ejecuta WordPress, Nginx/Apache y PHP. |
| **Amazon RDS** | Base de datos relacional (MySQL/MariaDB) para almacenar el contenido del sitio web de forma segura. |
| **Amazon S3** | Almacenamiento de objetos escalable para medios de WordPress y respaldos. |
| **Application Load Balancer** | Distribución de tráfico entrante entre múltiples instancias EC2 para garantizar Alta Disponibilidad. |
| **Amazon CloudWatch** | Monitoreo del rendimiento de las instancias y bases de datos, con alertas automáticas. |
| **IAM** | Gestión de accesos y permisos aplicando el principio del mínimo privilegio. |

## Pasos para Desplegar (Reproducción del Entorno)
1. Desplegar la VPC con 1 subred pública y 1 subred privada.
2. Configurar los Security Groups (Web y Base de Datos).
3. Desplegar la instancia Amazon RDS (MySQL) en la subred privada.
4. Crear el Bucket S3 con políticas restrictivas.
5. Lanzar instancias EC2 en la subred pública, instalar el stack web e inicializar WordPress.
6. Conectar WordPress a la base de datos RDS.
7. Configurar el Application Load Balancer apuntando a las instancias EC2.

## Acceso al Proyecto
* **URL de WordPress (vía Load Balancer / EC2):** `[http://tu-direccion-ip-o-dns-del-balanceador]`

## Estrategia de Seguridad, Monitoreo y Costos
* **Seguridad:** Los servidores de base de datos no tienen salida directa a Internet (Subred Privada). El acceso SSH está restringido por IP. Se utilizan roles IAM para evitar el uso de credenciales en texto plano.
* **Monitoreo:** Se implementó un Dashboard en CloudWatch para métricas de CPU de EC2 y conexiones a RDS, incluyendo una alarma de uso crítico de CPU (>70%).
* **Costos:** Se estimó el costo en AWS Pricing Calculator. Optimizaciones propuestas: Uso de instancias de nueva generación (t3), horarios de apagado para entornos no productivos y S3 Infrequent Access.

## Evidencias Específicas
Las evidencias detalladas (capturas de pantalla con nombre y hora) se encuentran en la carpeta `/aws/evidencias/` y en el documento PDF adjunto:
* [Evidencias de VPC, EC2, S3, RDS y IAM](./aws/evidencias/)
* [Evidencias de Publicación y Funcionamiento](./wordpress/evidencia_publicacion_contenido.md)
* [Evidencias de CloudWatch (Dashboard y Alerta)](./monitoreo/)

## Limitaciones Conocidas y Mejoras Futuras
* **Limitaciones:** [Ej: Debido a las restricciones de AWS Academy, no se implementó un NAT Gateway, por lo que las instancias EC2 requieren estar en subredes públicas para descargar actualizaciones].
* **Mejoras Futuras:** Implementar Amazon CloudFront (CDN) para acelerar la entrega de contenido estático desde S3 a nivel global y agregar un Web Application Firewall (WAF) para mitigar ataques.
