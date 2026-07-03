# Justificación de la Arquitectura Cloud - Comercial Nova

Se seleccionó una arquitectura desacoplada de 3 capas distribuidas en modalidad Multi-AZ (Zonas de Disponibilidad us-east-1a y us-east-1b) para eliminar puntos únicos de fallo (SPOF):
1. **Capa de Balanceo (Pública):** Un Application Load Balancer (ALB) expone un DNS único a Internet, distribuyendo las peticiones concurrentes de los usuarios y aislando las instancias de cómputo directas.
2. **Capa de Cómputo (Aplicación):** Dos instancias EC2 con Ubuntu Server ejecutan de forma independiente el stack Apache/PHP, permitiendo el escalamiento horizontal.
3. **Capa de Datos (Privada):** Amazon RDS bajo el motor MySQL se aloja en subredes privadas dedicadas, delegando a AWS la alta disponibilidad del almacenamiento, parches automáticos y backups de seguridad.
