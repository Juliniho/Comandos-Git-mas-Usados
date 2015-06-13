# **Formato de Archivo**
Los archivos deberían guardarse con codificación Unicode (UTF-8). No debería usarse el BOM. A diferencia de UTF-16 y UTF-32, no hay un bit de orden para indicar en un archivo codificado con UTF-8, y el BOM puede tener efectos colaterales negativos en PHP en el envío de la salida, evitando que la aplicación sea capaz de establecer sus encabezados. Se deberían usar las terminaciones de línea de Unix (LF). 
Esta es la forma de aplicar esas configuraciones en los editores de texto más comunes. Las instrucciones para su editor de texto pueden variar; lea la documentación de su editor.
### TextMate
1. Abra las Preferencias de la Aplicación
2. Hacer clic en Avanzado, y luego en la solapa "Guardar"
3. En "Codificación de Archivo", seleccione "UTF-8 (recomendado)"
4. En "Terminación de Línea", seleccione "LF (recomendado)"
5. Opcional: Marque "También usar para los archivos existentes" si desea modificar las terminaciones de línea de archivos que abre para las nuevas preferencias.

### BBEdit
1. Abra las Preferencias de la Aplicación
2. Seleccione "Codificaciones del Texto" en la izquierda.
3. En "Codificación del texto para nuevos documentos", seleccione "Unicode (UTF-8, sin BOM)"
4. Opcional: En "Si no se puede determinar la codificación del archivo, usar", seleccione "Unicode (UTF-8, sin BOM)"
5. Selecciones "Archivos de Texto" en la izquierda.
6. En "Saltos de Línea por Defecto", seleccione "Mac OS X y Unix (LF)"

