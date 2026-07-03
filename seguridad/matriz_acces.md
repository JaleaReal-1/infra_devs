# Matriz de Accesos y Endurecimiento de Seguridad (Hardening)

| Recurso / Security Group | Puerto | Origen Permitido | Propósito |
| :--- | :--- | :--- | :--- |
| **SG-LoadBalancer** | 80 / 443 | `0.0.0.0/0` | Tráfico público de usuarios |
| **SG-Web-WordPress** | 80 (HTTP) | `SG-LoadBalancer` | Filtra el tráfico para que pase solo por el ALB |
| **SG-Web-WordPress** | 22 (SSH) | IP del Administrador | Acceso seguro para mantenimiento de la EC2 |
| **SG-Database-RDS** | 3306 (MySQL) | `SG-Web-WordPress` | Aislamiento absoluto de la capa de datos |

* **Cifrado en Reposo:** Activado por defecto en la capa de almacenamiento de RDS (AES-256) y mediante versionado y políticas restrictivas en el bucket de Amazon S3.
