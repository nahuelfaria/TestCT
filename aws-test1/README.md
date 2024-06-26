### Explicacion Teórica del desarrollo del diagrama de red (test1) ###

## Elementos del diagrama de red ##

- CloudFront: Distribucion de contenido global (CDN) para el frontend (js)
- Aplication Load Balancer (ALB): distribucion de tráfico al frontend
- Amazon EC2: instancias para el frontend (js)
- Amazon RDS (Relational Database Service): Base de datos relacional (mysql, postgresql, etc)
- Amazon DynamoDB: Base de datos no relacional
- Amason S3 (Simple Store Service): Almacenamiento de variables de entorno y otros archivos estáticos
- Amazon VPC (Virtual Private Cloud): Red privada virtual para aislar recursos
- Amazon Route 53: Servicio de DNS para la gestion de dominios
- Microservicios externos: Representados como servicios externos a los que se accede a través de la red
- AWS Secret Manager: Almacenamiento seguro de credenciales para acceder a los microservicios externos


# Frontend: 

1) CloudFront: Actua como CDN, almacenamiento en cache del contenido estatico (JS, CSS, imagenes) en ubicaciones perimetrales globales. Esto reduce la latenia y mejora la experiencia del usuario.
2) Application Load Balancer: Distribuye el trafico entrante entre varias instancias EC2 del frontend, garantizando alta disponibilidad y escalabilidad continua.
3) Amazon EC2: Aloja la aplicacion frontend desarrollada en JavaScript, se pueden agregar o eliminar instancias segun la demanda.
4) Amazon S3: Almacena variables de entorno de forma segura y centralizada, lo que facilita la gestion y la actualizacion misma de la configuracion.



# Backend:

1) Amazon RDS: Proporciona una base de datos relacional gestionada para almacenar datos estructurados de la aplicacion. Se elije el motor de base de datos adecuado (MySQL, PostgreSQL, etc) Segun los requisitos.
2) Amazon DynamoDB: Base de datos NOsql altamente escalable y de alto rendimiento para almacenar datos no estructurados o semiestructurados.
3) Microservicios externos: La aplicacion Backend interactua con dos microservicios externos a traves de la red. Estos microservicios pueden proporcionar funcionalidades especificas como procesamiento de pagos, envio de notificaciones, etc.
4) AWS Secrets: Almacena de forma segura las credenciales (claves de API, tokens, etc) necesarias para acceder a los microservicios externos, evitando la exposicion de la informacion sensible en el codigo.


- ALTA DISPONIBILIDAD (HA): 
* Multiples zonas de disponibilidad (az): Los recursos clave (ALB, EC2, RDS) se despliegan en varias AZ para garantizar que la aplicacion siga funcionando incluso si una AZ falla.
* Auto Scaling: Se configura el auto scalling para el frontend (EC2) y el backend (RDS) para ajustar automaticamente la capacidad segun la demanda, asegurando un rendimiento optimo.

- CONSIDERACIONES ADICIONALES E IMPORTANTES:
* Seguridad: Se pueden implementar medidas de seguridad como grupos de seguridad (AWS WAF, Web Application Firewall) y cifrado de datos en reposo y en reposo y en transito.
* Monitorizacion: Tambien se podrian utilizar servicios como Amazon CloudWatch para supervisar el rendimiento y la salud de la aplicacion, detectando y solucionando problemas de forma proactiva