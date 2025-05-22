**Descripción general del sistema:**

El sistema de “Gestión de Turnos Médicos” permite a pacientes, médicos y administradores interactuar de manera organizada para la programación, confirmación y administración de turnos médicos. Además, integra servicios externos para pagos y agendamiento, ofreciendo funcionalidades clave como recordatorios, visualización de historial médico, procesamiento de pagos, sincronización de agendas, y gestión de usuarios y reportes. Su arquitectura orientada a servicios, basada en REST y una estructura multicapa, permite escalabilidad, seguridad y mantenimiento eficiente.
##
Imagen:
![caso uso (2)](https://github.com/user-attachments/assets/f99b71c5-d3ed-4ac5-832d-94e033def7b0)


**Descripción y justificación de relaciones:**

•	Actores principales:

o	Paciente: Puede registrarse, agendar turnos, cancelar turnos, solicitar recordatorios, consultar historial y realizar pagos.

o	Médico: Gestiona su agenda, registra y confirma atenciones.

o	Administrador: Administra usuarios, médicos y genera reportes.

•	*Relaciones:*

o	<<include>>: Indica funciones obligatorias dentro de otra (e.g., "Agendar Turno" incluye "Validar Disponibilidad").

o	<<extend>>: Representa funcionalidades opcionales o extendidas según contexto (e.g., "Consultar Turnos" puede extenderse con "Cancelar Turno").

o	Interacción con Sistemas Externos se realiza para sincronizar agendas y procesar pagos, extendiendo así la funcionalidad del sistema central sin recargarlo internamente.
##

**Diagrama de clases**
**Imagen:**
![diagrama clases](https://github.com/user-attachments/assets/0e1e9c70-77fd-494c-8538-3e6ffb1d22c8)


Justificación profunda de patrones utilizados:

•	Patrón Adapter:

o	Usado en clases como AdaptadorPasarelaPago y AdaptadorNotificaciones para desacoplar la lógica interna del sistema de los servicios externos (pagos, notificaciones por SMS/Email).

o	Facilita la integración con múltiples proveedores mediante una interfaz común.

•	Patrón Singleton:

o	ConfiguracionSistema y el gestor de configuración en la arquitectura aseguran una única instancia global que centraliza parámetros críticos, evitando inconsistencias.

•	Patrón Bridge + Prototype (Notificación):

o	Permite flexibilidad para enviar notificaciones usando distintos medios, desacoplando el canal (Email, SMS) de la lógica de negocio. Además, facilita la clonación de objetos de notificación personalizados.

•	Asociaciones de dominio:

o	Un Paciente puede tener múltiples Turnos.

o	Un Médico tiene una agenda de horarios y atiende turnos.

o	Las entidades están claramente modeladas para reflejar la lógica del dominio: pagos, usuarios, horarios, y estado de los turnos.
##

**Diagrama de implementación**
Imagen:
![despliegue](https://github.com/user-attachments/assets/54c9001c-d73d-487d-b66b-499a826aca93)


Decisiones técnicas clave:

•	Arquitectura en capas (layered architecture):
o	Separación clara entre presentación (cliente), lógica de negocio (API Gestión de Turnos), y datos (servidor de base de datos).
o	Mejora mantenibilidad, reutilización y escalabilidad.
•	Comunicación RESTful:
o	Permite integración con frontend web, apps móviles y servicios externos como pasarelas de pago.
•	Uso de Nginx en el frontend:
o	Mejora el rendimiento y la seguridad al servir contenido estático y redirigir peticiones API.
•	Base de datos PostgreSQL:
o	Motor robusto y escalable que almacena todos los datos del sistema, estructurados según el esquema “Tunomático”.
•	Adaptadores y API externa:
o	Facilitan el desacoplamiento con terceros (pagos, notificaciones), permitiendo mayor flexibilidad y modularidad.

##
**Reflexiones finales del modelado**

Este sistema presenta un modelado estructurado, destacándose por:

•	Una separación de responsabilidades clara en los tres niveles: presentación, lógica y datos.

•	El uso de patrones de diseño adecuados, que mejoran la flexibilidad, mantenibilidad y extensibilidad del sistema.

•	La integración con servicios externos está diseñada de manera desacoplada, lo que facilita el cambio de proveedores sin afectar la lógica interna.

•Se consideraron aspectos importantes como la notificación a pacientes, la gestión del historial médico y la seguridad de los pagos.


