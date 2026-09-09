# Biblioteca-
DROP DATABASE IF EXISTS biblioteca;
CREATE DATABASE biblioteca;
USE biblioteca;
CREATE TABLE usuarios (
    id_usuario SERIAL PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    apellido VARCHAR(100) NOT NULL,
    documento VARCHAR(20) UNIQUE NOT NULL,
    telefono VARCHAR(20),
    correo VARCHAR(100)
);

CREATE TABLE autores (
    id_autor SERIAL PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    apellido VARCHAR(100) NOT NULL
);

CREATE TABLE libros (
    id_libro SERIAL PRIMARY KEY,
    titulo VARCHAR(200) NOT NULL,
    isbn VARCHAR(20),
    anio_publicacion INT,
    id_autor INT,

    FOREIGN KEY (id_autor)
        REFERENCES autores(id_autor)
);

CREATE TABLE prestamos (
    id_prestamo SERIAL PRIMARY KEY,
    id_usuario INT NOT NULL,
    id_libro INT NOT NULL,
    fecha_prestamo DATE NOT NULL,
    fecha_devolucion DATE,

    FOREIGN KEY (id_usuario)
        REFERENCES usuarios(id_usuario),

    FOREIGN KEY (id_libro)
        REFERENCES libros(id_libro)
);

CREATE TABLE devoluciones (
    id_devolucion SERIAL PRIMARY KEY,
    id_prestamo INT NOT NULL,
    fecha_devolucion DATE NOT NULL,

    FOREIGN KEY (id_prestamo)
        REFERENCES prestamos(id_prestamo)
);

INSERT INTO usuarios 
(id_usuario, nombre, apellido, documento, telefono, correo)
VALUES
(1, 'Juan', 'Perez', '1001001001', '3001112233', 'juan.perez@gmail.com'),
(2, 'Maria', 'Gomez', '1001001002', '3012223344', 'maria.gomez@gmail.com'),
(3, 'Carlos', 'Rodriguez', '1001001003', '3023334455', 'carlos.rodriguez@gmail.com'),
(4, 'Laura', 'Martinez', '1001001004', '3034445566', 'laura.martinez@gmail.com'),
(5, 'Andres', 'Lopez', '1001001005', '3045556677', 'andres.lopez@gmail.com'),
(6, 'Sofia', 'Torres', '1001001006', '3056667788', 'sofia.torres@gmail.com'),
(7, 'Daniel', 'Hernandez', '1001001007', '3067778899', 'daniel.hernandez@gmail.com'),
(8, 'Valentina', 'Castro', '1001001008', '3078889900', 'valentina.castro@gmail.com');

INSERT INTO autores
(id_autor, nombre, apellido)
VALUES
(1, 'Gabriel', 'Garcia Marquez'),
(2, 'George', 'Orwell'),
(3, 'Julio', 'Cortazar'),
(4, 'Mario', 'Vargas Llosa'),
(5, 'Isabel', 'Allende'),
(6, 'Jorge Luis', 'Borges'),
(7, 'Stephen', 'King'),
(8, 'J.K.', 'Rowling');

INSERT INTO libros
(id_libro, titulo, isbn, anio_publicacion, id_autor)
VALUES
(1, 'Cien años de soledad', '9780307474728', 1967, 1),
(2, '1984', '9780451524935', 1949, 2),
(3, 'Rayuela', '9788437604947', 1963, 3),
(4, 'La ciudad y los perros', '9788420471839', 1963, 4),
(5, 'La casa de los espiritus', '9788401352836', 1982, 5),
(6, 'El Aleph', '9788420633121', 1949, 6),
(7, 'It', '9781501142970', 1986, 7),
(8, 'Harry Potter y la piedra filosofal', '9788478884453', 1997, 8),
(9, 'El amor en los tiempos del colera', '9780307389732', 1985, 1),
(10, 'Animal Farm', '9780451526342', 1945, 2);

INSERT INTO prestamos
(id_prestamo, id_usuario, id_libro, fecha_prestamo, fecha_devolucion)
VALUES
(1, 1, 1, '2026-08-01', '2026-08-10'),
(2, 2, 2, '2026-08-03', '2026-08-12'),
(3, 3, 3, '2026-08-05', '2026-08-15'),
(4, 4, 4, '2026-08-10', NULL),
(5, 5, 5, '2026-08-12', '2026-08-20'),
(6, 6, 6, '2026-08-15', NULL),
(7, 1, 8, '2026-08-18', '2026-08-25'),
(8, 7, 7, '2026-08-20', NULL),
(9, 8, 9, '2026-08-22', '2026-08-30'),
(10, 2, 10, '2026-08-25', NULL);

INSERT INTO devoluciones
(id_devolucion, id_prestamo, fecha_devolucion)
VALUES
(1, 1, '2026-08-10'),
(2, 2, '2026-08-12'),
(3, 3, '2026-08-15'),
(4, 5, '2026-08-20'),
(5, 7, '2026-08-25'),
(6, 9, '2026-08-30');
