# Estrategia de Optimización de Costos Financieros

1. **Instance Scheduler:** Configurar ventanas automáticas de apagado para instancias EC2 de desarrollo y pruebas en horarios no laborales (reducción proyectada del 30% en costos de cómputo).
2. **Lifecycle Policies en S3:** Mover recursos multimedia heredados con más de 90 días sin accesos hacia la capa *S3 Standard-Infrequent Access (IA)*.
3. **Rightsizing Continuo:** Utilizar las métricas reales de CloudWatch para degradar o migrar componentes a familias de instancias de última generación con mejor rendimiento por dólar invertido.
