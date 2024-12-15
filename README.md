-- Creación de la tabla Cliente
CREATE TABLE Cliente (
    ID_Cliente INT PRIMARY KEY,
    Nombre VARCHAR(100) NOT NULL,
    Telefono VARCHAR(20),
    Correo VARCHAR(100),
    Experiencia VARCHAR(50)
);

-- Creación de la tabla Propietario
CREATE TABLE Propietario (
    ID_Propietario INT PRIMARY KEY,
    Nombre VARCHAR(100) NOT NULL,
    Telefono VARCHAR(20),
    Correo VARCHAR(100)
);

-- Creación de la tabla Barco
CREATE TABLE Barco (
    ID_Barco INT PRIMARY KEY,
    Tamano INT NOT NULL,
    Modelo VARCHAR(50) NOT NULL,
    Estado VARCHAR(20) NOT NULL,
    ID_Propietario INT NOT NULL,
    FOREIGN KEY (ID_Propietario) REFERENCES Propietario(ID_Propietario)
);

-- Creación de la tabla Equipo
CREATE TABLE Equipo (
    ID_Equipo INT PRIMARY KEY,
    Nombre_Equipo VARCHAR(100) NOT NULL,
    Tipo_Equipo VARCHAR(50) NOT NULL,
    Cantidad INT NOT NULL,
    ID_Barco INT NOT NULL,
    FOREIGN KEY (ID_Barco) REFERENCES Barco(ID_Barco)
);

-- Creación de la tabla Viaje
CREATE TABLE Viaje (
    ID_Viaje INT PRIMARY KEY,
    Fecha_Inicio DATE NOT NULL,
    Fecha_Fin DATE NOT NULL,
    Destino VARCHAR(100) NOT NULL,
    Estado VARCHAR(20) NOT NULL,
    ID_Cliente INT NOT NULL,
    ID_Barco INT NOT NULL,
    FOREIGN KEY (ID_Cliente) REFERENCES Cliente(ID_Cliente),
    FOREIGN KEY (ID_Barco) REFERENCES Barco(ID_Barco)
);

-- Creación de la tabla Tripulacion
CREATE TABLE Tripulacion (
    ID_Tripulante INT PRIMARY KEY,
    Nombre_Tripulante VARCHAR(100) NOT NULL,
    Costo_Hora DECIMAL(10,2) NOT NULL
);

-- Creación de la tabla Mantenimiento
CREATE TABLE Mantenimiento (
    ID_Mantenimiento INT PRIMARY KEY,
    Fecha DATE NOT NULL,
    Tipo VARCHAR(50) NOT NULL,
    Costo DECIMAL(10,2) NOT NULL,
    Descripcion TEXT,
    ID_Barco INT NOT NULL,
    FOREIGN KEY (ID_Barco) REFERENCES Barco(ID_Barco)
);

-- Tabla intermedia para la relación muchos a muchos entre Tripulacion y Viaje
CREATE TABLE Tripulacion_Viaje (
    ID_Tripulante INT NOT NULL,
    ID_Viaje INT NOT NULL,
    PRIMARY KEY (ID_Tripulante, ID_Viaje),
    FOREIGN KEY (ID_Tripulante) REFERENCES Tripulacion(ID_Tripulante),
    FOREIGN KEY (ID_Viaje) REFERENCES Viaje(ID_Viaje)
);
