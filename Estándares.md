# 1. CodeIgniter
## 1.1. Nombres de Controladores
### 1.1.1. Archivos
* nombres escritos en minúsculas.
* deben de ser nombres en plural.
* el nombre debe tener significado nemónico
* las palabras van separadas por guion bajo ```_```.
* ejemplos: ```usuarios.php```, ```centros_educativos.php```.
### 1.1.2. Clases
* se debe de llamar igual que el archivo ```php```.
* la primera letra es en mayúscula y el resto es en minúsculas.
* las palabras van separadas por guion bajo ```_```.
* solo la primera letra de la primera palabra será mayúscula.
* ejemplos: ```Usuarios```, ```Centros_educativos```.
## 1.2. Nombres de Modelos
### 1.2.1. Archivos
* nombres escritos en minúsculas.
* deben de ser nombres en plural.
* el nombre debe tener significado nemónico
* las palabras van separadas por guion bajo ```_```.
* incluir el postfijo ```_model``` después del nombre.
* ejemplos: ```usuarios_model.php```, ```centros_educativos_model.php```.
### 1.2.2. Clases
* se debe de llamar igual que el archivo ```php```.
* la primera letra es en mayúscula y el resto es en minúsculas.
* las palabras van separadas por guion bajo ```_```.
* solo la primera letra de la primera palabra será mayúscula.
* ejemplos: ```Usuarios_model```, ```Centros_educativos_model```.
### 1.2.3. Carga
* al cargar (o llamar) un modelo, debe tener el mismo nombre que el archivo ```php``` en minúsculas.
* ejemplos: $this->load->model('```usuarios_model```');, $this->load->model('```centros_educativos_model```');
## 1.3. Nombres de Vistas
### 1.3.1. Archivos
* nombres escritos en minúsculas.
* deben de ser nombres en plural.
* el nombre debe tener significado nemónico
* las palabras van separadas por guion bajo ```_```.
* incluir el postfijo ```_view``` después del nombre.
* ejemplos: ```usuarios_view.php```, ```centros_educativos_view.php```.
### 1.3.2. Carga
* al cargar (o llamar) una vista, debe tener el mismo nombre que el archivo ```php``` en minúsculas.
* ejemplos: $this->load->view('```usuarios_view```');, $this->load->view('```centros_educativos_view```');
## [1.4. Estilo y Sintaxis](https://bitbucket.org/titiushko/syscap/wiki/Estilo%20y%20Sintaxis%20Generales%20de%20PHP%20con%20CodeIgniter%20)
# 2. MySQL
## 2.1. Nombres de Tablas
* estar escrito en plural.
* escrito en letras minúsculas.
* tener significado nemónico.
* las palabras van separadas por guion bajo ```_```.
* ejemplos: ```usuarios```, ```centros_educativos```.
## 2.2. Nombres de Campos
* estar escrito en singular.
* escrito en letras minúsculas.
* tener significado nemónico.
* tener como postfijo el nombre de la tabla en singular.
* la llave primaria de una tabla tiene el prefijo ```id_```, seguido del nombre de la tabla en singular.
* la llave primaria es auto numérico.
* la llave secundaria o foránea en una tabla es el nombre de la llave primaria de la tabla a la que pertenece.
* ejemplos: ```nombre_usuario```, ```codigo_centro_educativo```, ```id_usuario```.
## 2.3. Nombre de Relación entre Tablas
* incluir el prefijo ```fk_``` seguido del nombre de la tabla secundaria y el nombre de la tabla primaria.
* escrito en letras minúsculas.
* ejemplo si centros_educativos (tabla secundaria) y departamentos (tabla primaria): ```fk_centros_educativos_departamentos```.
## 2.4. Nombre de Rutinas
* debe ser un verbo seguido de uno o más sustantivos.
* utilizar el estilo de escritura ```CamelCase```.
### 2.4.1. Variables
* dentro de un bloque, inician con el prefijo ```v_```, ejemplo: ```v_nombre```.
* pasadas como parámetros, inician con el prefijo ```p_```, ejemplo: ```p_codigo```.
### 2.4.2. Cursores
* inician con el prefijo ```c_```.
* ejemplo: ```c_nombre```.
* sintaxis:  
```
#!sql

DECLARE c_nombre CURSOR FOR
	SELECT CONCAT(first_name,' ',last_name) nombre
	FROM employees
	WHERE employee_id = p_codigo_empleado;
```  
* [Más sobre cursores](http://dev.mysql.com/doc/refman/5.7/en/declare-cursor.html)
### 2.4.3. Procedimientos
* iniciar con el prefijo ```P_```.
* ejemplo: ```P_ConsultarCentrosEducativos```.
* sintaxis:  
```
#!sql

DELIMITER $$
CREATE PROCEDURE P_EliminarEmpleado(p_codigo_empleado INTEGER(6), OUT p_resultado VARCHAR(255))
NOT DETERMINISTIC
SQL SECURITY DEFINER
COMMENT 'procedimiento que elimina un empleado'
BEGIN
	DELETE FROM employees WHERE employee_id = p_codigo_empleado;
	COMMIT;
	SET p_resultado = 'Se elimino correctamente el empleado.';
END;
$$
DELIMITER ;
```  
* [Más sobre procedimientos](http://dev.mysql.com/doc/refman/5.6/en/create-procedure.html)
### 2.4.4. Funciones
* iniciar con el prefijo ```F_```.
* ejemplo: ```F_NombreCentroEducativo```.
* sintaxis:  
```
#!sql

DELIMITER $$
CREATE FUNCTION F_NombreCompleto(p_codigo_empleado INTEGER(6)) RETURNS VARCHAR(100)
NOT DETERMINISTIC
SQL SECURITY DEFINER
COMMENT 'funcion que devuelve el nombre completo de un empleado'
BEGIN
	DECLARE v_nombre VARCHAR(100);
	-- DECLARE v_termina BOOL DEFAULT FALSE;
	DECLARE v_termina INT DEFAULT FALSE;
	
	DECLARE c_nombre CURSOR FOR
		SELECT CONCAT(first_name,' ',last_name) nombre
		FROM employees
		WHERE employee_id = p_codigo_empleado;
	
	DECLARE CONTINUE HANDLER FOR NOT FOUND SET v_termina = TRUE;
	
	OPEN c_nombre;
	recorre_cursor: LOOP
		FETCH c_nombre INTO v_nombre;
		
		IF v_termina THEN
			LEAVE recorre_cursor;
		END IF;
		
	END LOOP;
	CLOSE c_nombre;
	
	RETURN v_nombre;
END;
$$
DELIMITER ;
```  
* [Más sobre funciones](http://dev.mysql.com/doc/refman/5.6/en/create-procedure.html)
### 2.4.5. Triggers
* iniciar con el prefijo ```T_```, seguido de la operación que realiza y el nombre de la tabla a la que pertenece.
* ejemplo: ```T_ActualizarCentroEducativo```.
* sintaxis:  
```
#!sql

DELIMITER $$
CREATE TRIGGER T_GenerarCorreoEmpleado BEFORE INSERT ON employees
FOR EACH ROW
-- NOT DETERMINISTIC
-- SQL SECURITY DEFINER
-- COMMENT ''
BEGIN
    DECLARE v_inicial_nombre VARCHAR(2) DEFAULT NULL;
    DECLARE v_apellido VARCHAR(25) DEFAULT NULL;
    
	SET v_inicial_nombre = UPPER(SUBSTRING_INDEX(NEW.first_name,1,1));
    SET v_apellido = UPPER(NEW.last_name);
    SET NEW.email = CONCAT(v_inicial_nombre,v_apellido);
END;
$$
DELIMITER ;
```  
* [Más sobre triggers](http://dev.mysql.com/doc/refman/5.6/en/create-trigger.html)
### 2.4.6. Vistas
* iniciar con el prefijo ```V_```.
* ejemplo: ```V_MunicipiosPorDepartamentos```.
* sintaxis:  
```
#!sql

DELIMITER $$
CREATE VIEW V_Usuarios AS
	SELECT u.id_usuario, u.nombre_usuario, u.contrasena_usuario, tu.nombre_tipo_usuario
	FROM usuarios u LEFT JOIN tipos_usuarios tu ON(u.id_tipo_usuario = tu.id_tipo_usuario);
$$
DELIMITER ;
```  
* [Más sobre vistas](http://dev.mysql.com/doc/refman/5.6/en/create-view.html)
### 2.4.7. Eventos
* iniciar con el prefijo ```E```.
* ejemplo: ```E_ActualizarFechaContratoEmpleados```.
* sintaxis:  
```
#!sql

DELIMITER $$
CREATE EVENT E_ActualizarFechaContratoEmpleados
ON SCHEDULE EVERY 1 MINUTE STARTS '2014-09-30 06:15:00'
DO
CALL P_ActualizarFechaContratoEmpleados(70);
$$
DELIMITER ;
```  
* [Más sobre eventos](http://dev.mysql.com/doc/refman/5.6/en/create-event.html)
# 3. CSS
## [3.1. Reglas](http://olgacarreras.blogspot.com/2009/07/25-reglas-para-hacer-css-accesibles.html)
## [3.2. Buenas Prácticas](http://webusable.com/bestPractices.htm)
## [3.3. Convenciones](http://disenowebakus.net/convenciones-de-escritura-en-css.php)
## [3.4. Sintaxis](http://www.htmlhelp.com/es/reference/css/structure.html)