# **Etiqueta de Cierre de PHP**
La etiqueta de cierre de PHP en un documento PHP ```?>``` es opcional para el analizador de PHP. Sin embargo, si se usa, cualquier espacios en blanco que siga a la etiqueta de cierre, sea introducida por el desarrollador, el usuario o una aplicación FTP, puede causar una salida no deseada, errores de PHP, o si la última se suprime, páginas en blanco. Por esta razón, todos los archivos de PHP deberían **OMITIR** la etiqueta de cierre de PHP, y en su lugar usar un bloque de comentario para marcar el fin del archivo y su ubicación relativa a la raíz de la aplicación. Esto le permite aún identificar al archivo como completo y no trunco.
## INCORRECTO:
```
<?php

echo "Este es mi código!";

?>
```
## CORRECTO:
```
<?php

echo "Este es mi código!";

/* Fin del archivo mi_archivo.php */
/* Ubicación: ./system/modules/mi_modulo/mi_archivo.php */
```
# **Nomenclatura de Clases y Métodos**
Los nombres de clases siempre deberían comenzar con una letra mayúscula. Varias palabras se deberían separar con un guión de subrayado y no usar CamelCase. Todos los otros métodos de clase se deberían escribir completamente en minúsculas y su nombre debería indicar claramente su función, incluyendo preferiblemente un verbo. Trate de evitar los nombres demasiado largos y detallados.
## INCORRECTO:
```
class superclass
class SuperClass
```
## CORRECTO:
```
class Super_class
```
```
class Super_class {

	function __construct()
	{

	}
}
```
Ejemplos de una nomenclatura de métodos adecuada e inadecuada:
## INCORRECTO:
```
function fileproperties()					// no es descriptivo y necesita un guión de subrayado de separación
function fileProperties()					// no es descriptivo y usa CamelCase
function getfileproperties()					// Mejor! Pero todavía le falta el guión de subrayado de separación
function getFileProperties()					// usa CamelCase
function get_the_file_properties_from_the_file()	// demasiada palabrería
```
## CORRECTO:
```
function get_file_properties()	// descriptivo, guión de subrayado de separación y todas la letras son minúsculas
```
# **Nombres de Variable**
La directriz para el nombramiento de variables es muy similar al usado para métodos de clase. Concretamente, las variables deberían contener solamente letras minúsculas, usar guiones de subrayado como separadores y tener un nombre que razonablemente indique su propósito y contendo. Variables de nombre muy corto o sin palabras se deberían usar solamente como iteradores en ciclos **for()**.
## INCORRECTO:
```
$j = 'foo';				//las variables de una sola letra se deberían usar solamente en ciclos for()
$Str					// contiene letras mayúsculas
$bufferedText			// usas CamelCase y podría acortarse sin perder sentido semántico
$groupid				// varias palabras, necesita un separador de guión de subrayado
$name_of_last_city_used	// demasiado largo
```
## CORRECTO:
```
for ($j = 0; $j < 10; $j++)
$str
$buffer
$group_id
$last_city
```
# **Comentarios**
En general, el código debe ser comentado de forma prolífica. No sólo ayuda a describir el flujo y la intención del código para los programadores con menos experiencia, sino que puede resultar muy valiosa al regresar a su propio código meses después en línea. No hay un formato establecido para comentarios, pero se recomienda lo siguiente.  
Estilo de comentarios [DocBlock](http://manual.phpdoc.org/HTMLSmartyConverter/HandS/phpDocumentor/tutorial_phpDocumentor.howto.pkg.html#basics.docblock) que precede declaraciones de clases y métodos, que puede ser levantado por los IDEs:
```
/**
 * Super Class
 *
 * @package	Nombre del paquete
 * @subpackage	Subpaquete
 * @category	Categoría
 * @author		Nombre del autor
 * @link		http://ejemplo.com
 */
class Super_class {
```
```
/**
 * Codifica una cadena para usarla en XML
 *
 * @access	public
 * @param	string
 * @return	string
 */
function xml_encode($str)
```
Usar comentarios en línea simple dentro del código, dejando una línea en blanco entre un bloque largo de comentarios y el código.
```
// rompe las cadenas mediante caracteres de nueva línea
$parts = explode("\n", $str);

// Un comentario más grande de lo que necesita para dar un gran detalle de lo que
// está ocurriendo y porque puede usar varios comentarios de línea simple. Trate
// de mantener un ancho razonable, alrededor de 70 caracteres es más fácil para
// leer. No dude en vincular recursos externos que pueden proveer grandes
// detalles:
//
// http://ejemplo.com/informacion_acerca_de_algo/en_particular/

$parts = $this->foo($parts);
```
# **Constantes**
Las constantes siguen las mismas directrices que las variables, excepto que las constantes siempre deberían escribirse completamente en mayúsculas. Siempre usar constantes de CodeIgniter cuando sea adecuado, por ejemplo, SLASH, LD, RD, PATH_CACHE, etc.
## INCORRECTO:
```
myConstant					// missing underscore separator and not fully uppercase
N							// no single-letter constants
S_C_VER						// not descriptive
$str = str_replace('{foo}', 'bar', $str);	// should use LD and RD constants
```
## CORRECTO:
```
MY_CONSTANT
NEWLINE
SUPER_CLASS_VERSION
$str = str_replace(LD.'foo'.RD, 'bar', $str);
```
# **TRUE, FALSE y NULL**
Las palabras clave **TRUE**, **FALSE** y **NULL** siempre deberían escribirse completamente en mayúsculas.
## INCORRECTO:
```
if ($foo == true)
$bar = false;
function foo($bar = null)
```
## CORRECTO:
```
if ($foo == TRUE)
$bar = FALSE;
function foo($bar = NULL)
Operadores Lógicos
```
Se desaconseja el uso de **||** dado que la claridad de algunos dispositivos de salida es baja (por ejemplo, podría verse como el número 11). Es preferible **&&** en lugar de AND pero ambos son aceptables y un espacio siempre debería preceder y seguir a **!**.
## INCORRECTO:
```
if ($foo || $bar)
if ($foo AND $bar)  // okay but not recommended for common syntax highlighting applications
if (!$foo)
if (! is_array($foo))
```
## CORRECTO:
```
if ($foo OR $bar)
if ($foo && $bar) // recommended
if ( ! $foo)
if ( ! is_array($foo))
```
# **Operadores Lógicos**
Se desaconseja el uso de || dado que la claridad de algunos dispositivos de salida es baja (por ejemplo, podría verse como el número 11). Es preferible && en lugar de AND pero ambos son aceptables y un espacio siempre debería preceder y seguir a !.
## INCORRECTO:
```
if ($foo || $bar)
if ($foo AND $bar)  // okay but not recommended for common syntax highlighting applications
if (!$foo)
if (! is_array($foo))
```
## CORRECTO:
```
if ($foo OR $bar)
if ($foo && $bar) // recommended
if ( ! $foo)
if ( ! is_array($foo))
```
# **Comparar Valores de Retorno y Typecasting**
Algunas funciones de PHP devuelven FALSE en caso de falla, pero también puede haber un valor de retorno válido de **""** o **0**, lo que se evaluaría como FALSE en comparaciones poco precisas. Sea explícito al comparar el tipo de variable al usar esos valores de retorno en condicionales para asegurar que el valor de retorno es en realidad lo que espera, y no un valor que tiene un equivalente de evaluación de tipo relajado. 
Use el mismo rigor cuando en el retorno y verificación de sus propias variables. Use **===** y **!==** según sea necesario.
## INCORRECTO:
```
// Si 'foo' está al inicio de la cadena, strpos devolverá un 0,
// resultando esta evaluación condicional como TRUE
if (strpos($str, 'foo') == FALSE)
```
## CORRECTO:
```
if (strpos($str, 'foo') === FALSE)
```
## INCORRECTO:
```
function build_string($str = "")
{
	if ($str == "")	 // oh-oh! ¿Qué ocurre si se pasa como argumento FALSE o el entero 0?
	{

	}
}
```
## CORRECTO:
```
function build_string($str = "")
{
	if ($str === "")
	{

	}
}
```
Vea también acerca del [typecasting](http://us3.php.net/manual/en/language.types.type-juggling.php#language.types.typecasting), lo que puede ser muy útil. El typecasting tiene un efecto ligeramente distinto que puede ser deseable. Al convertir una variable a una cadena, por ejemplo, las variables **NULL** y **FALSE** se convierten en cadenas vacías, 0 (y otros números) se convierten en cadenas de dígitos, y el booleano **TRUE** se convierte en "1":
```
$str = (string) $str;	// trata a $str como una cadena
```
# **Código de Depuración**
No se puede dejar código de depuración en el lugar a menos que se lo comente, por ejemplo, ninguna llamada a ***var_dump()***, ***print_r()***, ***die()***, o ***exit()*** usada durante la creación de un complemento.
```
// print_r($foo);
```
# **Espacios en Blanco en Archivos**

Los espacios en blanco no pueden preceder a la etiqueta de apertura de PHP o seguir a la etiqueta de cierre de PHP. La salida se almacena en búfer, por lo tanto los espacios en blanco en sus archivos pueden provocar que la salida comience antes que CodeIgniter imprima su contenido, conduciendo a errores y a la incapacidad de CodeIgniter de enviar los encabezados adecuados. En el siguiente ejemplo, seleccione el texto con el ratón para revelar los espacios en blanco INCORRECTOS.
## INCORRECTO:
```
(espacio en blanco)
<?php
	// ...hay un espacio en blanco y un salto de línea antes de la etiqueta de
	// apertura de PHP
	// así como un espacio en blanco después de la etiqueta de cierre de PHP
?>
(espacio en blanco)
```
## CORRECTO:
```
<?php
	// este ejemplo no tiene espacios en blanco antes o después de las etiquetas
	// de apertura y cierre de PHP
?>
```
# **Compatibilidad**
A menos que sea mencionado específicamente en la documentación de su complemento, todo código tiene que ser compatible con PHP versión 4.3 o superior. Además, no usar funciones de PHP que necesiten instalar de bibliotecas no estándares, a menos que su código contenga un método alternativo cuando la función no esté disponible, o implícitamente documente que su complemento necesita dichas bibliotecas de PHP.
# **Nombres de Clases y Archivos usando Palabras Comunes**
Cuando su clase o nombre de archivo son una palabra común, o puede ser bastante probable que nombre igual en otro script de PHP, proveer un prefijo único para ayudar a impedir esa colisión. Siempre darse cuenta que sus usuarios finales pueden ejecutar otros complementos o scripts de PHP o de terceras partes. Elija un prefijo que sea único para identificarlo como desarrollador o compañía.
## INCORRECTO:
```
class Email		pi.email.php
class Xml		ext.xml.php
class Import		mod.import.php
```
## CORRECTO:
```
class Pre_email		pi.pre_email.php
class Pre_xml		ext.pre_xml.php
class Pre_import	mod.pre_import.php
```
# **Nombres de Tablas de Base de Datos**
Cualquier tabla que su complemento pueda usar tiene que tener el prefijo '***exp_***', seguido por un prefijo de unicidad que lo identifique a Ud como desarrollador o compañía, y luego un breve nombre descriptivo de tabla. No necesita preocuparse acerca del prefijo de base de datos que se usa en la instalación del usuario, ya que la clase database de CodeIgniter convertirá automáticamente '***exp_***' a lo que realmente se usa.
## INCORRECTO:
```
email_addresses		// faltan ambos prefijos
pre_email_addresses	// falta el prefijo exp_
exp_email_addresses	// falta el prefijo único
```
## CORRECTO:
```
exp_pre_email_addresses
```
**Nota:** Tenga en cuenta que MySQL tiene un límite de 64 caracteres para los nombres de tablas. Esto no debería ser un problema, ya que los nombres de tablas que superan esa cantidad probablemente no tengan nombres razonables. Por ejemplo, el siguiente nombre de tabla excede esta limitación por un caracter. Tonto ¿no? **exp_pre_email_addresses_of_registered_users_in_seattle_washington**
$ **Un Archivo por Clase**
Usar archivos separados para cada clase que su complemento use, a menos que las clases estén estrechamente relacionadas. Un ejemplo de archivos de CodeIgniter que contienen varias clases es el archivo de la clase ***Database***, que contiene tanto a la clase ***DB*** como a la clase ***DB_Cache***, y el complemento ***Magpie***, que contiene tanto a la clase ***Magpie*** como a ***Snoopy***.
# **Espacios en Blanco**
Usar tabuladores en lugar de espacios en blanco en su código. Esto puede parecer una pequeñez, pero usando tabuladores en lugar de espacios en blanco le permite al desarrollador que mira su código para tener indentación en los niveles que prefiera y personalizar en cualquier aplicación que use. Y como beneficio colateral, resulta en archivos (un poco) más compactos, almacenando un caracter de tabulador contra, digamos, cuatro caracteres de espacio.
# **Saltos de Línea**
Los archivos se tienen que guardar con saltos de línea de Unix. Esto es más un problema para los desarrolladores que trabajan en Windows, pero en cualquier caso, asegúrese de que su editor de texto está configurado para guardar los archivos con saltos de línea de Unix.
# **Indentación de Código**
Usar el estilo de indentación de Allman. Con excepción de las declaraciones de clase, las llaves siempre se ubican en línea con ellas mismas, e indentadas al mismo nivel que las sentencias de control que las "poseen".
## INCORRECTO:
```
function foo($bar) {
	// ...
}

foreach ($arr as $key => $val) {
	// ...
}

if ($foo == $bar) {
	// ...
} else {
	// ...
}

for ($i = 0; $i < 10; $i++)
	{
	for ($j = 0; $j < 10; $j++)
		{
		// ...
		}
	}
```
## CORRECTO:
```
function foo($bar)
{
	// ...
}

foreach ($arr as $key => $val)
{
	// ...
}

if ($foo == $bar)
{
	// ...
}
else
{
	// ...
}

for ($i = 0; $i < 10; $i++)
{
	for ($j = 0; $j < 10; $j++)
	{
		// ...
	}
}
```
# **Espaciado de Paréntesis y Llaves**
En general, los paréntesis y las llaves no deberían usar espacios adicionales. La excepción es que un espacio siempre debería seguir a las estructuras de control de PHP que acepten argumentos entre paréntesis (declare, do-while, elseif, for, foreach, if, switch, while), para ayudar a distinguirlas de las funciones e incrementar la legibilidad.  
In general, parenthesis and brackets should not use any additional spaces. The exception is that a space should always follow PHP control structures that accept arguments with parenthesis (declare, do-while, elseif, for, foreach, if, switch, while), to help distinguish them from functions and increase readability.
## INCORRECTO:
```
$arr[ $foo ] = 'foo';
```
## CORRECTO:
```
$arr[$foo] = 'foo'; // no spaces around array keys
```
## INCORRECTO:
```
function foo ( $bar )
{

}
```
## CORRECTO:
```
function foo($bar) // no spaces around parenthesis in function declarations
{

}
```
## INCORRECTO:
```
foreach( $query->result() as $row )
```
## CORRECTO:
```
foreach ($query->result() as $row) // single space following PHP control structures, but not in interior parenthesis
```
# **Texto Localizado**
Cualquier texto que se muestre en el panel de control, debería usar variables de idioma en su archivo de idioma para permitir la localización
## INCORRECTO:
```
return "Invalid Selection";
```
## CORRECTO:
```
return $this->lang->line('invalid_selection');
Métodos Privados y Variables
```
Se deberían prefijar con un guión de subrayado los métodos y variables que solamente son accedidos internamente por su clase, tales como utilidades y helpers de funciones usan para abstracción del código.
```
convert_text()		// método público
_convert_text()		// método privado
```
# **Errores de PHP**
El código tiene que ejecutar libre de errores y no depender que las advertencias y avisos estén ocultos para cumplir con este requisito. Por ejemplo, nunca acceder una variable que no estableció por si mismo (tal como claves del array $_POST), sin primero verificar si están establecidas con isset().  
Asegurarse que durante el desarrollo de su complemento, el reporte de errores esté habilitado para TODOS los usuarios y que display_errors está habilitado en el entorno de PHP. Puede verificar esto con:
```
if (ini_get('display_errors') == 1)
{
	exit "Enabled";
}
```
En algunos servidores donde display_errors está deshabilitado, y no tiene la posibilidad de cambiar esto en el php.ini, a menudo se puede habilitar con:
```
ini_set('display_errors', 1);
```
NOTA: Establecer el parámetro ***display_errors*** con ini_set() en tiempo de ejecución, no es lo mismo que tenerlo habilitado en el entorno de PHP. Es decir, no tendrá ningún efecto si el script contiene errores fatales.
# **Etiquetas de Apertura Cortas**
Usar siempre etiquetas de apertura de PHP completas, en caso que el servidor no tenga habilitada la directiva short_open_tag.
## INCORRECTO:
```
<? echo $foo; ?>

<?=$foo?>
```
## CORRECTO:
```
<?php echo $foo; ?>
```
# **Una Sentencia por Línea**
Nunca combinar sentencias en una sola línea.
## INCORRECTO:
```
$foo = 'this'; $bar = 'that'; $bat = str_replace($foo, $bar, $bag);
```
## CORRECTO:
```
$foo = 'this';
$bar = 'that';
$bat = str_replace($foo, $bar, $bag);
# **Cadenas**
```
Siempre use cadenas de comillas simples a menos que necesite variables analizadas, y en casos donde necesite variables analizadas, use llaves para impedir ávidos análisis sintácticos de elementos. También puede usar cadenas de comillas dobles si la cadena contiene comillas simples, por lo tanto no hay necesidad de escapar caracteres.
## INCORRECTO:
```
"My String"							// no hay análisis de variables, por lo tanto no use comillas dobles
"My string $foo"						// se necesitan llaves
'SELECT foo FROM bar WHERE baz = \'bag\''	// repugnante
```
## CORRECTO:
```
'My String'
"My string {$foo}"
"SELECT foo FROM bar WHERE baz = 'bag'"
```
# **Consultas SQL**
Las palabras clave de MySQL se ponen siempre en mayúsculas: SELECT, INSERT, UPDATE, WHERE, AS, JOIN, ON, IN, etc. Dividir las consultar largas en varias líneas para darles legibilidad, preferiblemente cortando en cada cláusula.
## INCORRECTO:
```
// las palabras clave están en minúsculas y las consultas son demasiado largas
// para una línea simple (... indica continuación de línea)
$query = $this->db->query("select foo, bar, baz, foofoo, foobar as raboof, foobaz
...from exp_pre_email_addresses
...where foo != 'oof' and baz != 'zab' order by foobaz limit 5, 100");
```
## CORRECTO:
```
$query = $this->db->query("SELECT foo, bar, baz, foofoo, foobar AS raboof, foobaz
				FROM exp_pre_email_addresses
				WHERE foo != 'oof'
				AND baz != 'zab'
				ORDER BY foobaz
				LIMIT 5, 100");
```
# **Argumentos Por Defecto de Funciones**
Cuando sea adecuado, proveer argumentos por defecto a las funciones, que ayudan a evitar errores de PHP con llamadas erróneas y proveen valores comunes alternativos que pueden salvar unas pocas líneas de código. Ejemplo:
```
function foo($bar = '', $baz = FALSE)
```