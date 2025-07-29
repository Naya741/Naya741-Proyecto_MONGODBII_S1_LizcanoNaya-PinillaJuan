## Sistema Hospitalario MongoDB 🏥


## Introducción 
Este documento servirá como una guía detallada del proceso completo de diseño, estructuración e implementación de un sistema de base de datos que permita gestionar de manera eficiente todas las operaciones relacionadas con la administración de un sistema hospitalario . El objetivo principal es gestionar eficazmente la gestión de los hospitales, pacientes, médicos, tratamientos, medicamentos, visitas médicas, historiales clínicos, áreas especializadas y personal administrativo.
Inicialmente, se analizará el caso de estudio junto con sus requerimientos específicos. A partir de esta investigación, se procederá a desarrollar un modelo conceptual detallado donde se identificarán las entidades principales, sus atributos y las relaciones entre ellas. Este paso determina las bases para comprender la estructura esencial de la gestión de los hospitales de Bucaramanga.
Después de realizar el modelo conceptual, se realizará la conversión de este modelo dicho al modelo lógico. El modelo lógico  ofrece una representación más precisa de cómo se organizará la información, facilitando una comprensión clara de la base de datos en desarrollo. Se aplicará el proceso de Normalización hasta la tercera forma normal (3FN) para optimizar la organización de los datos, reduciendo redundancias y eliminando dependencias transitivas. 
Posteriormente, se llevará a cabo la conversión del modelo lógico al modelo físico, el cual define la implementación real de entidades, atributos y relaciones, incorporando detalles técnicos como los tipos de datos adecuados para cada elemento. 
Para mejorar la comprensión del sistema, se incluirá un diagrama UML que visualice de manera gráfica y concisa la estructura de la base de datos y sus relaciones. 
Finalmente, se detallarán algunos procedimientos, funciones, consultas, funciones y acceso total, la funcionalidad del sistema de información desarrollado, asegurando así su eficiencia y utilidad para la unidad de sistema hospitalario. 
Con estos pasos y elementos, se garantiza una guía completa y efectiva para el diseño y desarrollo de la base de datos necesaria para la gestión eficiente de los hospitales de Bucaramanga y su área metropolitana.

## Caso de Estudio 
El sistema hospitalario de Bucaramanga nos ha pedido crear un diseño inicial de un Software que permita manejar los datos e información que se generan sobre los hospitales de Bucaramanga gestionados por cada municipio, por lo que comenzamos estructurando los requerimientos dados: 
Estructura del sistema
Un hospital puede tener múltiples áreas especializadas como: Cardiología, Neurología y más especialidades. 
2. Cada hospital tiene un director general, pero un director puede supervisar varios hospitales. 
3. Cada hospital tiene un conjunto de médicos, enfermeras y personal administrativo. 
4. Los hospitales deben contar con un historial detallado de pacientes y tratamientos realizados. 

Pacientes

5. Los pacientes se identifican por su número de historia clínica, nombre, dirección, teléfono correo electrónico y seguros médicos. 
6. Los historiales médicos incluyen diagnósticos, tratamientos realizados y resultados obtenidos. 

Médicos y personal 

7. Los médicos se identifican por su número de colegiatura, nombre, especialidad, teléfono, correo electrónico y salario. 

8. Se definen los siguientes tipos de personal.

001: Director General: Gestión general del hospital.

002: Médico Especialista: Atiende pacientes y realiza diagnósticos.

003: Enfermero/a: Asiste a médicos y cuida los pacientes.

004: Personal Administrativo: Gestión de recursos de logística.

005: Personal de mantenimiento: Mantenimiento y limpieza de las instalaciones.

Tratamientos y Medicamentos:

9. Los tratamientos se identifican por su nombre, descripción, área médica relacionada y costo. 
10. Los medicamentos se almacenan por nombre, fabricante, tipo y disponibilidad en inventario(stock).

Visitas Médicas:

11. Las visitas médicas se registran con fecha, hora, médico asignado, paciente atendido ydiagnóstico.

12. Los pacientes pueden tener múltiples visitas médicas a lo largo del tiempo.


Con base en la información anterior, se procederá a crear una base de datos en MONGODB y a la misma vez con funcionalidades de MYSQL esta para agrupar y relacionar los datos de los parques naturales ubicados en cada departamento, así como la información del personal y de los visitantes.

## Instalación General

Los archivos relacionados con la BBDD del Ministerio del Medio Ambiente, se encuentran en la plataforma GitHub, estos archivos se encuentran en formato json y se dividen en 4 partes: 

❖ ddl.json : Creación de la base de datos con tablas y relaciones. 

❖ dml.json: Inserciones de datos. 

❖ dql select.json : Consultas en MONGODB enfocadas en: Estado de los hospitales, inventarios de medicamentos, gestión de visitas médicas etc.

 ❖ dql funciones.json: Aquí  se gestionan las funciones en JavaScript simuladas para implementarlas como consultas reutilizables en MONGODB, se consulta cálculo de inventarios, generación de reportes de visitas médicas y obtención de estadísticas de tratamientos realizados . 

## Planificación 
Ejecución:

Una vez se analizó la información requerida por el sistema hospitalario de Bucaramanga, se inició la creación del modelo conceptual. Este modelo proporciona una descripción de alto nivel de las necesidades de información que están detrás del diseño de una base de datos. Representa los conceptos principales de la base de datos y las relaciones entre ellos. 
Construcción del Modelo Conceptual 
Se diseñó el modelo conceptual identificando cada una de las entidades, sus atributos y las relaciones entre ellas. Este modelo conceptual proporciona una visión clara y estructurada de cómo se organizan y conectan los diferentes elementos de la base de datos. 
A continuación veremos cada una de las entidades y atributos por todos los hospitales:

## Descripción 

Las Entidades y Atributos 
1. Hospital:

❖ id hospital: id único de entidad. 

❖ Nombre: nombre del hospital.

❖ Municipio: Municipio de Bucaramanga donde se encuentre cada hospital.

❖ Dirección: Dirección del hospital.


2. Director: 

❖ id_director: id único de directores. 

❖ Nombre_completo: Nombre completo del director.

❖ Documento Documento del director. 

❖ Especialidad: Especialidad del director. 

❖ Correo: Correo del director.

❖ Teléfono: Teléfono del director.

3. Área Médica: 

❖ id_area: id único del área médica.

❖ Nombre: nombre del área médica como: 
Cardiología, Neurología etc. 

❖ id_hospital : Id de cada hospital para saber en qué hospital se encuentra la especialidad o el área médica requerida. 

4. Personal_Medico: 

❖ id_personal: id del personal médico de cada hospital. 
❖ Nombre completo: nombre de cada persona que haga parte del personal médico. 

❖Rol: Rol de cada persona como Médico, Enfermero, Administrativo, Mantenimiento.

❖Especialidad: la especialidad es solo para los médicos

❖id_hospital: Id de cada hospital para saber en qué hospital se encuentran el personal. 


5. Paciente: 

❖ id_paciente : id único para cada paciente. 
❖ Nombre completo: nombre completo de cada paciente. 

❖ Documento: documento de identificación de cada paciente. 

❖ Fecha_nacimiento: fecha de nacimiento de cada paciente.

❖ Sexo: sexo femenino o masculino de cada paciente.

❖ Correo: correo electrónico de cada paciente para que obtenga información sobre lo que desee.

❖ Teléfono: teléfono ya sea celular o fijo de cada paciente para poder comunicarse con el paciente.

6. Visita:

❖ id_visita: id único de visita. 

❖ id_paciente: id del paciente ya que es único para cada paciente. 

❖ id_hospital: id del hospital para saber a cuál hospital se dirigió el paciente.
❖ Fecha_visita: fecha en la cual visitó el hospital.

❖ Motivo: motivo de visita al hospital (enfermedad, consultas etc).

❖ Diagnostico: diagnostico dado a cada paciente para conocer su estado de salud.

❖ id_área: id area para saber a cuál área del hospital se dirige o se dirigió el paciente.

7. Medicamento: 

❖ id_medicamento: id único de medicamento. 

❖ Nombre: nombre del medicamento. 

❖ Fabricante: Fabricante del medicamento. 

❖ Tipo: Tipo de medicamento. 

❖ Stock_actual: stock para conocer cuántas cantidades de medicamento hay actualmente en cada hospital. 

❖ id_hospital: id hospital para conocer en qué hospital se encuentra cada medicamento y cuanta cantidad. 

8. Tratamiento: 

❖ id_tratamiento: id único para cada tratamiento. 

❖ Nombre: nombre de cada tratamiento.

❖ Descripción: descripción de cada tratamiento.

❖ Costo: costos y precios en general para cada tratamiento.

❖id_área: id área para conocer en qué hospital se realice algún tratamiento.

❖ id_visita: id visita para conocer todas las especificaciones que se realiza en id visita.

9. Medicamento_tratamiento: 

❖ id: id único del medicamento y tratamiento.

❖ id_ tratamiento: id tratamiento para conocer el tratamiento a realizar. 

❖ id_medicamento: id medicamento para conocer el medicamento a usar. 

❖ dosis: dosis para saber cómo administrar medicamento dependiendo del tratamiento. 

❖ Frecuencia: frecuencia de la dosis de medicamento. 

## Relaciones y Cardinalidades 
Se realizó las relaciones y cardinalidades respectivas del modelo conceptual con sus entidades para tener mejor visualización de la base de datos: 
1. Director - Hospital: 

❖ Relación: "Administra", Un director puede administrar varios hospitales y cada hospital es administrado por un solo director.

❖ Cardinalidad: 1-N (uno a muchos).

2. Hospital - Área médica: 

❖ Relación: “Tiene”, un hospital tiene múltiples áreas médicas, y casa área médica pertenece a un solo hospital. 

❖ Cardinalidad: 1-N (uno a muchos). 

3. Hospital - Personal:

❖ Relación: "Cuenta con", Un hospital cuenta con muchos miembros de personal (médico, enfermeros, administrativo y  mantenimiento), y cada miembro trabaja en un solo hospital 

❖ Cardinalidad: 1-N (uno a muchos). 

4. Área Médica - Tratamiento: 

❖ Relación: “Aplica”, Un área médica aplica muchos tratamientos, y cada tratamiento está relacionado con un solo área médica. 

❖ Cardinalidad: 1-N (uno a muchos). 

5. Hospital - Medicamento: 

❖ Relación: “Administra”, Un hospital administra varios medicamentos, y cada medicamento está asignado a un solo hospital.

❖ Cardinalidad: 1-N (uno a muchos). 

6. Paciente - Visita: 

❖ Relación: “Realiza”, Un paciente puede tener muchas visitas, pero cada visita pertenece a un solo paciente. 

❖ Cardinalidad: 1-N (uno a muchos). 


7. Hospital - Visita: 

❖ Relación: “Atiende”, Un hospital atiende muchas visitas, y cada visita se realiza en un solo hospital. 

❖ Cardinalidad: 1-N (uno a muchos). 


8. Visita -  Tratamiento: 

❖ Relación: “Genera”, Una visita puede generar múltiples tratamientos, y cada tratamiento 
corresponde a una sola visita. 
❖ Cardinalidad: 1-N (uno a muchos). 


9. Tratamiento - Medicamento: 

❖ Relación: “Usa”, Un tratamiento puede requerir varios medicamentos, y un medicamento puede ser usado en muchos tratamientos. 

❖ Cardinalidad: N-M (muchos a muchos). 
Se implementa mediante la entidad intermedia “Medicamento_Tratamiento”


10. Personal_Rol Específico: 

❖ Relación: “Corresponde”, Un miembro de personal puede estar asociado a un único rol específico(médico, enfermero, administrativo, mantenimiento), y cada rol específico corresponde a un personal.

❖ Cardinalidad: 1-1 (uno a uno). 
## Grafica:

```mermaid 
graph TD
    %% Entidades principales
    Director[Director]
    Hospital[Hospital]
    Personal[Personal]
    AreaMedica[Área Médica]
    Medicamento[Medicamento]
    Paciente[Paciente]
    Visita[Visita]
    Diagnostico[Diagnóstico]
    Tratamiento[Tratamiento]

    %% Atributos de Director
    DNombre((nombre_completo))
    DDoc((documento))
    DEsp((especialidad))
    DCorreo((correo))
    DTel((telefono))

    %% Atributos de Hospital
    HNombre((nombre))
    HMun((municipio))
    HDir((direccion))

    %% Atributos de Personal
    PNombre((nombre_completo))
    PEsp((especialidad))
    PRol((rol))

    %% Atributos de Área Médica
    ANombre((nombre))

    %% Atributos de Medicamento
    MNombre((nombre))
    MFab((fabricante))
    MTipo((tipo))
    MStock((stock_actual))

    %% Atributos de Paciente
    PacNombre((nombre_completo))
    PacDoc((documento))
    PacFecha((fecha_nacimiento))
    PacSexo((sexo))
    PacTel((telefono))
    PacCorreo((correo))

    %% Atributos de Visita
    VFecha((fecha_visita))
    VHospital((es_hospital))

    %% Atributos de Diagnóstico
    DiagMotivo((motivo))

    %% Atributos de Tratamiento
    TFecha((fecha_inicio))
    TDesc((descripcion))

    %% Conexiones de atributos con entidades
    Director --> DNombre
    Director --> DDoc
    Director --> DEsp
    Director --> DCorreo
    Director --> DTel

    Hospital --> HNombre
    Hospital --> HMun
    Hospital --> HDir

    Personal --> PNombre
    Personal --> PEsp
    Personal --> PRol

    AreaMedica --> ANombre

    Medicamento --> MNombre
    Medicamento --> MFab
    Medicamento --> MTipo
    Medicamento --> MStock

    Paciente --> PacNombre
    Paciente --> PacDoc
    Paciente --> PacFecha
    Paciente --> PacSexo
    Paciente --> PacTel
    Paciente --> PacCorreo

    Visita --> VFecha
    Visita --> VHospital

    Diagnostico --> DiagMotivo

    Tratamiento --> TFecha
    Tratamiento --> TDesc

    %% Relaciones entre entidades
    Director -->|administra| Hospital
    Hospital -->|cuenta con| Personal
    Hospital -->|tiene| AreaMedica
    Hospital -->|administra| Medicamento
    Personal -->|trabaja en| AreaMedica
    AreaMedica -->|atiende| Visita
    Paciente -->|realiza| Visita
    Paciente -->|recibe| Diagnostico
    Visita -->|genera| Diagnostico
    Medicamento -->|se usa en| Tratamiento
    Tratamiento -->|se aplica en| Hospital
    Diagnostico -->|requiere| Tratamiento
```



## Construcción del Modelo Lógico 
Se ha diseñado el modelo lógico teniendo en cuenta el modelo conceptual, incorporando detalles más específicos como las características de cada atributo, incluidas las claves primarias, foráneas y las relaciones de cardinalidad. 

## Descripción 

Las Entidades y Atributos 
1. Hospital :

❖ id_hospital: INT AUTO_INCREMENT PRIMARY KEY. 

❖ nombre: VARCHAR(100) NOT NULL. 

❖ ciudad: VARCHAR(100) NOT NULL.

❖ dirección: VARCHAR(200) NOT NULL.

❖ id_director: VARCHAR(100) INT NOT NULL FOREIGN KEY.


2. Director: 

❖ id_director: INT AUTO_INCREMENT PRIMARY KEY.

❖ nombre: VARCHAR (100) NOT NULL.

❖ documento: VARCHAR(20) NOT NULL. 

❖ correo VARCHAR(100) NOT NULL. 

❖ telefono: VARCHAR(20).

3. Área Médica : 

❖ id_area: INT AUTO_INCREMENT PRIMARY KEY.

❖ nombre: VARCHAR(100) NOT NULL. 

❖ id_hospital: INT NOT  NULL FOREIGN KEY.

4. Personal : 

❖ id_personal: INT PRIMARY KEY, FOREIGN KEY. 

❖ id_hospital: INT NOT NULL FOREIGN KEY. 

❖ Nombre: VARCHAR(100) NOT NULL.

❖ Documento: VARCHAR(20)  UNIQUE NOT NULL.

❖ Rol: VARCHAR(100)  ENUM (‘Médico’, ‘Enfermero’, ‘Administrativo’, ‘Mantenimiento’) NOT NULL.

❖ Especialidad: VARCHAR(100) 

❖ Correo: VARCHAR(100) 

❖ Telefono: VARCHAR(20) 

5. Paciente: 

❖ id_paciente: INT AUTO_INCREMENT PRIMARY KEY.

❖ nombre: VARCHAR (100) NOT NULL. 

❖ documento: VARCHAR(20)  UNIQUE NOT NULL. 

❖ fecha_nacimiento: DATE NOT NULL. 

❖ sexo: varchar ENUM (‘M’, ‘F’) NOT NULL.

❖ correo: varchar(100).

❖ telefono: VARCHAR (20).

6. Visita : 

❖ id_visita INT AUTO_INCREMENT PRIMARY KEY.

❖ id_paciente: INT NOT NULL FOREIGN KEY. 

❖  id_hospital: INT NOT NULL FOREIGN KEY. 

❖  id_area: INT NOT NULL FOREIGN KEY. 

❖ fecha_visita: DATE NOT NULL. 

❖ motivo: VARCHAR (100) NOT NULL. 

❖ diagnóstico: TEXT.

7. Tratamiento  : 

❖ id_tratamiento: INT AUTO_INCREMENT PRIMARY KEY. 

❖ id_visita: INT NOT NULL FOREIGN KEY.

❖ id_area: INT(20) INT NOT NULL FOREIGN KEY. 

❖ nombre: VARCHAR(100) NOT NULL. 

❖ descripcion: TEXT. 

❖ costo: DECIMAL (10,2) NOT NULL.


8. Medicamento : 

❖ id_medicamento: INT AUTO_INCREMENT PRIMARY KEY. 

❖ id_hospital: INT NOT NULL FOREIGN KEY.

❖ nombre: VARCHAR (100) NOT NULL.

❖ fabricante: VARCHAR (100) NOT NULL.

❖ tipo: VARCHAR (50) NOT NULL. 

❖ stock_actual: INT (10) NOT NULL. 


9. Medicamento_tratamiento : 

❖ id_tratamiento: INT AUTO_INCREMENT PRIMARY KEY. 

❖ id_medicamento: INT NOT NULL FOREIGN KEY.

❖ dosis:  VARCHAR (50) NOT NULL. 

❖ frecuencia: VARCHAR(100) NOT NULL. 

❖ marca_vehiculo: VARCHAR(50) NOT NULL. 

## Relaciones y Cardinalidades 
Se realizó las relaciones y cardinalidades respectivas del modelo lógico con sus entidades para tener mejor visualización de la base de datos: 
1. Director- Hospital: 

❖ Un director administra varios hospitales, pero un hospital solo tiene un director

❖Cardinalidad: 1-N (uno a muchos).

2. Hospital - Area Medica: 

❖Un hospital tiene varias areas, y cada area medica pertenece a un solo hospital.

❖ Cardinalidad: 1-N (uno a muchos).

3. Hospital- Personal: 

❖ Un hospital cuenta con muchos trabajadores, y cada uno pertenece a un solo hospital.

❖ Cardinalidad: 1-N (uno a muchos).

4. Hospital - Medicamento: 

❖Un hospital almacena múltiples medicamentos, y cada medicamento está registrado en un hospital. 

❖ Cardinalidad: 1-N (uno a muchos).

5. Paciente - Visita: 

❖Un paciente puede tener muchas visitas, y cada visita pertenece a un solo paciente.

❖ Cardinalidad: 1-N (uno a muchos).

6. Hospital - Visita: 

❖Un hospital atiende muchas visitas, cada una realizada en un solo hospital.

❖ Cardinalidad: 1-N (uno a muchos).

7. Área Médica - Visita: 

❖ Una visita se registra bajo un área médica especifica, y un área puede tener muchas visitas. 

❖ Cardinalidad: 1-N (uno a muchos).

8. Visita - Tratamiento: 
❖ Una visita puede generar varios tratamientos, pero un tratamiento pertenece a una sola visita. 

❖ Cardinalidad: 1-N (uno a muchos).

9. Área Médica - Tratamiento :

❖ Cada tratamiento se asocia a un área médica, y un área médica puede aplicar varios tratamientos. 

❖ Cardinalidad: 1-N (uno a muchos).

10. Tratamiento - Medicamento:

❖Un tratamiento puede usar muchos medicamentos, y un medicamento puede ser utilizado en muchos tratamientos.

❖ Cardinalidad: N- M ( muchos a muchos). 

❖ Entidad intermedia: medicamento_tratamiento.

## Gráfica

```mermaid     
erDiagram
    MEDICAMENTO {
        int id_medicamento PK
        int id_hospital FK
        string nombre
        string fabricante
        string tipo
        int stock_actual
    }
    
    HOSPITAL {
        int id_hospital PK
        int id_director FK
        string nombre
        string ciudad
        string direccion
    }
    
    DIRECTOR {
        int id_director PK
        string nombre
        string documento
        string correo
        string telefono
    }
    
    AREA_MEDICA {
        int id_area PK
        int id_hospital FK
        string nombre
    }
    
    PERSONAL {
        int id_personal PK
        int id_hospital FK
        string nombre
        string documento
        string rol
        string especialidad
        string correo
        string telefono
    }
    
    VISITA {
        int id_visita PK
        int id_paciente FK
        int id_hospital FK
        int id_area FK
        date fecha_visita
        string motivo
        string diagnostico
    }
    
    PACIENTE {
        int id_paciente PK
        string nombre
        string documento
        date fecha_nacimiento
        string sexo
        string correo
        string telefono
    }
    
    TRATAMIENTO {
        int id_tratamiento PK
        int id_visita FK
        int id_area FK
        string nombre
        string descripcion
        decimal costo
    }

    %% Relaciones con cardinalidades
    DIRECTOR ||--|| HOSPITAL : "administra"
    HOSPITAL ||--o{ MEDICAMENTO : "gestiona"
    HOSPITAL ||--o{ AREA_MEDICA : "contiene"
    HOSPITAL ||--o{ PERSONAL : "emplea"
    HOSPITAL ||--o{ VISITA : "atiende"
    AREA_MEDICA ||--o{ VISITA : "realiza"
    AREA_MEDICA ||--o{ TRATAMIENTO : "aplica"
    PACIENTE ||--o{ VISITA : "programa"
    VISITA ||--o{ TRATAMIENTO : "genera"
```

## Normalización del Modelo Lógico 

Se realizó el proceso de la normalización de las tablas anteriormente visualizadas para organizar los datos de manera más eficiente,minimizando redundancias y dependencias transitivas en la base de datos en desarrollo. 

## Primera Forma Normal (1FN) 

Una tabla está en 1FN si cumple con los siguientes criterios: 

❖ Todos los atributos contienen valores atómicos (indivisibles). 

❖ No debe haber grupos repetitivos de columnas.

❖ Cada columna debe contener un solo valor en cada fila. 

## Descripción 
La primera forma normal, es el primer nivel de normalización en el diseño de la base de datos que se aplicará a las tablas de la base de datos para garantizar la organización de los datos de manera que evite redundancias y asegure la consistencia de la información. 

## Descripción Técnica 

1. Hospital : 

❖ Se encuentra en 1FN, ya que cuenta con una clave primaria única y cada columna tiene valores atómicos.

2. Director : 

❖ Se encuentra en 1FN, cumple con unicidad en su clave primaria y los atrbutosno son multivaluados.

3. Area_medica : 

❖ Se encuentra en 1FN,todos los valores son indivisibles. 

4. Personal: 

❖ Se encuentra en 1FN, sus atributos son únicos por fila y no hay columnas multivaluadas. 

5. Paciente:

❖ Se encuentra en 1FN, los datos principales están bien estructuradas. 

6. Visita: 

❖ Se encuentra en 1FN, cada visita representa un evento único y los campos son atómicos. 

7. Tratamiento: 

❖ Se encuentra en 1FN, todos los valores son unicos por fila.

