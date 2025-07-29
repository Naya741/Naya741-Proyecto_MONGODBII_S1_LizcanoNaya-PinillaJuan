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

❖ nombre: VARCHAR(100) NOT NULL.

❖ documento: VARCHAR(20)  UNIQUE NOT NULL.

❖ rol: VARCHAR(100)  ENUM (‘Médico’, ‘Enfermero’, ‘Administrativo’, ‘Mantenimiento’) NOT NULL.

❖ especialidad: VARCHAR(100) 

❖ correo: VARCHAR(100) 

❖ telefono: VARCHAR(20) 

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









