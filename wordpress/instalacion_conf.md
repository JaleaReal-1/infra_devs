# Proceso de Instalación y Configuración del CMS

La instalación en la instancia EC2 base se ejecutó mediante los siguientes bloques de comandos automatizados:
1. Actualización e instalación del stack LAMP: `sudo apt update -y && sudo apt install apache2 php libapache2-mod-php php-mysql mysql-client unzip -y`
2. Descarga y despliegue del core: `wget https://wordpress.org/latest.zip && unzip latest.zip && sudo cp -r wordpress/* /var/www/html/`
3. Endurecimiento base de permisos: `sudo chown -R www-data:www-data /var/www/html/ && sudo chmod -R 755 /var/www/html`
4. Ajuste de conectividad del archivo `wp-config.php` apuntando las variables `DB_HOST` al Endpoint de la instancia RDS de producción.