8. Medicamento: 
❖ Se encuentra en 1FN, sin atributos repetitivos o compuestos.

9. Medicamento_tratamiento: 

❖ Se encuentra en 1FN, representa una relacion M:N, bien estructurada con claves compuestas. 

9. Factura: 
❖ Se encuentra en 1FN, ya que cada factura tiene una clave primaria única (id_factura) y los atributos son atómicos, sin grupos repetitivos.

## Gráfica

```mermaid 
erDiagram
AreaMedica {
int id_area PK
string nombre
int id_hospital FK
}
Director {
int id_director PK
string Nombre
string Documento
string Correo
string Telefono
}

Hospital {
int id_hospital PK
string Nombre
string Ciudad
string Direccion
int id_director FK
}

Personal {
int id_personal PK
int id_hospital FK
string Nombre
string Documento
int id_rol FK
string id_especialidad
string Correo
string Telefono
}

Paciente {
int id_paciente PK
string Nombre
string Documento
date Fecha_nacimiento
string Sexo
string Correo
string Telefono
}

Visita {
int id_visita PK
int id_paciente FK
int id_hospital FK
int id_area FK
date fecha_visita
string Motivo
string Diagnostico
}

Medicamento {
int id_medicamento PK
int id_hospital FK
string Nombre
string Fabricante
int id_categoria FK
int stock_actual
}

Tratamiento {
int id_tratamiento PK
int id_visita FK
int id_area FK
string Nombre
string Descripcion
decimal Costo
}

Factura {
int id_factura PK
int id_paciente FK
date fecha_emision
decimal Total}

Hospital ||--o{ AreaMedica : "tiene"
Director ||--|| Hospital : "dirige"
Hospital ||--o{ Personal : "emplea"
Hospital ||--o{ Visita : "atiende"
Hospital ||--o{ Medicamento : "almacena"
Paciente ||--o{ Visita : "realiza"
Paciente ||--o{ Factura : "genera"
AreaMedica ||--o{ Visita : "recibe"
AreaMedica ||--o{ Tratamiento : "ofrece"
Visita ||--o{ Tratamiento : "incluye"
```

## Segunda Forma Normal (2FN) 

Una tabla está en 2FN si cumple con los siguientes criterios: 

❖ Está en 1FN. 

❖ Todos los atributos no clave (no pertenecientes a una clave primaria compuesta) dependen completamente de la clave primaria. 
## Descripción 
La segunda forma normal, es el segundo nivel de normalización en el diseño de la base de datos que se aplicará a las tablas de una base de datos que ya cumplen con la primera forma normal y lleva a cabo la eliminación de dependencias parciales dentro de una tabla. 

## Descripción Técnica 

1. Hospital :

❖ Esta en 2FN ya que todos los atributos dependen únicamente del id_hospital. 

2. Director: 

❖ Se encuentra en 2FN, sin claves compuestas ni dependencias parciales. 

3. Area_medica : 

❖ Se encuentra en 2FN, ya que depende totalmente de id_area. 
4. Personal: 

❖ Se encuentra en 2FN, atributos como nombre, documento y rol dependen totalmente de id_personal. 

5. Paciente : 

❖ Se encuentra en 2FN, ya que cada columna depende completamente de su clave primaria. 

6. Visita : 

❖ Se encuentra en 2FN, ya que el diagnóstico, fecha y visita dependen de id_visita. 

7. Tratamiento :  

❖ Se encuentra en 2FN, ya que nombre, descripción, costo dependen totalmente de la clave id_tratamiento . 

8. : Medicamento:

❖ Se encuentra en 2FN, los atributos son función directa de la clave primaria. 

9. Medicamento_tratamiento : 

❖ Se encuentra en 2FN, ya que cada columna depende de la combinacion 

10. Factura: 

❖ Se encuentra en 2FN, ya que cada atributo (fecha_emision, total) depende completamente de la clave primaria y no existen claves compuestas.

11. Detalle_Factura:

❖ Se encuentra en 2FN, ya que los atributos no clave (cantidad, subtotal) dependen por completo de la clave primaria (id_detalle).

12. Rol:

❖ Se encuentra en 2FN, ya que el atributo nombre_rol depende totalmente de la clave primaria.

13. Especialidad:

❖ Se encuentra en 2FN, ya que el atributo nombre_especialidad depende solo de la clave primaria.

## Gráfica



```mermaid
erDiagram
Paciente {
        int id_paciente PK
        string Nombre
        string Documento
        date Fecha_nacimiento
        string Sexo
        string Correo
        string Telefono
    }
    
AreaMedica {
    int id_area PK
    string nombre
    int id_hospital FK
}

Visita {
    int id_visita PK
    int id_paciente FK
    int id_hospital FK
    int id_area FK
    date fecha_visita
    string Motivo
    string Diagnostico
}

Tratamiento {
    int id_tratamiento PK
    int id_visita FK
    int id_area FK
    string Nombre
    string Descripcion
    decimal Costo
}

Director {
    int id_director PK
    string Nombre
    string Documento
    string Correo
    string Telefono
}

Hospital {
    int id_hospital PK
    string Nombre
    string Ciudad
    string Direccion
    int id_director FK
}

Medicamento {
    int id_medicamento PK
    int id_hospital FK
    string Nombre
    string Fabricante
    int id_categoria FK
    int stock_actual
}

Rol {
    int id_rol PK
    string Nombre_rol
}

Especialidad {
    int id_especialidad PK
    string Nombre_especialidad
}

Personal {
    int id_personal PK
    int id_hospital FK
    string Nombre
    string Documento
    int id_rol FK
    int id_especialidad FK
    string Correo
    string Telefono
}

Medicamento_tratamiento {
    int id_Medicamento_Tratamiento PK
    int id_medicamento FK
    int id_tratamiento FK
    string Dosis
    string Frecuencia
}

Factura {
    int id_factura PK
    int id_paciente FK
    date fecha_emision
    decimal Total
}

Detalle_factura {
    int id_detalle PK
    int id_factura FK
    int id_tratamiento FK
    int Cantidad
    decimal Subtotal
}

%% Relaciones principales
Paciente ||--o{ Visita : "realiza"
Paciente ||--o{ Factura : "genera"

Hospital ||--o{ AreaMedica : "tiene"
Hospital ||--o{ Visita : "atiende"
Hospital ||--o{ Medicamento : "almacena"
Hospital ||--o{ Personal : "emplea"

Director ||--|| Hospital : "dirige"

AreaMedica ||--o{ Visita : "recibe"
AreaMedica ||--o{ Tratamiento : "ofrece"

Visita ||--o{ Tratamiento : "incluye"

Rol ||--o{ Personal : "asigna"
Especialidad ||--o{ Personal : "define"

%% Relación muchos a muchos entre Medicamento y Tratamiento
Medicamento ||--o{ Medicamento_tratamiento : "incluye"
Tratamiento ||--o{ Medicamento_tratamiento : "requiere"

%% Relaciones de facturación
Factura ||--o{ Detalle_factura : "contiene"
Tratamiento ||--o{ Detalle_factura : "factura"
```
´´´

## Tercera Forma Normal (3FN) 
Una tabla está en 3NF si cumple con los siguientes criterios: 

❖ Está en 2NF. 

❖ No hay dependencias transitivas: ningún atributo no clave depende de otro atributo no clave. 

## Descripción 
La tercera forma normal, es el tercer nivel de normalización en el diseño de la base de datos que se aplicará a las tablas de una base de datos que ya cumplen con la segunda forma normal y se enfoca en la eliminación de dependencias transitivas, evitando que un atributo no clave dependa de otro no clave.

## Descripción Técnica 
1. Hospital: 

❖ Se encuentra en 3FN, ya que no existen dependencias con atributos no clave.. 

2. Director: 

❖ Se encuentra en 3FN, ya que los datos de contacto no dependen entre si.

3. Area_medica : 

❖ Se encuentra en 3FN, ya que no tiene transacciones entre atributos no clave. 

4. Personal : 

Se encuentra en 3FN, ya que rol, especialidad, correo, etc, no dependen entre si. 

5. Paciente : 

❖ Se encuentra en 3FN, no hay relaciones transitivas entre los atributos de la tabla. 

6. Visita: 

❖ Se encuentra en 3FN, motivo y diagnostico dependen solo de la visita, no de paciente o hospital . 

7. Tratamiento: 

❖ Se encuentra en 3FN, ya que no hay atributos no clave relacionados entre si. 

8. Medicamento : 

❖ Se encuentra en 3FN, ya  que todos los campos son dependientes directos de la clave.

9. Medicamento_tratamiento : 

❖ Se encuentra en 3FN, ya que la dosis y frecuencia dependen de la clave compuesta. 

10. Factura:
❖ Se encuentra en 3FN, ya que no hay dependencias transitivas entre atributos; el total y la fecha dependen solo de la clave primaria.

11. Detalle_Factura:

❖ Se encuentra en 3FN, ya que no existen dependencias transitivas; la relación con Factura y Tratamiento está normalizada mediante claves foráneas.


12. Rol:

❖ Se encuentra en 3FN, ya que no existen dependencias transitivas; todos los atributos dependen únicamente de id_especialidad.

13. Especialidad:

❖ Se encuentra en 3FN, ya que la dosis y frecuencia dependen de la clave compuesta. 

14. Categoria_Medicamento:

❖ Se encuentra en 3FN, ya que no hay dependencias transitivas; el nombre de la categoría depende únicamente de la clave primaria.


15. Historia_Tratamiento

❖ Se encuentra en 3FN, ya que no hay dependencias transitivas; las fechas y el estado dependen únicamente de la clave primaria y están normalizadas respecto al tratamiento.

## Gráfica

```mermaid
erDiagram
    Paciente {
        int id_paciente PK
        string nombre
        string documento
        date fecha_nacimiento
        string sexo
        string correo
        string telefono
    }
    
    Factura {
        int id_factura PK
        int id_paciente FK
        date fecha_emision
        decimal total
    }
    
    Detalle_factura {
        int id_detalle PK
        int id_factura FK
        int id_tratamiento FK
        int cantidad
        decimal subtotal
    }
    
    Historia_tratamiento {
        int id_historia_tratamiento PK
        int id_paciente FK
        int id_tratamiento FK
        date fecha_inicio
        date fecha_fin
    }
    
    Tratamiento {
        int id_tratamiento PK
        int id_visita FK
        int id_area FK
        string nombre
        string descripcion
        decimal costo
    }
    
    Visita {
        int id_visita PK
        int id_paciente FK
        int id_hospital FK
        int id_area FK
        date fecha_visita
        string motivo
        string diagnostico
    }
    
    AreaMedica {
        int id_area PK
        string nombre
        int id_hospital FK
    }
    
    Hospital {
        int id_hospital PK
        string nombre
        string ciudad
        string direccion
        int id_director FK
    }
    
    Director {
        int id_director PK
        string nombre
        string documento
        string correo
        string telefono
    }
    
    Personal {
        int id_personal PK
        int id_hospital FK
        string nombre
        string documento
    }
    
    Rol {
        int id_rol PK
        string nombre_rol
    }
    
    Especialidad {
        int id_especialidad PK
        string nombre_especialidad
        string correo
        string telefono
    }
    
    Medicamento {
        int id_medicamento PK
        int id_hospital FK
        string nombre
        string fabricante
        int id_categoria FK
        int stock_actual
    }
    
    Categoria_Medicamento {
        int id_categoria_medic PK
        string nombre_categoria
    }
    
    Medicamento_tratamiento {
        int id_Medicamento_Tratamiento PK
        int id_medicamento FK
        int id_tratamiento FK
        string dosis
        string frecuencia
    }

    %% Relaciones
    Paciente ||--o{ Factura : "tiene"
    Paciente ||--o{ Historia_tratamiento : "posee"
    Paciente ||--o{ Visita : "realiza"
    
    Factura ||--o{ Detalle_factura : "contiene"
    Detalle_factura }o--|| Tratamiento : "incluye"
    
    Historia_tratamiento }o--|| Tratamiento : "registra"
    
    Visita }o--|| Hospital : "se_realiza_en"
    Visita }o--|| AreaMedica : "corresponde_a"
    Visita ||--o{ Tratamiento : "genera"
    
    AreaMedica }o--|| Hospital : "pertenece_a"
    
    Hospital }o--|| Director : "dirigido_por"
    Hospital ||--o{ Personal : "emplea"
    Hospital ||--o{ Medicamento : "almacena"
    
    Personal }o--|| Rol : "tiene_rol"
    Personal }o--|| Especialidad : "tiene_especialidad"
    
    Medicamento }o--|| Categoria_Medicamento : "pertenece_a"
    Medicamento ||--o{ Medicamento_tratamiento : "usado_en"
    
    Tratamiento ||--o{ Medicamento_tratamiento : "requiere"
```

