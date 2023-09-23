--@block
CREATE TABLE Localidad(
    Id_localidad INT PRIMARY KEY AUTO_INCREMENT,
    Nombre VARCHAR(20),
    Poblacion INT
); --run :d

--@block
CREATE TABLE Barrio(
    Id_Barrio INT PRIMARY KEY AUTO_INCREMENT,
    Nombre VARCHAR(30),
    Id_localidad INT FOREIGN KEY (Id_localidad) REFERENCES Localidad (Id_localidad)
    Id_Aplicacion INT FOREIGN KEY (Id_Aplicacion) REFERENCES Aplicacion_Denuncia (Id_Aplicacion),
    ZIP_code VARCHAR(10),
    Estrato INT,
    Id_aplicacion INT
);

--@block
CREATE TABLE Indicador(
    ID_Indicador INT PRIMARY KEY AUTO_INCREMENT,
    Nombre VARCHAR(20),
    Descripcion VARCHAR(100)
); --run :d

--@block
CREATE TABLE Factor_Social (
    ID_Factor INT PRIMARY KEY AUTO_INCREMENT,
    Nombre VARCHAR(20),
    Descripcion VARCHAR(100)
); --run :d

--@block
CREATE TABLE Adolescente(
    ID_Adolescente INT PRIMARY KEY AUTO_INCREMENT,
    Edad SMALLINT,
    Estrato NUMBER(1),
    ID_Factor INT FOREIGN KEY AUTO_INCREMENT REFERENCES Factor_Social
);

--@block
CREATE TABLE Estructura_Criminal (
    ID_Estructura INT PRIMARY KEY AUTO_INCREMENT,
    Descripcion VARCHAR(100)
); --run :d

--@block
CREATE TABLE Victima_Violencia (
    ID_Victima INT PRIMARY KEY AUTO_INCREMENT,
    Tipo_Delito VARCHAR(30),
    Descripcion VARCHAR(100),
    Genero CHAR(1),
    Edad NUMBER(1)
);

--@block
CREATE TABLE Delincuente_Juvenil (
    ID_Delincuente INT PRIMARY KEY,
    Edad SMALLINT
); -- run :d

--@block
CREATE TABLE Aplicacion_Denuncia (
    ID_Aplicacion INT PRIMARY KEY AUTO_INCREMENT,
    Descripcion VARCHAR(100),
    Entidad_Denunciante VARCHAR(30)
);

--@block
CREATE TABLE Adolescente_EstructuraCriminal (
    ID_Adolescente INT PRIMARY KEY AUTO_INCREMENT,
    ID_Estructura INT PRIMARY KEY AUTO_INCREMENT,

    ID_Adolescente INT FOREIGN KEY AUTO_INCREMENT REFERENCES Adolescente,
    ID_Estructura INT FOREIGN KEY AUTO_INCREMENT REFERENCES Estructura_Criminal
);
--@block
CREATE TABLE VictimaViolencia_DelincuenteJuvenil (
    ID_Victima INT PRIMARY KEY AUTO_INCREMENT,
    ID_Delincuente INT PRIMARY KEY AUTO_INCREMENT,
    ID_Victima INT FOREIGN KEY AUTO_INCREMENT REFERENCES Victima_Violencia,
    ID_Delincuente INT FOREIGN KEY AUTO_INCREMENT REFERENCES Delincuente_Juvenil
);

--@block
ALTER TABLE Barrio ADD CONSTRAINT FK_Barrio_Localidad FOREIGN KEY (ID_Localidad) REFERENCES Localidad (ID_Localidad);
ALTER TABLE Barrio ADD CONSTRAINT FK_Barrio_Aplicacion_Denuncia FOREIGN KEY (ID_Aplicacion) REFERENCES Aplicacion_Denuncia (ID_Aplicacion);