## Construcción del Modelo Físico:

Se diseñó el modelo físico considerando el modelo lógico que incluye todas las entidades, sus atributos y las relaciones entre ellas. Además, este modelo incorpora los tipos de datos de los atributos previamente definidos, los cuales fueron estructurados en tablas utilizando el lenguaje de un Sistema de Gestión de Bases en MONGODB .

## Descripción 

El modelo físico se diseñó para funcionar en MONGODB, donde se haran 100 consultas enfocadas en toda el sistema hospitalario. 
Creación de colecciones
Para crear la base de datos utilice el siguiente comando: 
create database Hospitales; 
Para utilizar cada colección use: 
use Hospitales; 
Comenzaremos creando las colecciones de cada apartado de los hospitales: 

1. Creación de la colección directores:
```js
db.createCollection("directores", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["_id", "nombre", "documento", "correo", "telefono"],
      properties: {
        _id: { bsonType: "string" },
        nombre: { bsonType: "string" },
        documento: { bsonType: "string" },
        correo: { bsonType: "string" },
        telefono: { bsonType: "string" }
      }
    }
  }
});
```

* Insertar datos a la coleccion ("directores):
```js
db.directores.insertMany([
  {
    "_id": "DIR001",
    "nombre": "Dr. Carlos Alberto Mendoza Rivera",
    "documento": "12345678",
    "correo": "carlos.mendoza@hospitales.gov.co",
    "telefono": "3001234567"
  },
  {
    "_id": "DIR002", 
    "nombre": "Dra. María Elena Rodríguez Vargas",
    "documento": "87654321",
    "correo": "maria.rodriguez@hospitales.gov.co",
    "telefono": "3007654321"
  },
  {
    "_id": "DIR003",
    "nombre": "Dr. José Antonio Vargas Herrera",
    "documento": "11223344",
    "correo": "jose.vargas@hospitales.gov.co", 
    "telefono": "3001122334"
  }
]);
```
2. Creación de la colección hospitales :
```js
db.createCollection("hospitales", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["_id", "nombre", "ciudad", "direccion", "id_director"],
      properties: {
        _id: { bsonType: "string" },
        nombre: { bsonType: "string" },
        ciudad: { bsonType: "string" },
        direccion: { bsonType: "string" },
        id_director: { bsonType: "string" }
      }
    }
  }
});
```

* Insertar datos a la coleccion ("hospitales"):
```js
db.hospitales.insertMany([ {
      "id_hospital": "HOS001",
      "nombre": "Hospital Universitario de Santander (HUS)",
      "ciudad": "Bucaramanga",
      "direccion": "Carrera 33 #28-126",
      "id_director": "DIR001"
    },
    {
      "id_hospital": "HOS002", 
      "nombre": "Hospital Universitario Los Comuneros",
      "ciudad": "Bucaramanga",
      "direccion": "Autopista Floridablanca Km 1",
      "id_director": "DIR001"
    },
    {
      "id_hospital": "HOS003",
      "nombre": "E.S.E. Hospital San Juan de Dios de Floridablanca",
      "ciudad": "Floridablanca", 
      "direccion": "Calle 4 #11-50",
      "id_director": "DIR002"
    },
    {
      "id_hospital": "HOS004",
      "nombre": "Hospital Internacional de Colombia",
      "ciudad": "Bucaramanga",
      "direccion": "Calle 155 #23-09",
      "id_director": "DIR003"
    }
]);
```

3. Creación de la colección roles :
```js
db.createCollection("roles", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["_id", "nombre_rol"],
      properties: {
        _id: { bsonType: "string" },
        nombre_rol: { bsonType: "string" }
      }
    }
  }
});
```

* Insertar datos a la coleccion ("roles"):
```js
db.roles.insertMany([ {
      "id_hospital": "HOS001",
      "nombre": "Hospital Universitario de Santander (HUS)",
      "ciudad": "Bucaramanga",
      "direccion": "Carrera 33 #28-126",
      "id_director": "DIR001"
    },
    {
      "id_hospital": "HOS002", 
      "nombre": "Hospital Universitario Los Comuneros",
      "ciudad": "Bucaramanga",
      "direccion": "Autopista Floridablanca Km 1",
      "id_director": "DIR001"
    },
    {
      "id_hospital": "HOS003",
      "nombre": "E.S.E. Hospital San Juan de Dios de Floridablanca",
      "ciudad": "Floridablanca", 
      "direccion": "Calle 4 #11-50",
      "id_director": "DIR002"
    },
    {
      "id_hospital": "HOS004",
      "nombre": "Hospital Internacional de Colombia",
      "ciudad": "Bucaramanga",
      "direccion": "Calle 155 #23-09",
      "id_director": "DIR003"
    }
]);
```

4. Creación de la colección especialidades :
```js
db.createCollection("especialidades", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["_id", "nombre_especialidad"],
      properties: {
        _id: { bsonType: "string" },
        nombre_especialidad: { bsonType: "string" }
      }
    }
  }
});
```

* Insertar datos a la coleccion ("especialidades"):
```js
db.especialidades.insertMany([ {
      "id_especialidad": "ESP001",
      "nombre_especialidad": "Cardiología"
    },
    {
      "id_especialidad": "ESP002",
      "nombre_especialidad": "Cirugía cardiovascular"
    },
    {
      "id_especialidad": "ESP003", 
      "nombre_especialidad": "Neurología"
    },
    {
      "id_especialidad": "ESP004",
      "nombre_especialidad": "Neumología"
    },
    {
      "id_especialidad": "ESP005",
      "nombre_especialidad": "Gastroenterología"
    },
    {
      "id_especialidad": "ESP006",
      "nombre_especialidad": "Endocrinología"
    },
    {
      "id_especialidad": "ESP007",
      "nombre_especialidad": "Pediatría"
    },
    {
      "id_especialidad": "ESP008",
      "nombre_especialidad": "Reumatología"
    },
    {
      "id_especialidad": "ESP009",
      "nombre_especialidad": "Infectología"
    },
    {
      "id_especialidad": "ESP010",
      "nombre_especialidad": "Oncología clínica"
    },
    {
      "id_especialidad": "ESP011",
      "nombre_especialidad": "Dermatología"
    },
    {
      "id_especialidad": "ESP012",
      "nombre_especialidad": "Psiquiatría"
    },
    {
      "id_especialidad": "ESP013",
      "nombre_especialidad": "Otorrinolaringología"
    },
    {
      "id_especialidad": "ESP014",
      "nombre_especialidad": "Medicina Interna"
    },
    {
      "id_especialidad": "ESP015",
      "nombre_especialidad": "Medicina Familiar"
    },
    {
      "id_especialidad": "ESP016",
      "nombre_especialidad": "Nefrología"
    },
    {
      "id_especialidad": "ESP017",
      "nombre_especialidad": "Ginecología"
    },
    {
      "id_especialidad": "ESP018",
      "nombre_especialidad": "Psicología"
    },
    {
      "id_especialidad": "ESP019",
      "nombre_especialidad": "Medicina General"
    },
    {
      "id_especialidad": "ESP020",
      "nombre_especialidad": "Obstetricia"
    },
    {
      "id_especialidad": "ESP021",
      "nombre_especialidad": "Fisioterapia"
    },
    {
      "id_especialidad": "ESP022",
      "nombre_especialidad": "Terapia Respiratoria"
    },
    {
      "id_especialidad": "ESP023",
      "nombre_especialidad": "Neurocirugía"
    },
    {
      "id_especialidad": "ESP024",
      "nombre_especialidad": "Oncología quirúrgica"
    },
    {
      "id_especialidad": "ESP025",
      "nombre_especialidad": "Urología"
    },
    {
      "id_especialidad": "ESP026",
      "nombre_especialidad": "Cirugía plástica"
    },
    {
      "id_especialidad": "ESP027",
      "nombre_especialidad": "Unidad de Quemados"
    },
    {
      "id_especialidad": "ESP028",
      "nombre_especialidad": "Medicina integrativa"
    }
]);
```

5. Creación de la colección areas_medicas :
```js
db.createCollection("areas_medicas", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["_id", "nombre", "id_hospital"],
      properties: {
        _id: { bsonType: "string" },
        nombre: { bsonType: "string" },
        id_hospital: { bsonType: "string" }
      }
    }
  }
});
```

* Insertar datos a la coleccion ("areas_medicas"):
```js
db.areas_medicas.insertMany([ {
      "id_area": "AREA001",
      "nombre": "Cardiología y Cirugía cardiovascular",
      "id_hospital": "HOS001"
    },
    {
      "id_area": "AREA002",
      "nombre": "Neurología", 
      "id_hospital": "HOS001"
    },
    {
      "id_area": "AREA003",
      "nombre": "Neumología",
      "id_hospital": "HOS001"
    },
    {
      "id_area": "AREA004",
      "nombre": "Gastroenterología",
      "id_hospital": "HOS001"
    },
    {
      "id_area": "AREA005",
      "nombre": "Endocrinología",
      "id_hospital": "HOS001"
    },
    {
      "id_area": "AREA006",
      "nombre": "Pediatría",
      "id_hospital": "HOS001"
    },
    {
      "id_area": "AREA007",
      "nombre": "Reumatología",
      "id_hospital": "HOS001"
    },
    {
      "id_area": "AREA008",
      "nombre": "Infectología",
      "id_hospital": "HOS001"
    },
    {
      "id_area": "AREA009",
      "nombre": "Oncología clínica",
      "id_hospital": "HOS001"
    },
    {
      "id_area": "AREA010",
      "nombre": "Dermatología",
      "id_hospital": "HOS001"
    },
    {
      "id_area": "AREA011",
      "nombre": "Psiquiatría",
      "id_hospital": "HOS001"
    },
    {
      "id_area": "AREA012",
      "nombre": "Otorrinolaringología",
      "id_hospital": "HOS001"
    },
    {
      "id_area": "AREA013",
      "nombre": "Medicina Interna y Familiar",
      "id_hospital": "HOS002"
    },
    {
      "id_area": "AREA014",
      "nombre": "Cardiología",
      "id_hospital": "HOS002"
    },
    {
      "id_area": "AREA015",
      "nombre": "Nefrología",
      "id_hospital": "HOS002"
    },
    {
      "id_area": "AREA016",
      "nombre": "Gastroenterología",
      "id_hospital": "HOS002"
    },
    {
      "id_area": "AREA017",
      "nombre": "Ginecología",
      "id_hospital": "HOS002"
    },
    {
      "id_area": "AREA018",
      "nombre": "Infectología",
      "id_hospital": "HOS002"
    },
    {
      "id_area": "AREA019",
      "nombre": "Reumatología",
      "id_hospital": "HOS002"
    },
    {
      "id_area": "AREA020",
      "nombre": "Pediatría",
      "id_hospital": "HOS002"
    },
    {
      "id_area": "AREA021",
      "nombre": "Psicología",
      "id_hospital": "HOS002"
    },
    {
      "id_area": "AREA022",
      "nombre": "Consulta general y pediatría",
      "id_hospital": "HOS003"
    },
    {
      "id_area": "AREA023",
      "nombre": "Medicina general",
      "id_hospital": "HOS003"
    },
    {
      "id_area": "AREA024",
      "nombre": "Ginecología y obstetricia",
      "id_hospital": "HOS003"
    },
    {
      "id_area": "AREA025",
      "nombre": "Psicología",
      "id_hospital": "HOS003"
    },
    {
      "id_area": "AREA026",
      "nombre": "Fisioterapia",
      "id_hospital": "HOS003"
    },
    {
      "id_area": "AREA027",
      "nombre": "Terapia respiratoria",
      "id_hospital": "HOS003"
    },
    {
      "id_area": "AREA028",
      "nombre": "Neurología",
      "id_hospital": "HOS004"
    },
    {
      "id_area": "AREA029",
      "nombre": "Neurocirugía",
      "id_hospital": "HOS004"
    },
    {
      "id_area": "AREA030",
      "nombre": "Oncología clínica y quirúrgica",
      "id_hospital": "HOS004"
    },
    {
      "id_area": "AREA031",
      "nombre": "Urología",
      "id_hospital": "HOS004"
    },
    {
      "id_area": "AREA032",
      "nombre": "Nefrología",
      "id_hospital": "HOS004"
    },
    {
      "id_area": "AREA033",
      "nombre": "Gastroenterología",
      "id_hospital": "HOS004"
    },
    {
      "id_area": "AREA034",
      "nombre": "Neumología",
      "id_hospital": "HOS004"
    },
    {
      "id_area": "AREA035",
      "nombre": "Endocrinología",
      "id_hospital": "HOS004"
    },
    {
      "id_area": "AREA036",
      "nombre": "Ginecología",
      "id_hospital": "HOS004"
    },
    {
      "id_area": "AREA037",
      "nombre": "Pediatría general",
      "id_hospital": "HOS004"
    },
    {
      "id_area": "AREA038",
      "nombre": "Cirugía plástica",
      "id_hospital": "HOS004"
    },
    {
      "id_area": "AREA039",
      "nombre": "Unidad de Quemados",
      "id_hospital": "HOS004"
    },
    {
      "id_area": "AREA040",
      "nombre": "Medicina integrativa",
      "id_hospital": "HOS004"
    }
]);
```

6. Creacion de la coleccion personal:
```js
db.createCollection("personal", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["_id", "id_hospital", "nombre", "documento", "id_rol", "correo", "telefono", "salario"],
      properties: {
        _id: { bsonType: "string" },
        id_hospital: { bsonType: "string" },
        nombre: { bsonType: "string" },
        documento: { bsonType: "string" },
        numero_colegiatura: { bsonType: ["string", "null"] },
        id_rol: { bsonType: "string" },
        id_especialidad: { bsonType: ["string", "null"] },
        correo: { bsonType: "string" },
        telefono: { bsonType: "string" },
        salario: { bsonType: "number" }
      }
    }
  }
});
```

* Insertar datos a la coleccion ("personal"):
```js
db.personal.insertMany([{
      "id_personal": "PER001",
      "id_hospital": "HOS001",
      "nombre": "Dr. Roberto Silva Mendoza",
      "documento": "98765432",
      "numero_colegiatura": "COL001",
      "id_rol": "001",
      "id_especialidad": "ESP014",
      "correo": "roberto.silva@hus.gov.co",
      "telefono": "3009876543",
      "salario": 8500000
    },
    {
      "id_personal": "PER002",
      "id_hospital": "HOS001", 
      "nombre": "Dr. Ana Lucía Pérez Torres",
      "documento": "45678912",
      "numero_colegiatura": "COL002",
      "id_rol": "002",
      "id_especialidad": "ESP001",
      "correo": "ana.perez@hus.gov.co",
      "telefono": "3004567891",
      "salario": 6500000
    },
    {
      "id_personal": "PER003",
      "id_hospital": "HOS001",
      "nombre": "Dr. Miguel Ángel Torres Castro",
      "documento": "78912345",
      "numero_colegiatura": "COL003",
      "id_rol": "002", 
      "id_especialidad": "ESP003",
      "correo": "miguel.torres@hus.gov.co",
      "telefono": "3007891234",
      "salario": 7200000
    },
    {
      "id_personal": "PER004",
      "id_hospital": "HOS001",
      "nombre": "Dra. Carmen Rosa Jiménez Vargas",
      "documento": "32165498",
      "numero_colegiatura": "COL004",
      "id_rol": "002",
      "id_especialidad": "ESP007",
      "correo": "carmen.jimenez@hus.gov.co", 
      "telefono": "3003216549",
      "salario": 6800000
    },
    {
      "id_personal": "PER005",
      "id_hospital": "HOS001",
      "nombre": "Dr. Fernando Andrés López Herrera",
      "documento": "65498732",
      "numero_colegiatura": "COL005",
      "id_rol": "002",
      "id_especialidad": "ESP010",
      "correo": "fernando.lopez@hus.gov.co",
      "telefono": "3006549873",
      "salario": 7500000
    },
    {
      "id_personal": "PER006",
      "id_hospital": "HOS001",
      "nombre": "Enfermera Luz Marina Gómez Ruiz",
      "documento": "65432198",
      "numero_colegiatura": null,
      "id_rol": "003",
      "id_especialidad": null,
      "correo": "luz.gomez@hus.gov.co",
      "telefono": "3006543219",
      "salario": 2800000
    },
    {
      "id_personal": "PER007",
      "id_hospital": "HOS001",
      "nombre": "Enfermera Patricia Morales Díaz",
      "documento": "98765123",
      "numero_colegiatura": null,
      "id_rol": "003",
      "id_especialidad": null,
      "correo": "patricia.morales@hus.gov.co",
      "telefono": "3009876512",
      "salario": 2800000
    },
    {
      "id_personal": "PER008",
      "id_hospital": "HOS001",
      "nombre": "Enfermero Carlos Ruiz Sánchez",
      "documento": "14725836",
      "numero_colegiatura": null,
      "id_rol": "003",
      "id_especialidad": null,
      "correo": "carlos.ruiz@hus.gov.co",
      "telefono": "3001472583",
      "salario": 2800000
    },
    {
      "id_personal": "PER009",
      "id_hospital": "HOS001",
      "nombre": "Enfermera Sandra López Martínez",
      "documento": "36925814",
      "numero_colegiatura": null,
      "id_rol": "003",
      "id_especialidad": null,
      "correo": "sandra.lopez@hus.gov.co",
      "telefono": "3003692581",
      "salario": 2800000
    },
    {
      "id_personal": "PER010",
      "id_hospital": "HOS001",
      "nombre": "Enfermera Diana Herrera González",
      "documento": "75395148",
      "numero_colegiatura": null,
      "id_rol": "003",
      "id_especialidad": null,
      "correo": "diana.herrera@hus.gov.co",
      "telefono": "3007539514",
      "salario": 2800000
    },
    {
      "id_personal": "PER011",
      "id_hospital": "HOS001",
      "nombre": "Enfermero Andrés Castro Ramírez",
      "documento": "95175346",
      "numero_colegiatura": null,
      "id_rol": "003",
      "id_especialidad": null,
      "correo": "andres.castro@hus.gov.co",
      "telefono": "3009517534",
      "salario": 2800000
    },
    {
      "id_personal": "PER012",
      "id_hospital": "HOS001",
      "nombre": "Enfermera Mónica Vega Rodríguez",
      "documento": "15935748",
      "numero_colegiatura": null,
      "id_rol": "003",
      "id_especialidad": null,
      "correo": "monica.vega@hus.gov.co",
      "telefono": "3001593574",
      "salario": 2800000
    },
    {
      "id_personal": "PER013",
      "id_hospital": "HOS001",
      "nombre": "Enfermera Claudia Ramírez Torres",
      "documento": "75315926",
      "numero_colegiatura": null,
      "id_rol": "003",
      "id_especialidad": null,
      "correo": "claudia.ramirez@hus.gov.co",
      "telefono": "3007531592",
      "salario": 2800000
    },
    {
      "id_personal": "PER014",
      "id_hospital": "HOS001",
      "nombre": "Administradora Esperanza Díaz Morales",
      "documento": "85296374",
      "numero_colegiatura": null,
      "id_rol": "004",
      "id_especialidad": null,
      "correo": "esperanza.diaz@hus.gov.co",
      "telefono": "3008529637",
      "salario": 3200000
    },
    {
      "id_personal": "PER015",
      "id_hospital": "HOS001",
      "nombre": "Contador Luis Fernando Sánchez Pérez",
      "documento": "96385274",
      "numero_colegiatura": null,
      "id_rol": "004",
      "id_especialidad": null,
      "correo": "luis.sanchez@hus.gov.co",
      "telefono": "3009638527",
      "salario": 3500000
    },
    {
      "id_personal": "PER016",
      "id_hospital": "HOS001",
      "nombre": "Secretaria Rosa Elena Martínez Castro",
      "documento": "74185296",
      "numero_colegiatura": null,
      "id_rol": "004",
      "id_especialidad": null,
      "correo": "rosa.martinez@hus.gov.co",
      "telefono": "3007418529",
      "salario": 2200000
    },
    {
      "id_personal": "PER017",
      "id_hospital": "HOS001",
      "nombre": "Auxiliar Administrativo Pedro González Herrera",
      "documento": "52963741",
      "numero_colegiatura": null,
      "id_rol": "004",
      "id_especialidad": null,
      "correo": "pedro.gonzalez@hus.gov.co",
      "telefono": "3005296374",
      "salario": 2000000
    },
    {
      "id_personal": "PER018",
      "id_hospital": "HOS001",
      "nombre": "Recepcionista María José Vargas López",
      "documento": "41852963",
      "numero_colegiatura": null,
      "id_rol": "004",
      "id_especialidad": null,
      "correo": "maria.vargas@hus.gov.co",
      "telefono": "3004185296",
      "salario": 1800000
    },
    {
      "id_personal": "PER019",
      "id_hospital": "HOS001",
      "nombre": "Auxiliar de Archivo Beatriz Rojas Silva",
      "documento": "96374185",
      "numero_colegiatura": null,
      "id_rol": "004",
      "id_especialidad": null,
      "correo": "beatriz.rojas@hus.gov.co",
      "telefono": "3009637418",
      "salario": 1900000
    },
    {
      "id_personal": "PER020",
      "id_hospital": "HOS001",
      "nombre": "Coordinadora de Recursos Humanos Liliana Torres Mendoza",
      "documento": "85274196",
      "numero_colegiatura": null,
      "id_rol": "004",
      "id_especialidad": null,
      "correo": "liliana.torres@hus.gov.co",
      "telefono": "3008527419",
      "salario": 3800000
    },
    {
      "id_personal": "PER021",
      "id_hospital": "HOS001",
      "nombre": "Técnico de Mantenimiento Jorge Herrera Ramírez",
      "documento": "74196385",
      "numero_colegiatura": null,
      "id_rol": "005",
      "id_especialidad": null,
      "correo": "jorge.herrera@hus.gov.co",
      "telefono": "3007419638",
      "salario": 2100000
    },
    {
      "id_personal": "PER022",
      "id_hospital": "HOS001",
      "nombre": "Auxiliar de Limpieza Carmen Gutiérrez Díaz",
      "documento": "19638527",
      "numero_colegiatura": null,
      "id_rol": "005",
      "id_especialidad": null,
      "correo": "carmen.gutierrez@hus.gov.co",
      "telefono": "3001963852",
      "salario": 1500000
    },
    {
      "id_personal": "PER023",
      "id_hospital": "HOS001",
      "nombre": "Auxiliar de Limpieza Roberto Mendoza Torres",
      "documento": "63852741",
      "numero_colegiatura": null,
      "id_rol": "005",
      "id_especialidad": null,
      "correo": "roberto.mendoza@hus.gov.co",
      "telefono": "3006385274",
      "salario": 1500000
    },
    {
      "id_personal": "PER024",
      "id_hospital": "HOS001",
      "nombre": "Técnico Eléctrico Fernando Castro López",
      "documento": "52741963",
      "numero_colegiatura": null,
      "id_rol": "005",
      "id_especialidad": null,
      "correo": "fernando.castro@hus.gov.co",
      "telefono": "3005274196",
      "salario": 2300000
    },
    {
      "id_personal": "PER025",
      "id_hospital": "HOS001",
      "nombre": "Auxiliar de Mantenimiento Gloria Pérez Vargas",
      "documento": "41963852",
      "numero_colegiatura": null,
      "id_rol": "005",
      "id_especialidad": null,
      "correo": "gloria.perez@hus.gov.co",
      "telefono": "3004196385",
      "salario": 1800000
    },
    {
      "id_personal": "PER026",
      "id_hospital": "HOS001",
      "nombre": "Jardinero Álvaro Ramírez Sánchez",
      "documento": "96385274",
      "numero_colegiatura": null,
      "id_rol": "005",
      "id_especialidad": null,
      "correo": "alvaro.ramirez@hus.gov.co",
      "telefono": "3009638527",
      "salario": 1600000
    }
]);
```

6. Creación de la colección ("Pacientes"):
```js
db.createCollection("pacientes", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["_id", "historia_clinica", "nombre", "documento", "fecha_nacimiento", "sexo", "correo", "telefono", "direccion", "seguro_medico"],
      properties: {
        _id: { bsonType: "string" },
        historia_clinica: { bsonType: "string" },
        nombre: { bsonType: "string" },
        documento: { bsonType: "string" },
        fecha_nacimiento: { bsonType: "string" },
        sexo: { bsonType: "string" },
        correo: { bsonType: "string" },
        telefono: { bsonType: "string" },
        direccion: { bsonType: "string" },
        seguro_medico: { bsonType: "string" }
      }
    }
  }
});
```

* Insertar datos a la colección pacientes:
```js
db.pacientes.insertMany([
  {
      "id_paciente": "PAC001",
      "historia_clinica": "HC001001",
      "nombre": "María Fernanda Rodríguez Gómez",
      "documento": "1098765432",
      "fecha_nacimiento": "1985-03-15",
      "sexo": "F",
      "correo": "maria.rodriguez@email.com",
      "telefono": "3101234567",
      "direccion": "Calle 45 #12-34, Bucaramanga",
      "seguro_medico": "EPS Sanitas"
    },
    {
      "id_paciente": "PAC002",
      "historia_clinica": "HC001002",
      "nombre": "Carlos Alberto Gómez Herrera",
      "documento": "1087654321",
      "fecha_nacimiento": "1978-07-22",
      "sexo": "M",
      "correo": "carlos.gomez@email.com",
      "telefono": "3107654321",
      "direccion": "Carrera 27 #56-78, Bucaramanga",
      "seguro_medico": "EPS Sura"
    },
    {
      "id_paciente": "PAC003",
      "historia_clinica": "HC001003",
      "nombre": "Ana Lucía Martínez Torres",
      "documento": "1076543210",
      "fecha_nacimiento": "1992-11-08",
      "sexo": "F",
      "correo": "ana.martinez@email.com",
      "telefono": "3106543210",
      "direccion": "Avenida Quebradaseca #89-12, Bucaramanga",
      "seguro_medico": "EPS Famisanar"
    },
    {
      "id_paciente": "PAC004",
      "historia_clinica": "HC001004",
      "nombre": "José Miguel Torres Castro",
      "documento": "1065432109",
      "fecha_nacimiento": "1965-05-30",
      "sexo": "M",
      "correo": "jose.torres@email.com",
      "telefono": "3105432109",
      "direccion": "Calle 36 #23-45, Bucaramanga",
      "seguro_medico": "EPS Nueva EPS"
    },
    {
      "id_paciente": "PAC005",
      "historia_clinica": "HC001005",
      "nombre": "Claudia Patricia Herrera Vargas",
      "documento": "1054321098",
      "fecha_nacimiento": "1988-12-14",
      "sexo": "F",
      "correo": "claudia.herrera@email.com",
      "telefono": "3104321098",
      "direccion": "Carrera 15 #67-89, Bucaramanga",
      "seguro_medico": "EPS Compensar"
    },
    {
      "id_paciente": "PAC006",
      "historia_clinica": "HC001006",
      "nombre": "Roberto Carlos Jiménez López",
      "documento": "1043210987",
      "fecha_nacimiento": "1975-09-03",
      "sexo": "M",
      "correo": "roberto.jimenez@email.com",
      "telefono": "3103210987",
      "direccion": "Calle 52 #34-56, Bucaramanga",
      "seguro_medico": "EPS Sanitas"
    },
    {
      "id_paciente": "PAC007",
      "historia_clinica": "HC001007",
      "nombre": "Diana Carolina López Mendoza",
      "documento": "1032109876",
      "fecha_nacimiento": "1990-02-18",
      "sexo": "F",
      "correo": "diana.lopez@email.com",
      "telefono": "3102109876",
      "direccion": "Avenida González Valencia #78-90, Bucaramanga",
      "seguro_medico": "EPS Sura"
    },
    {
      "id_paciente": "PAC008",
      "historia_clinica": "HC001008",
      "nombre": "Fernando Andrés Castro Ruiz",
      "documento": "1021098765",
      "fecha_nacimiento": "1982-06-25",
      "sexo": "M",
      "correo": "fernando.castro@email.com",
      "telefono": "3101098765",
      "direccion": "Carrera 33 #45-67, Bucaramanga",
      "seguro_medico": "EPS Famisanar"
    },
    {
      "id_paciente": "PAC009",
      "historia_clinica": "HC001009",
      "nombre": "Mónica Alejandra Vega Sánchez",
      "documento": "1010987654",
      "fecha_nacimiento": "1995-01-12",
      "sexo": "F",
      "correo": "monica.vega@email.com",
      "telefono": "3100987654",
      "direccion": "Calle 28 #56-78, Bucaramanga",
      "seguro_medico": "EPS Nueva EPS"
    },
    {
      "id_paciente": "PAC010",
      "historia_clinica": "HC001010",
      "nombre": "Andrés Felipe Ramírez Díaz",
      "documento": "1009876543",
      "fecha_nacimiento": "1987-04-07",
      "sexo": "M",
      "correo": "andres.ramirez@email.com",
      "telefono": "3109876543",
      "direccion": "Carrera 19 #67-89, Bucaramanga",
      "seguro_medico": "EPS Compensar"
    },
    {
      "id_paciente": "PAC011",
      "historia_clinica": "HC001011",
      "nombre": "Sandra Milena Díaz Morales",
      "documento": "1098765431",
      "fecha_nacimiento": "1983-08-19",
      "sexo": "F",
      "correo": "sandra.diaz@email.com",
      "telefono": "3108765431",
      "direccion": "Calle 41 #78-90, Bucaramanga",
      "seguro_medico": "EPS Sanitas"
    },
    {
      "id_paciente": "PAC012",
      "historia_clinica": "HC001012",
      "nombre": "Luis Eduardo Sánchez Pérez",
      "documento": "1087654320",
      "fecha_nacimiento": "1979-10-26",
      "sexo": "M",
      "correo": "luis.sanchez@email.com",
      "telefono": "3107654320",
      "direccion": "Avenida Santander #89-01, Bucaramanga",
      "seguro_medico": "EPS Sura"
    },
    {
      "id_paciente": "PAC013",
      "historia_clinica": "HC001013",
      "nombre": "Patricia Elena González Castro",
      "documento": "1076543219",
      "fecha_nacimiento": "1991-03-13",
      "sexo": "F",
      "correo": "patricia.gonzalez@email.com",
      "telefono": "3106543219",
      "direccion": "Carrera 25 #12-34, Bucaramanga",
      "seguro_medico": "EPS Famisanar"
    },
    {
      "id_paciente": "PAC014",
      "historia_clinica": "HC001014",
      "nombre": "Miguel Ángel Vargas Herrera",
      "documento": "1065432108",
      "fecha_nacimiento": "1986-07-04",
      "sexo": "M",
      "correo": "miguel.vargas@email.com",
      "telefono": "3105432108",
      "direccion": "Calle 37 #45-67, Bucaramanga",
      "seguro_medico": "EPS Nueva EPS"
    },
    {
      "id_paciente": "PAC015",
      "historia_clinica": "HC001015",
      "nombre": "Carmen Rosa Morales González",
      "documento": "1054321097",
      "fecha_nacimiento": "1994-12-21",
      "sexo": "F",
      "correo": "carmen.morales@email.com",
      "telefono": "3104321097",
      "direccion": "Carrera 21 #56-78, Bucaramanga",
      "seguro_medico": "EPS Compensar"
    },
    {
      "id_paciente": "PAC016",
      "historia_clinica": "HC001016",
      "nombre": "Jorge Alberto Ruiz Torres",
      "documento": "1043210986",
      "fecha_nacimiento": "1977-05-16",
      "sexo": "M",
      "correo": "jorge.ruiz@email.com",
      "telefono": "3103210986",
      "direccion": "Calle 48 #67-89, Bucaramanga",
      "seguro_medico": "EPS Sanitas"
    },
    {
      "id_paciente": "PAC017",
      "historia_clinica": "HC001017",
      "nombre": "Luz Marina Peña Rodríguez",
      "documento": "1032109875",
      "fecha_nacimiento": "1989-09-28",
      "sexo": "F",
      "correo": "luz.pena@email.com",
      "telefono": "3102109875",
      "direccion": "Avenida Los Estudiantes #78-90, Bucaramanga",
      "seguro_medico": "EPS Sura"
    },
    {
      "id_paciente": "PAC018",
      "historia_clinica": "HC001018",
      "nombre": "Álvaro Enrique Mendoza Silva",
      "documento": "1021098764",
      "fecha_nacimiento": "1981-11-11",
      "sexo": "M",
      "correo": "alvaro.mendoza@email.com",
      "telefono": "3101098764",
      "direccion": "Carrera 29 #89-01, Bucaramanga",
      "seguro_medico": "EPS Famisanar"
    },
    {
      "id_paciente": "PAC019",
      "historia_clinica": "HC001019",
      "nombre": "Beatriz Elena Rojas Martínez",
      "documento": "1010987653",
      "fecha_nacimiento": "1993-02-05",
      "sexo": "F",
      "correo": "beatriz.rojas@email.com",
      "telefono": "3100987653",
      "direccion": "Calle 32 #12-34, Bucaramanga",
      "seguro_medico": "EPS Nueva EPS"
    },
    {
      "id_paciente": "PAC020",
      "historia_clinica": "HC001020",
      "nombre": "Pedro Antonio Silva López",
      "documento": "1009876542",
      "fecha_nacimiento": "1984-06-17",
      "sexo": "M",
      "correo": "pedro.silva@email.com",
      "telefono": "3109876542",
      "direccion": "Carrera 17 #45-67, Bucaramanga",
      "seguro_medico": "EPS Compensar"
    },
    {
      "id_paciente": "PAC021",
      "historia_clinica": "HC001021",
      "nombre": "Gloria Esperanza Torres Castro",
      "documento": "1098765430",
      "fecha_nacimiento": "1976-08-23",
      "sexo": "F",
      "correo": "gloria.torres@email.com",
      "telefono": "3108765430",
      "direccion": "Calle 44 #56-78, Bucaramanga",
      "seguro_medico": "EPS Sanitas"
    },
    {
      "id_paciente": "PAC022",
      "historia_clinica": "HC001022",
      "nombre": "Ricardo Javier Castro Herrera",
      "documento": "1087654319",
      "fecha_nacimiento": "1980-10-09",
      "sexo": "M",
      "correo": "ricardo.castro@email.com",
      "telefono": "3107654319",
      "direccion": "Avenida La Rosita #67-89, Bucaramanga",
      "seguro_medico": "EPS Sura"
    },
    {
      "id_paciente": "PAC023",
      "historia_clinica": "HC001023",
      "nombre": "Liliana María Herrera González",
      "documento": "1076543218",
      "fecha_nacimiento": "1996-01-14",
      "sexo": "F",
      "correo": "liliana.herrera@email.com",
      "telefono": "3106543218",
      "direccion": "Carrera 23 #78-90, Bucaramanga",
      "seguro_medico": "EPS Famisanar"
    },
    {
      "id_paciente": "PAC024",
      "historia_clinica": "HC001024",
      "nombre": "Jairo Augusto López Vargas",
      "documento": "1065432107",
      "fecha_nacimiento": "1974-04-20",
      "sexo": "M",
      "correo": "jairo.lopez@email.com",
      "telefono": "3105432107",
      "direccion": "Calle 39 #89-01, Bucaramanga",
      "seguro_medico": "EPS Nueva EPS"
    },
    {
      "id_paciente": "PAC025",
      "historia_clinica": "HC001025",
      "nombre": "Esperanza del Carmen Jiménez Díaz",
      "documento": "1054321096",
      "fecha_nacimiento": "1988-07-31",
      "sexo": "F",
      "correo": "esperanza.jimenez@email.com",
      "telefono": "3104321096",
      "direccion": "Carrera 31 #12-34, Bucaramanga",
      "seguro_medico": "EPS Compensar"
    },
    {
      "id_paciente": "PAC026",
      "historia_clinica": "HC001026",
      "nombre": "Hernando José Gómez Morales",
      "documento": "1043210985",
      "fecha_nacimiento": "1972-12-06",
      "sexo": "M",
      "correo": "hernando.gomez@email.com",
      "telefono": "3103210985",
      "direccion": "Calle 46 #45-67, Bucaramanga",
      "seguro_medico": "EPS Sanitas"
    },
    {
      "id_paciente": "PAC027",
      "historia_clinica": "HC001027",
      "nombre": "Rocío Amparo Martínez Sánchez",
      "documento": "1032109874",
      "fecha_nacimiento": "1985-03-18",
      "sexo": "F",
      "correo": "rocio.martinez@email.com",
      "telefono": "3102109874",
      "direccion": "Avenida Centenario #56-78, Bucaramanga",
      "seguro_medico": "EPS Sura"
    },
    {
      "id_paciente": "PAC028",
      "historia_clinica": "HC001028",
      "nombre": "Guillermo Enrique Vargas Pérez",
      "documento": "1021098763",
      "fecha_nacimiento": "1983-09-24",
      "sexo": "M",
      "correo": "guillermo.vargas@email.com",
      "telefono": "3101098763",
      "direccion": "Carrera 35 #67-89, Bucaramanga",
      "seguro_medico": "EPS Famisanar"
    },
    {
      "id_paciente": "PAC029",
      "historia_clinica": "HC001029",
      "nombre": "Amparo Stella Rodríguez Torres",
      "documento": "1010987652",
      "fecha_nacimiento": "1991-05-02",
      "sexo": "F",
      "correo": "amparo.rodriguez@email.com",
      "telefono": "3100987652",
      "direccion": "Calle 34 #78-90, Bucaramanga",
      "seguro_medico": "EPS Nueva EPS"
    },
    {
      "id_paciente": "PAC030",
      "historia_clinica": "HC001030",
      "nombre": "Édgar Mauricio Sánchez Castro",
      "documento": "1009876541",
      "fecha_nacimiento": "1987-11-15",
      "sexo": "M",
      "correo": "edgar.sanchez@email.com",
      "telefono": "3109876541",
      "direccion": "Carrera 27 #89-01, Bucaramanga",
      "seguro_medico": "EPS Compensar"
    }
]);
```

7. Creacion de la colección ("categorias_medicamentos"):
```js
db.createCollection("categorias_medicamentos", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["_id", "nombre", "id_hospital"],
      properties: {
        _id: { bsonType: "string" },
        nombre: { bsonType: "string" },
        id_hospital: { bsonType: "string" }
      }
    }
  }
});
```

* Insertar datos a la colección categorias_medicamentos:
```js
db.categorias_medicamentos.insertMany([
  {
      "id_categoria": "CAT001",
      "nombre": "Analgésicos"
    },
    {
      "id_categoria": "CAT002",
      "nombre": "Antibióticos"
    },
    {
      "id_categoria": "CAT003",
      "nombre": "Antiinflamatorios"
    },
    {
      "id_categoria": "CAT004",
      "nombre": "Cardiovasculares"
    },
    {
      "id_categoria": "CAT005",
      "nombre": "Neurológicos"
    },
    {
      "id_categoria": "CAT006",
      "nombre": "Gastrointestinales"
    },
    {
      "id_categoria": "CAT007",
      "nombre": "Endocrinos"
    },
    {
      "id_categoria": "CAT008",
      "nombre": "Respiratorios"
    },
    {
      "id_categoria": "CAT009",
      "nombre": "Dermatológicos"
    },
    {
      "id_categoria": "CAT010",
      "nombre": "Oncológicos"
    }
]);
```

8. Creacion de la colección ("medicamentos"):
```js
db.createCollection("categorias_medicamentos", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["_id", "nombre", "id_hospital"],
      properties: {
        _id: { bsonType: "string" },
        nombre: { bsonType: "string" },
        id_hospital: { bsonType: "string" }
      }
    }
  }
});
```

* Insertar datos a la colección medicamentos:
```js
db.medicamentos.insertMany([
  {
      "id_medicamento": "MED001",
      "id_hospital": "HOS001",
      "nombre": "Acetaminofén 500mg",
      "fabricante": "Genfar",
      "id_categoria": "CAT001",
      "stock_actual": 500
    },
    {
      "id_medicamento": "MED002",
      "id_hospital": "HOS001",
      "nombre": "Amoxicilina 500mg",
      "fabricante": "MK",
      "id_categoria": "CAT002",
      "stock_actual": 300
    },
    {
      "id_medicamento": "MED003",
      "id_hospital": "HOS001",
      "nombre": "Ibuprofeno 400mg",
      "fabricante": "Tecnoquímicas",
      "id_categoria": "CAT003",
      "stock_actual": 250
    },
    {
      "id_medicamento": "MED004",
      "id_hospital": "HOS001",
      "nombre": "Enalapril 10mg",
      "fabricante": "Lafrancol",
      "id_categoria": "CAT004",
      "stock_actual": 180
    },
    {
      "id_medicamento": "MED005",
      "id_hospital": "HOS001",
      "nombre": "Carbamazepina 200mg",
      "fabricante": "Procaps",
      "id_categoria": "CAT005",
      "stock_actual": 120
    },
    {
      "id_medicamento": "MED006",
      "id_hospital": "HOS001",
      "nombre": "Omeprazol 20mg",
      "fabricante": "Tecnoquímicas",
      "id_categoria": "CAT006",
      "stock_actual": 400
    },
    {
      "id_medicamento": "MED007",
      "id_hospital": "HOS001",
      "nombre": "Metformina 850mg",
      "fabricante": "MK",
      "id_categoria": "CAT007",
      "stock_actual": 200
    },
    {
      "id_medicamento": "MED008",
      "id_hospital": "HOS001",
      "nombre": "Salbutamol 100mcg",
      "fabricante": "Genfar",
      "id_categoria": "CAT008",
      "stock_actual": 150
    },
    {
      "id_medicamento": "MED009",
      "id_hospital": "HOS002",
      "nombre": "Losartán 50mg",
      "fabricante": "Genfar",
      "id_categoria": "CAT004",
      "stock_actual": 200
    },
    {
      "id_medicamento": "MED010",
      "id_hospital": "HOS002",
      "nombre": "Ciprofloxacina 500mg",
      "fabricante": "MK",
      "id_categoria": "CAT002",
      "stock_actual": 180
    },
    {
      "id_medicamento": "MED011",
      "id_hospital": "HOS002",
      "nombre": "Diclofenaco 75mg",
      "fabricante": "Tecnoquímicas",
      "id_categoria": "CAT003",
      "stock_actual": 220
    },
    {
      "id_medicamento": "MED012",
      "id_hospital": "HOS002",
      "nombre": "Furosemida 40mg",
      "fabricante": "Lafrancol",
      "id_categoria": "CAT004",
      "stock_actual": 160
    },
    {
      "id_medicamento": "MED013",
      "id_hospital": "HOS003",
      "nombre": "Paracetamol 500mg",
      "fabricante": "Procaps",
      "id_categoria": "CAT001",
      "stock_actual": 350
    },
    {
      "id_medicamento": "MED014",
      "id_hospital": "HOS003",
      "nombre": "Cefalexina 500mg",
      "fabricante": "Genfar",
      "id_categoria": "CAT002",
      "stock_actual": 280
    },
    {
      "id_medicamento": "MED015",
      "id_hospital": "HOS003",
      "nombre": "Ranitidina 150mg",
      "fabricante": "MK",
      "id_categoria": "CAT006",
      "stock_actual": 190
    },
    {
      "id_medicamento": "MED016",
      "id_hospital": "HOS004",
      "nombre": "Atorvastatina 20mg",
      "fabricante": "Lafrancol",
      "id_categoria": "CAT004",
      "stock_actual": 100
    },
    {
      "id_medicamento": "MED017",
      "id_hospital": "HOS004",
      "nombre": "Fenitoína 100mg",
      "fabricante": "Procaps",
      "id_categoria": "CAT005",
      "stock_actual": 80
    },
    {
      "id_medicamento": "MED018",
      "id_hospital": "HOS004",
      "nombre": "Cisplatino 50mg",
      "fabricante": "Tecnoquímicas",
      "id_categoria": "CAT010",
      "stock_actual": 25
    },
    {
      "id_medicamento": "MED019",
      "id_hospital": "HOS004",
      "nombre": "Betametasona 0.5mg",
      "fabricante": "Genfar",
      "id_categoria": "CAT009",
      "stock_actual": 120
    },
    {
      "id_medicamento": "MED020",
      "id_hospital": "HOS004",
      "nombre": "Budesonida 200mcg",
      "fabricante": "MK",
      "id_categoria": "CAT008",
      "stock_actual": 90
    }
]);
```

10. Creacion de la colección ("visitas"):
```js
db.createCollection("categorias_medicamentos", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["_id", "nombre", "id_hospital"],
      properties: {
        _id: { bsonType: "string" },
        nombre: { bsonType: "string" },
        id_hospital: { bsonType: "string" }
      }
    }
  }
});
```

* Insertar datos a la colección visitas:
```js
db.visitas.insertMany([
   {
      "id_visita": "VIS001",
      "id_paciente": "PAC001",
      "id_hospital": "HOS001",
      "id_area": "AREA001",
      "id_personal": "PER002",
      "fecha_visita": "2024-01-15",
      "hora_visita": "08:30",
      "motivo": "Dolor en el pecho",
      "diagnostico": "Angina de pecho estable"
    },
    {
      "id_visita": "VIS002",
      "id_paciente": "PAC001",
      "id_hospital": "HOS001",
      "id_area": "AREA001",
      "id_personal": "PER002",
      "fecha_visita": "2024-02-20",
      "hora_visita": "10:15",
      "motivo": "Control cardiológico",
      "diagnostico": "Evolución favorable"
    },
    {
      "id_visita": "VIS003",
      "id_paciente": "PAC001",
      "id_hospital": "HOS001",
      "id_area": "AREA001",
      "id_personal": "PER002",
      "fecha_visita": "2024-03-25",
      "hora_visita": "14:00",
      "motivo": "Control de medicación",
      "diagnostico": "Respuesta adecuada al tratamiento"
    },
    {
      "id_visita": "VIS004",
      "id_paciente": "PAC002",
      "id_hospital": "HOS001",
      "id_area": "AREA002",
      "id_personal": "PER003",
      "fecha_visita": "2024-01-22",
      "hora_visita": "09:00",
      "motivo": "Cefalea persistente",
      "diagnostico": "Migraña crónica"
    },
    {
      "id_visita": "VIS005",
      "id_paciente": "PAC002",
      "id_hospital": "HOS001",
      "id_area": "AREA002",
      "id_personal": "PER003",
      "fecha_visita": "2024-02-28",
      "hora_visita": "11:30",
      "motivo": "Control neurológico",
      "diagnostico": "Mejoría parcial de síntomas"
    },
    {
      "id_visita": "VIS006",
      "id_paciente": "PAC003",
      "id_hospital": "HOS001",
      "id_area": "AREA006",
      "id_personal": "PER004",
      "fecha_visita": "2024-01-28",
      "hora_visita": "15:45",
      "motivo": "Control pediátrico",
      "diagnostico": "Desarrollo normal"
    },
    {
      "id_visita": "VIS007",
      "id_paciente": "PAC003",
      "id_hospital": "HOS001",
      "id_area": "AREA006",
      "id_personal": "PER004",
      "fecha_visita": "2024-03-15",
      "hora_visita": "16:20",
      "motivo": "Vacunación",
      "diagnostico": "Esquema de vacunación completo"
    },  
    
    {
      "id_visita": "VIS008",
      "id_paciente": "PAC004",
      "id_hospital": "HOS001",
      "id_area": "AREA009",
      "id_personal": "PER005",
      "fecha_visita": "2024-02-05",
      "hora_visita": "08:00",
      "motivo": "Seguimiento oncológico",
      "diagnostico": "Respuesta parcial al tratamiento"
    },
    {
      "id_visita": "VIS009",
      "id_paciente": "PAC004",
      "id_hospital": "HOS001",
      "id_area": "AREA009",
      "id_personal": "PER005",
      "fecha_visita": "2024-03-10",
      "hora_visita": "09:30",
      "motivo": "Control post-quimioterapia",
      "diagnostico": "Tolerancia adecuada al tratamiento"
    },
    {
      "id_visita": "VIS010",
      "id_paciente": "PAC005",
      "id_hospital": "HOS001",
      "id_area": "AREA001",
      "id_personal": "PER002",
      "fecha_visita": "2024-01-18",
      "hora_visita": "13:15",
      "motivo": "Hipertensión arterial",
      "diagnostico": "HTA grado II"
    },
    {
      "id_visita": "VIS011",
      "id_paciente": "PAC005",
      "id_hospital": "HOS001",
      "id_area": "AREA001",
      "id_personal": "PER002",
      "fecha_visita": "2024-02-22",
      "hora_visita": "14:45",
      "motivo": "Control de presión arterial",
      "diagnostico": "Presión arterial controlada"
    },
    {
      "id_visita": "VIS012",
      "id_paciente": "PAC006",
      "id_hospital": "HOS001",
      "id_area": "AREA002",
      "id_personal": "PER003",
      "fecha_visita": "2024-02-12",
      "hora_visita": "10:00",
      "motivo": "Mareos frecuentes",
      "diagnostico": "Vértigo posicional benigno"
    },
    {
      "id_visita": "VIS013",
      "id_paciente": "PAC007",
      "id_hospital": "HOS001",
      "id_area": "AREA003",
      "id_personal": "PER003",
      "fecha_visita": "2024-01-25",
      "hora_visita": "11:30",
      "motivo": "Dificultad respiratoria",
      "diagnostico": "Asma bronquial"
    },
    {
      "id_visita": "VIS014",
      "id_paciente": "PAC008",
      "id_hospital": "HOS001",
      "id_area": "AREA004",
      "id_personal": "PER002",
      "fecha_visita": "2024-02-08",
      "hora_visita": "15:00",
      "motivo": "Dolor abdominal",
      "diagnostico": "Gastritis crónica"
    },
    {
      "id_visita": "VIS015",
      "id_paciente": "PAC009",
      "id_hospital": "HOS001",
      "id_area": "AREA005",
      "id_personal": "PER004",
      "fecha_visita": "2024-01-30",
      "hora_visita": "09:45",
      "motivo": "Control diabético",
      "diagnostico": "Diabetes mellitus tipo 2 controlada"
    }
]);
```

11. Creacion de la colección ("hitoria_tratamiento"):
```js
db.createCollection("historia_tratamiento", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["_id", "nombre", "id_hospital"],
      properties: {
        _id: { bsonType: "string" },
        nombre: { bsonType: "string" },
        id_hospital: { bsonType: "string" }
      }
    }
  }
});
```

* Insertar datos a la colección historia_tratamiento:
```js
db.historia_tratamiento.insertMany([
    {
      "id_historia": "HT001",
      "id_paciente": "PAC001",
      "id_tratamiento": "TRA001",
      "fecha_inicio": "2024-01-15",
      "fecha_fin": null,
      "estado": "Activo",
      "resultado": "En seguimiento"
    },
    {
      "id_historia": "HT002",
      "id_paciente": "PAC001",
      "id_tratamiento": "TRA002",
      "fecha_inicio": "2024-01-15",
      "fecha_fin": "2024-01-15",
      "estado": "Completado",
      "resultado": "Normal"
    },
    {
      "id_historia": "HT003",
      "id_paciente": "PAC002",
      "id_tratamiento": "TRA004",
      "fecha_inicio": "2024-01-22",
      "fecha_fin": null,
      "estado": "Activo",
      "resultado": "En tratamiento"
    },
    {
      "id_historia": "HT004",
      "id_paciente": "PAC002",
      "id_tratamiento": "TRA005",
      "fecha_inicio": "2024-02-01",
      "fecha_fin": "2024-02-01",
      "estado": "Completado",
      "resultado": "Sin alteraciones significativas"
    },
    {
      "id_historia": "HT005",
      "id_paciente": "PAC003",
      "id_tratamiento": "TRA013",
      "fecha_inicio": "2024-01-28",
      "fecha_fin": null,
      "estado": "Activo",
      "resultado": "Desarrollo adecuado"
    },
    {
      "id_historia": "HT006",
      "id_paciente": "PAC004",
      "id_tratamiento": "TRA019",
      "fecha_inicio": "2024-02-05",
      "fecha_fin": null,
      "estado": "Activo",
      "resultado": "Respuesta parcial"
    },
    {
      "id_historia": "HT007",
      "id_paciente": "PAC005",
      "id_tratamiento": "TRA001",
      "fecha_inicio": "2024-01-18",
      "fecha_fin": null,
      "estado": "Activo",
      "resultado": "Presión controlada"
    }
]);
```

12. Creacion de la colección ("medicamento_tratamiento"):
```js
db.createCollection("historia_tratamiento", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["_id", "nombre", "id_hospital"],
      properties: {
        _id: { bsonType: "string" },
        nombre: { bsonType: "string" },
        id_hospital: { bsonType: "string" }
      }
    }
  }
});
```

* Insertar datos a la colección medicamento_tratamiento:
```js
db.medicamento_tratamiento.insertMany([{
      "id_medicamento_tratamiento": "MT001",
      "id_medicamento": "MED001",
      "id_tratamiento": "TRA001",
      "dosis": "500mg cada 8 horas",
      "frecuencia": "3 veces al día"
    },
    {
      "id_medicamento_tratamiento": "MT002",
      "id_medicamento": "MED004",
      "id_tratamiento": "TRA001",
      "dosis": "10mg cada 12 horas",
      "frecuencia": "2 veces al día"
    },
    {
      "id_medicamento_tratamiento": "MT003",
      "id_medicamento": "MED005",
      "id_tratamiento": "TRA004",
      "dosis": "200mg cada 12 horas",
      "frecuencia": "2 veces al día"
    },
    {
      "id_medicamento_tratamiento": "MT004",
      "id_medicamento": "MED002",
      "id_tratamiento": "TRA013",
      "dosis": "500mg cada 8 horas",
      "frecuencia": "3 veces al día"
    },
    {
      "id_medicamento_tratamiento": "MT005",
      "id_medicamento": "MED006",
      "id_tratamiento": "TRA009",
      "dosis": "20mg en ayunas",
      "frecuencia": "1 vez al día"
    },
    {
      "id_medicamento_tratamiento": "MT006",
      "id_medicamento": "MED007",
      "id_tratamiento": "TRA011",
      "dosis": "850mg con las comidas",
      "frecuencia": "2 veces al día"
    },
    {
      "id_medicamento_tratamiento": "MT007",
      "id_medicamento": "MED008",
      "id_tratamiento": "TRA007",
      "dosis": "100mcg cada 6 horas",
      "frecuencia": "4 veces al día"
    },
    {
      "id_medicamento_tratamiento": "MT008",
      "id_medicamento": "MED018",
      "id_tratamiento": "TRA019",
      "dosis": "50mg/m2 cada 21 días",
      "frecuencia": "Ciclos de quimioterapia"
    }
]);
```

13. Creacion de la colección ("facturas"):
```js
db.createCollection("faturas", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["_id", "nombre", "id_hospital"],
      properties: {
        _id: { bsonType: "string" },
        nombre: { bsonType: "string" },
        id_hospital: { bsonType: "string" }
      }
    }
  }
});
```

* Insertar datos a la colección facturas:
```js
db.facturas.insertMany([{
      "id_factura": "FAC001",
      "id_paciente": "PAC001",
      "fecha_emision": "2024-01-15",
      "total": 230000
    },
    {
      "id_factura": "FAC002",
      "id_paciente": "PAC002",
      "fecha_emision": "2024-01-22",
      "total": 980000
    },
    {
      "id_factura": "FAC003",
      "id_paciente": "PAC003",
      "fecha_emision": "2024-01-28",
      "total": 170000
    },
    {
      "id_factura": "FAC004",
      "id_paciente": "PAC004",
      "fecha_emision": "2024-02-05",
      "total": 2500000
    },
    {
      "id_factura": "FAC005",
      "id_paciente": "PAC005",
      "fecha_emision": "2024-01-18",
      "total": 150000
    },
    {
      "id_factura": "FAC006",
      "id_paciente": "PAC006",
      "fecha_emision": "2024-02-12",
      "total": 180000
    },
    {
      "id_factura": "FAC007",
      "id_paciente": "PAC007",
      "fecha_emision": "2024-01-25",
      "total": 100000
    },
    {
      "id_factura": "FAC008",
      "id_paciente": "PAC008",
      "fecha_emision": "2024-02-08",
      "total": 300000
    },
    {
      "id_factura": "FAC009",
      "id_paciente": "PAC009",
      "fecha_emision": "2024-01-30",
      "total": 240000
    }
]);
```

14. Creacion de la colección ("datalle_factura"):
```js
db.createCollection("detalle_factura", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["_id", "nombre", "id_hospital"],
      properties: {
        _id: { bsonType: "string" },
        nombre: { bsonType: "string" },
        id_hospital: { bsonType: "string" }
      }
    }
  }
});
```

* Insertar datos a la colección detalle_factura:
```js
db.detalle_factura.insertMany([ {
      "id_detalle": "DET001",
      "id_factura": "FAC001",
      "id_tratamiento": "TRA001",
      "cantidad": 1,
      "subtotal": 150000
    },
    {
      "id_detalle": "DET002",
      "id_factura": "FAC001",
      "id_tratamiento": "TRA002",
      "cantidad": 1,
      "subtotal": 80000
    },
    {
      "id_detalle": "DET003",
      "id_factura": "FAC002",
      "id_tratamiento": "TRA004",
      "cantidad": 1,
      "subtotal": 180000
    },
    {
      "id_detalle": "DET004",
      "id_factura": "FAC002",
      "id_tratamiento": "TRA005",
      "cantidad": 1,
      "subtotal": 800000
    },
    {
      "id_detalle": "DET005",
      "id_factura": "FAC003",
      "id_tratamiento": "TRA013",
      "cantidad": 1,
      "subtotal": 120000
    },
    {
      "id_detalle": "DET006",
      "id_factura": "FAC003",
      "id_tratamiento": "TRA014",
      "cantidad": 1,
      "subtotal": 50000
    },
    {
      "id_detalle": "DET007",
      "id_factura": "FAC004",
      "id_tratamiento": "TRA019",
      "cantidad": 1,
      "subtotal": 2500000
    },
    {
      "id_detalle": "DET008",
      "id_factura": "FAC005",
      "id_tratamiento": "TRA001",
      "cantidad": 1,
      "subtotal": 150000
    },
    {
      "id_detalle": "DET009",
      "id_factura": "FAC006",
      "id_tratamiento": "TRA004",
      "cantidad": 1,
      "subtotal": 180000
    },
    {
      "id_detalle": "DET010",
      "id_factura": "FAC007",
      "id_tratamiento": "TRA007",
      "cantidad": 1,
      "subtotal": 100000
    },
    {
      "id_detalle": "DET011",
      "id_factura": "FAC008",
      "id_tratamiento": "TRA009",
      "cantidad": 1,
      "subtotal": 300000
    },
    {
      "id_detalle": "DET012",
      "id_factura": "FAC009",
      "id_tratamiento": "TRA011",
      "cantidad": 1,
      "subtotal": 160000
    },
    {
      "id_detalle": "DET013",
      "id_factura": "FAC009",
      "id_tratamiento": "TRA012",
      "cantidad": 1,
      "subtotal": 80000
    }
]);
```
