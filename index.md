![Union europea](./images/union_europea.jpeg)  ![Generalitat](./images/generalitat.jpeg) ![Mare Nostrum](./images/mare_nostrum.png)


# Unidad 2. El lenguaje Dart

![Dart](./images/imagen1.png)

El framework **Flutter** hace uso del lenguaje **Dart**. 

En esta unidad vamos a hacer una breve introducción a este lenguaje y a sus principales características, con especial atención a la programación orientada a objetos, y a los mecanismos que se ofrecen para la programación asíncrona, de gran importancia en el desarrollo de interfaces dinámicas en Flutter.

[*1. Introducción a Dart*](#_apartado1)

[*2. Tipos de Datos*](#_apartado2)

[*3. Programación Estructurada*](#_apartado3)

[*4. Funciones*](#_apartado4)

[*5. Colecciones*](#_apartado5)

[*6. Programación Orientada a Objetos*](#_apartado6)

[*7. Programación Asíncrona*](#_apartado7)

[*8. Proyectos en Dart*](#_apartado8)

[*9. Peticiones HTTP*](#_apartado9)


<br>
<br>

# <a name="_apartado1"></a>1. Introducción a Dart

## El lenguaje Dart

El lenguaje utilizado para el desarrollo en Flutter es **Dart**, y por eso antes de entrar con la programación de lleno con el framework, nos familiarizaremos un poco con este lenguaje.

Para trabajar con los diferentes ejemplos que veremos en esta unidad, solo tenemos que escribirlos en un fichero de texto con extensión **dart** y luego, en el terminal, llamar a el ejecutable dart con el nombre del fichero.

`dart nombre_de_fichero.dart`

En proyectos más complejos creados con Dart, también es habitual ejecutar aplicaciones mediante:

`dart run nombre_proyecto`

Alternativamente, también podemos trabajar con el [Playground de Dart](https://dartpad.dev/). Éste, además, tiene la ventaja que incluye en la misma ventana el editor de código con resaltado de sintaxis y detección de errores, la salida del programa, documentación y algunos ejemplos, tanto con Dart como con Flutter para explorar las diferentes posibilidades de los mismos.

### **Conceptos básicos.**

Como muchos otros lenguajes, Dart utiliza la función *main* como punto de entrada a un programa. Partiremos de un clásico *Hola Mundo* con parámetros de entrada como ejemplo inicial:

```dart
void main(List<String> args){
  // Ejemplo de Hola Mundo
    if (args.isNotEmpty) {
      print ("Hola ${args[0]}");
    } else  {
      print("Hola mundo!");
    } 
}
```

Vemos algunos detalles de Dart en este código:

- La función `main` no devuelve ningún valor, y aunque el tipo `void` no es obligatorio indicarlo, suele ser una buena práctica hacerlo. 
  
- Esta función principal puede recibir argumentos, en forma de lista de cadena de caracteres (`List<String> args`). En caso de que no necesitemos argumentos, podemos usar directamente `void main()`.
  
- Para comprobar si la lista está vacía, aunque podríamos haber comprobado si su longitud es positiva (`args.length>0`) es más correcto hacer uso de `isNotEmpty`.
  
- Los bloques de código deben incluirse entre llaves `{}`. Cuando el bloque sólo se compone de una línea de código (como es el caso de los dos `print()` al ejemplo), aunque no es obligatorio, también se aconseja hacerlo.
  
- Los comentarios se expresan como en otros lenguajes tipo Java o C, con `//` y `/* ... */`, según sean de una línea o multilínea. 
  
- Para mostrar un mensaje por pantalla empleamos la orden `print()`. Cuando hay variables dentro del texto, aunque podemos usar el operador + para concatenar literales, se recomienda el uso de la interpolación de cadenas (*String interpolation*), haciendo uso del símbolo del $ (`$variable`) o bien de `${}` si tenemos que acotar la interpolación (`${variable.propiedad}`), tal y como hacemos en *Bash*.
  
- Las sentencias en Dart acaban con punto y coma ;
  
- Para acceder a las listas, lo podemos hacer directamente con el operador `[]`, como si se tratara de un vector.

### **Entrada y salida**
Como hemos visto, para mostrar mensajes para la consola podemos hacer uso de la función `print()`, pero esta no es la única forma.

Dart provee a través de la biblioteca `dart:io` mecanismos para gestionar la entrada y la salida a través de consola y teclado, entre otros. 

Concretamente, para la salida por consola nos provee el método `write()` de las clases `stdout` y `stderr`, correspondiente a la salida estándar y de error respectivamente. En cuanto a la entrada por teclado, podemos hacer uso del método `readLineSync()` de la clase `stdin`.

Veamos un pequeño ejemplo:

```dart
import 'dart:io';

void main(){
  stdout.write("Hola! Cómo te llamas? ");
  var name = stdin.readLineSync();
  print("Hola $name!");
}
```

La salida de este programa será la siguiente:

```
$ dart exemple.dart 
Hola! Cómo te llamas? Jose 
Hola Jose!
```

Como podréis apreciar, la principal diferencia entre el método `stdout.write` y `print` es que el primero no arroja un salto de línea al final, mientras `print` sí lo hace.

Hay que decir que, la clase `Stdin` permite al usuario leer datos de la entrada estándar de manera tanto síncrona como asíncrona. Tal y como hemos visto, con el fin de realizar la lectura desde el teclado de forma síncrona, haremos uso del método `readLineSync()`.

<br>
<br>

# <a name="_apartado2"></a>2. Tipos de Datos

Los tipos de datos soportados por Dart son:

- **Numéricos**: enteros (`int`) y decimales (`double`),
- **Cadenas de caracteres**: (`String`)
- **Valores lógicos**: (`bool`)
- **Colecciones de objetos**: Listas (`List`), Conjuntos (`Set`) y diccionarios (`Map`)

Para declarar una variable con Dart podemos utilizar `var`, de manera que el tipo de dato se infiera forma automática a partir del valor dado, o bien indicar directamente el tipo. Una vez inferido o declarado un tipo para una variable, ésta sólo podrá almacenar valores compatibles con dicho tipo. 

Veamos algunos ejemplos:

```dart
var dia='jueves';       // Infiere el tipo a String
String dia='martes';   // Definimos un String
int numero=42;          // Definimos un entero
bool laborable=true;    // Definimos un valor bool

// También podemos realizar conversiones de tipo
String cadena_numero="1";               // Definimos un String que contiene un número
int numero2=int.parse(cadena_numero);   // Convierte la cadena "1" a un tipo numérico
```

Además de los tipos básicos, Dart dispone del tipo `Object`, del que heredan todos los objetos del lenguaje.

### **Constantes y finales**

Para definir **constantes** utilizaremos la palabra reservada `const`, con la que declaramos un valor en tiempo de compilación que será inmutable y no podrá ser reasignado:

```
const curso='Flutter'
```

Además, también podemos declarar datos como `final`, para indicar que no podrán ser reasignados. La diferencia con las constantes es que **un objeto declarado como `final`, aunque no pueda ser reasignado, sí es mutable**, es decir, sí pueden cambiar las propiedades internas. Por ejemplo, si definimos una lista como constante, no podremos añadirle elementos, pero si la declaramos como final, aunque no podamos asignarle otra lista, sí podremos añadir elementos.

### **Null Safety y tratamiento de valores nulos**

Dart es un lenguaje de **tipado seguro**, lo que significa que cuando declaramos una variable de algún tipo, el compilador garantiza que los valores asignados sean de este tipo. Aunque el tipado es obligatorio, indicar el tipo de una variable es opcional. En caso de que no indiquemos el tipo, éste será inferido a partir del valor con que se inicialice.

Desde la versión 2.12 (marzo de 2021), Dart soporta también *Null Safety*, de manera que, por defecto, una variable no podrá contener valores nulos a no ser que se especifique lo contrario, ahorrando así los problemas derivados de valores nulos.

Vemos los diferentes operadores con los que podemos tratar los nulos con Dart:

- **Declaración de valor *nullable* (?)**: Si queremos indicar de manera explícita que una variable puede contener valores nulos, hacemos uso del interrogante en su declaración, tal y como se hace en otros lenguajes como Kotlin:

```dart
  int? variable1; // variable1 podrá tener el valor null
  ```

- **Operador de aserción nula (*null assertion operator*) (!)**: Se utiliza cuando queremos asignar una variable que puede contener nulos a variables que no pueden contenerlas.

`int variable2=variable1!`

Ejemplo:

```dart
int? variable1;
int variable2=variable1!; // TypeError: null has no 
print(variable2);         // propertiesError: TypeError:
                          // null has no properties
```

- El error de arriba detiene la ejecución del programa. Con el fin de gestionar las excepciones que se realizan, podemos hacer uso de bloques *try-catch*, como en otros lenguajes de programación.

```dart
int? variable1;
try{
  int variable2=variable1!; 
  print(variable2);         
} catch (e){
    print(e.runtimeType); // -> NullError
    print(e);             // -> NoSuchMethodError: t1 is null
}
```

- **Operador nulo (`??`)**: Este operador devuelve el valor resultante de la expresión de la parte izquierda del operador, siempre que no sea nulo. En caso contrario nos devolverá la expresión de la derecha. Podemos verlo como una especie de operador condicional a los valores nulos:

```dart
var nom;
// Escribe el nombre si no el nulo, o escriu "Anónimo"
print(nom ?? "Anónimo");
```

- **Asignación consciente de nulos *(null aware assignment)* (`?? =`)**: Asigna un valor a una variable si ésta tiene valor *nulo*. En caso de que la variable tenga un valor previamente diferente a *null*, no se asignará.

```dart
int? variable1;   // Si no indicamos nullable daría error
print(variable1); // Muestra null
variable1 ??= 10; 
print(variable1); // Muestra "10"
variable1 ??= 15; 
print(variable1); // Muestra "10", ya que variable1 ya tenia valor.
```

- **Acceso consciente de nulos *(null-aware access)***(`?.`): Evita que se lance una excepción cuando se accede a una propiedad o método de un objeto que puede ser nulo.

```dart
String? cadena;
print (cadena?.length);
```

### **El tipo *dynamic***

Dart es un lenguaje que soporta tanto tipado estático como dinámico. Cuando hablamos de **tipado estático** hacemos referencia a que los tipos se asignan *en tiempos de compilación*, por lo que se debe indicar el tipo de variable en la propia declaración, tal y como hemos visto hasta ahora. Ahora bien, Dart también soporta tipado de datos **dinámico**, de manera que hace la comprobación de tipos en *tiempo de ejecución*.

Para ello, se hace uso del tipo `dynamic`, un tipo de dato subyacente a todos los objetos Dart, y que nos permite utilizar tipado dinámico de datos, de manera que la comprobación de estos tipos se realiza en tiempo de ejecución en lugar de tiempo de compilación.

```dart
List<dynamic> paises;
```

Encontraremos este tipo con frecuencia cuando trabajemos con datos procedentes de servicios web, ya que inicialmente la información obtenida desde una API suele representarse mediante estructuras dinámicas que posteriormente convertiremos en objetos Dart.

Tenemos más detalles al artículo [Dart es un lenguaje de programación de tipo estático o dinámico](https://medium.com/@farhanaslam910/dart-is-a-static-or-dynamic-typed-programming-language-3d934c95b7b)

### **Tipos enumerados**

Los tipos enumerados en Dart (`enum`), como en otros lenguajes, nos sirven para representar un número fijo de valores constantes.

Por ejemplo, podemos definir un enumerado con los días de la semana:

```dart
enum DiasSemana { lunes, martes, miercoles, jueves, viernes, sabado, domingo }
```

Internamente, cada uno de estos valores se representa por el índice que ocupa, siendo el primero el 0.

Para acceder a estos valores, lo haremos a través de la notación punto. Por ejemplo:

```dart
DiasSemana dia=DiasSemana.lunes;
```

Si queremos obtener una lista con los valores del enumerado, haremos uso de `values`:

```dart
List<DiasSemana> lista = DiasSemana.values;
```

Un tipo enumerado, al igual que las clases, debe definirse fuera de cualquier función o clase.

<br>
<br>


# <a name="_apartado3"></a>3. Programación Estructurada

La programación estructurada con Dart se basa en las estructuras condicionales y de repetición habituales: *`if..else`*, *`switch`*, *`for`*, *`forEach`* y *`while`*. Además, también soporta el operador condicional ternario (`?`).

Vamos a ver algunos ejemplos comentados de estas estructuras:

## Estructuras condicionales

**Ejemplo 1: el operador `if/if-else`**

```dart
// Importamos la librería dart:io, que contiene
// la definición de la función exit
import 'dart:io';

// La función principal comprueba que haya
// recibido un argumento en la llamada
void main(List<String> args) {
  // Ejemplo sencillo de if
  if (args.length != 1) {
    print("Error, hay que introducir un argumento");
    exit(1);
  }

  // Recogemos el valor del primer argumento
  //Utilizamos un bloque try-catch por si
  // hay una excepción de tipo

  var temperatura;
  try {
    temperatura = int.parse(args[0]);
  } catch (e) {
    print("Se ha producido la excepción: ${e.toString()}");
    exit(1);
  }

  // Ejemplo de if-else
  // Aunque no es necesario se recomienda
  // utilizar siempre las llaves {}

  if (temperatura > 21) {
    print("Hace calor");
  } else {
    print("Hace frío");
  }

  // Ejemplo de operador condicional ternario
  temperatura > 21 ? print("Hace calor") : print("Hace frío");

  // Ejemplo de if ternario como expresión para asignar a variable
  var text = temperatura > 21 ? "Hace calor" : "Hace frío";
  print(text);
}
```

Para ejecutar el ejemplo anterior (si lo hemos llamado *ejemplo1.dart*), haremos:

```
dart ejemplo1.dart temp
```

Siendo *temp* un valor numérico que represente una temperatura.

<br>

**Ejemplo 2: El operador switch**

```dart
// Importamos la librería dart:io, que contiene
// la definición de la función exit
import 'dart:io';

// La función principal comprueba que haya
// recibido un argumento en la llamada
void main(List<String> args) {
  // Ejemplo sencillo de if
  if (args.length != 1) {
    print("Error, hay que indicar un argumento");
    exit(1);
  }

  // Ejemplo de switch
  var diaSemana = args[0];

  // Utilizamos el método toLowerCase de los
  // strings para pasarlo todo a minúscula.
  switch (diaSemana.toLowerCase()) {
    case "sábado":
    case "domingo":
      print("No es laborable");
      break;
    default:
      print('Es laborable o no es un dia correcto');
  }
}
```
Observad que la forma de operar es la misma que con otros lenguajes como **C#** o **Java**, de manera que cuando el valor sobre el que estamos haciendo el switch coincide con uno de los `case`, se ejecuta su contenido hasta encontrar un `break`. De esta manera, comprobamos si el día es *sábado* o *domingo*, y ejecutamos el mismo bloque en ambos casos.

<br>

## Estructuras repetitivas

**Ejemplo 1: Uso de for**

```dart
void main(List<String> args) {  
  // Ejemplo for
  for (int i = 0; i <= 10; i++) {
    //Comprobamos si es par
    if (i.isEven){
      print("${i} es par");
    } else{
      print("${i} es impar");
    }
  }
}
```

**Ejemplo2. Bucle while:**

```dart
// Ejemplo de While
void main(List<String> args) {

  // Requiere la inicialización
  // antesdel bucle
  int i = 0;
  while (i <= 10) {
    if (i.isEven)
      print("${i} és par");
    else
      print("${i} és impar");
    i++;
  }
}
```

**Ejemplo 3  Bucle do..while:**

```dart
void main(List<String> args) {
  // Inicialización previa
  int i = 0;

  do {
    // El contenido del bucle se ejecutará 
    // al menos una vez.
    if (i.isEven)
      print("${i} és par");
    else
      print("${i} és impar");
    i++;
  } while (i <= 10);
}
```

**Ejemplo 4. Uso de for..in**
```dart
void main() {
  List<String> continentes = [
    "Europa",
    "Asia",
    "África",
    "América",
    "Oceanía"
  ];

  for (var continente in continentes) {
    print(continente);
  }
}
```

**Ejemplo 5. Uso de forEach**

Es una forma funcional de recorrer colecciones.

```dart
List<String> continentes = [
  "Europa",
  "Asia",
  "África",
  "América",
  "Oceanía"
];

continentes.forEach((continente) {
  print(continente);
});
```

<br>
<br>

# <a name="_apartado4"></a>4. Funciones

## Declaración de funciones

Dart admite funciones de primer orden, es decir, funciones que no estén vinculadas a un objeto como método.

La declaración de funciones se hace de forma muy parecida a otros lenguajes como **C#** o **Kotlin**:

### Función sin argumentos y sin valor de retorno

```dart
void funcion(){
  // Cuerpo de la función
}
```

### Función con argumentos y sin valor de retorno

```dart
void funcion(tipo1 argumento1, ..., tipoN argumentoN){
  // Cuerpo de la función
}
```

```dart
void mostrarPais(String pais) {
  print("País seleccionado: $pais");
}
```

### Función con argumentos y con valor de retorno

```dart
tipoRetorno funcion(tipo1 argument1, ..., tipoN argumentN){
  // Cuerpo de la función
  return ValorDeTipoRetorno;
}
```

<br>

## Funciones anónimas y funciones flecha

Dart admite funciones sin nombre o funciones anónimas, que no pueden ser invocadas directamente, pero que pueden utilizarse como `callbacks`, es decir, como argumentos para otras funciones. 

Por ejemplo, definimos una función `funcion` que recibe tres argumentos: los dos primeros (`arg1` y `arg2`) son valores, y el tercero es una función anónima (`callback`). Esta función `funcion`, lo que hace en su cuerpo es invocar la función que se nos proporciona como argumento, y devuelve el valor que ésta nos proporciona:

```dart
// Función que recibe dos argumentos y una
// función anónima que hace de callback
int funcion(
    int arg1,
    int arg2,
    int Function(int, int) callback) {

  return callback(arg1, arg2);
}
```

En este código, estamos invocando una función que recibimos como parámetro dentro del cuerpo de otra función. Aunque la función que recibimos es una función anónima, como la hemos recibido como argumento, haciendo uso del nombre del argumento (*callback*) para invocarla.

Ahora, podemos utilizar esta función proporcionándole en el momento de la invocación la funcionalidad que queremos que realice, a través de una función anónima:

```dart
void main(){
  int valor=funcion(3, 4, (arg1, arg2){
    // Estamos dentro de la función anónima
    return (arg1+arg2);
  });
  print(valor);
}

```
Como vemos la función anónima recibe dos argumentos y devuelve el valor de su suma.

### **Funciones flecha**

Por su parte, las funciones flecha o **arrow functions** nos permiten abreviar la declaración de una función anónima cuando ésta consta sólo de una línea, de manera que no utilizan ni las llaves ni la palabra reservada `return`. 

El ejemplo anterior, podría haberse expresado con funciones flecha de la siguiente manera:

```dart
int funcion(arg1, arg2, callback) => callback(arg1, arg2);

void main(){
  print (funcion(3, 4, (arg1, arg2) => arg1+arg2));
}
```
<br>

## Argumentos posicionales obligatorios, opcionales y con nombre

Las funciones en Dart admiten tres tipos de argumentos:

- Argumentos ***posicionales obligatorios***,
  
- Argumentos ***posicionales opcionales***, que indicaremos con `[]`, y que pueden tener o no valor predeterminado (si no se especifica será nulo), y 
  
- Argumentos ***opcionales con nombre***, que indicaremos con `{}`, y para los que se requerirá indicar el nombre a la hora de la invocación. Cabe destacar que en este tipo de parámetros, el orden en que se indican en la invocación no importa.

Veamos algunos ejemplos:

```dart
void f1(int obligatorio, [int opcional = 0]) {
  print("${obligatorio}, ${opcional}");
}

void f2(int obligatorio, {int opcionalConNombre = 0}) {
  print("${obligatorio}, ${opcionalConNombre}");
}

void main() {
  f1(1);    // Muestra: 1, 0
  //f1();   // Si llamamos f1() sin argumentos, obtendremos
            // el error: Context: Found this candidate,
            // but the arguments don't match.

  f1(1, 2); // Muestra:  1, 2

  f2(1);    // Muestra: 1, 0

  // f2(1, 2); // Si proporcionamos dos argumentos a f2, pero
              // sin indicar el nombre, tendremos un error.

  f2(1, opcionalConNombre: 3); // Muestra 1, 3
}
```

Cuando una llamada a función, a un método de un objeto o a un constructor hace uso de varios argumentos con nombre, es habitual separar los diferentes parámetros por líneas. Por ejemplo:

```dart
funcionX(
    paremetro1: valor1,
    parametro2: valor2
    ...
)
```

Como veremos posteriormente, esta será una construcción muy común cuando generemos componentes visuales con Flutter.

También es muy habitual cuando utilizamos constructores con argumentos con nombre para crear objetos.

<br>
<br>

# <a name="_apartado5"></a>5. Colecciones

Las colecciones son objetos que representan un grupo de elementos, y pueden tener diferentes estructuras y comportamientos. Las colecciones más habituales son las listas, los conjuntos y los mapas.

<br>

## Listas

Dart utiliza el principio del *mismo nivel de abstracción*, según el cual, un código neto no debe mezclar instrucciones de alto nivel con instrucciones de bajo nivel en la implementación de su lógica, de manera que se facilite su lectura.

Dart puede definirse como un lenguaje de alto nivel, y que no recurre a estructuras de bajo nivel como puedan ser los vectores, sino que directamente hace uso de listas (clase `List`) para representar colecciones ordenadas de elementos.

No obstante, Dart facilita el acceso a listas como si trabajáramos con vectores, al tiempo que nos ofrece funciones de más alto nivel que nos permiten trabajar de manera más cómoda.

### Creación de listas
Vemos algunas formas de definir listas:

```dart
// Lista nula
List? lista_nula;

// Lista Vacía
List listaVacia=[];

// Lista vacía especificando el tipo
List<String> listaVaciaTipo=[];   // Forma 1
List<String> _lista=<String>[];   // Forma 2

// Lista con valores
List<String> laborables=['lunes' , 'martes', 'miércoles', 'jueves', 'viernes'];

// Lista con valores especificando el tipo
List<String> festivos=['sábado', 'domingo'];

List<String> continentes = [
  "Europa",
  "Asia",
  "África",
  "América",
  "Oceanía"
];
```

### Manipulación de listas

Y ahora vemos algunas formas de acceder y manipularlas:

```dart
// Acceso a una posición
print(laborables[3]);

// Añadiendo elementos a la lista
listaVacia.add("Elemento");

// Modificando un elemento existente en la lista
// Ha de existir!!
listaVacia[0]="Elemento 2";

// Eliminar el último elemento de la lista
laborables.removeLast();

// Eliminando un elemento en una posición de la lista
laborables.removeAt(posicion);

// Añadiendo un lista completa al final de otra
List<String> diasSemana=[];
diasSemana.addAll(laborables);
diasSemana.addAll(festivos);
print (diasSemana);
```
En este último punto, para poder utilizar `addAll`, necesitamos que la lista haya sido inicializada (no sea null).

### Operador Spread (...)

Dart proporciona el operador spread (...), que permite insertar todos los elementos de una colección dentro de otra de forma más compacta y legible.
Por ejemplo, el código anterior puede escribirse también como:

```dart
List<String> diasSemana = [
  ...laborables,
  ...festivos
];

print(diasSemana);
```

<br>

## Sets (Conjuntos)

Otra colección de elementos interesante en Dart son los `Sets` o conjuntos, que, a diferencia de las listas, no mantienen los elementos indexados y evitan así elementos duplicados.

Vemos algunos ejemplos sobre cómo definir y trabajar con conjuntos:

```dart
// Declaramos un conjunto a partir de una lista
var modulos = Set.from(["PMDM", "AD", "PSP", "DI", "SGI"]);

// Para añadir elementos utilizamos add:
modulos.add("EIE");

// Los eliminamos con remove:
modulos.remove("EIE");

// contains nos permite ver si existe un elemento en el conjunto
print (modulos.contains("EIE"));
```

<br>

## Maps (Diccionarios)

Un diccionario es una estructura de datos que almacena pares clave-valor, de manera parecida a un `JSON`.

Vemos algunos ejemplos sobre cómo definir y trabajar con estas estructuras:

```dart
// Definición de mapa y asignación de valores
Map notas;
notas={ "PMDM": 8, "AD": 9, "PSP":9, "DI":7};

// Acceso
print(notas["PMDM"]);
notas["DI"]=9;

// Definición del mapa especificando los tipos:
Map<String, int> mapa2;

// Definición del mapa especificando un tipo dinámico para el valor
Map<String, dynamic> mapa3;

// Añadiendo nuevos elementos al mapa
// Si ya existe la clave se modifica el valor
notas["EIE"]=10;

// Eliminando elementos
notas.remove("PMDM");

// Para saber si un elemento existe
print (notas.containsKey("PMDM"));

Map<String, dynamic> pais = {
  "nombre": "España",
  "capital": "Madrid",
  "poblacion": "48500000"
};
```

Más adelante utilizaremos este mecanismo para transformar listas de objetos JSON obtenidas desde una API en listas de objetos Dart.

<br>

## Recorrido de estructuras

Con el fin de recorrer los diferentes tipos estructurados podemos hacer uso de bucles for con el operador in, o bien haciendo uso del método forEach. 

### Recorrido de listas

Si definimos, por ejemplo, la lista:

```dart
List laborables=['lunes', 'martes', 'miércoles', 'jueves', 'viernes'];
```


Podemos recorrerla con un bucle `for...in` de la siguiente manera:

```dart
for (String dia in laborables) {
  print(dia);
}
```

Y con un bucle forEach de la siguiente:

```dart
laborables.forEach((dia) {
  print(dia);
});
```

El método `forEach` recibe como argumento una **función anónima**, que se invoca para cada uno de los elementos de la lista. Esta función anónima recibe como argumento el elemento en cuestión, y lo procesa dentro del cuerpo de la función. En este caso, este procesamiento consiste en imprimir el valor.

Por otra parte, esta función anónima que proporcionamos al método forEach podría expresarse también como función flecha de la siguiente forma:

```dart
laborables.forEach((dia) => print(dia));
```

```dart
List<String> continentes = [
  "Europa",
  "Asia",
  "África",
  "América",
  "Oceanía"
];

for (String continente in continentes) {
  print(continente);
}
```

### Recorrido de conjuntos

El recorrido de conjuntos se realiza de la misma manera que las listas. Si definimos el siguiente conjunto a partir de una lista:

```dart
Set laborables =
      Set.from(['lunes', 'martes', 'miércoles', 'jueves', 'viernes']);
```

Su recorrido con un bucle `for.... in` será:

```dart
for (String dia in laborables) {
  print(dia);
}
```

Y con `forEach`, haciendo uso de una función flecha, sería:

```dart
laborables.forEach((dia) => print(dia));
```

### Recorrido de Maps

Definimos ahora un diccionario con módulos y sus calificaciones:

```dart
Map<String, int> notas = {"PMDM": 8, "AD": 9, "PSP": 9, "DI": 7};
```

Para recorrer este diccionario con un bucle `for.... in`, haremos uso de la propiedad `keys` del mapa, que nos proporciona una lista con las claves del mismo. Para mostrar las calificaciones para cada módulo, accederemos al valor de la clave en el diccionario:

```dart
for (String modulo in notas.keys) {
  print("Módulo: $modulo, nota: ${notas[modulo]}");
}
```

En cuanto al método `forEach` de los diccionarios, éste recibe dos argumentos en lugar de uno: la clave y el valor de cada uno de los elementos, de manera que para mostrar su contenido haríamos:

```dart
notas.forEach((key, value) => print("Módulo: $key, nota: $value"));
```

### Mapeado de estructuras

Las colecciones en *Dart* poseen un método `map` para transformar unas estructuras en otras. Para ello, habrá que proporcionarle una función anónima que se aplicará a cada uno de los elementos para obtener el nuevo elemento correspondiente.

Vemos con un ejemplo, cómo convertir un conjunto de `Strings` expresados en mayúscula, en una colección donde se expresan en minúscula.

```dart
void main(){

  // Definimos un conjunto de elementos
  var modulos = Set.from(["PMDM", "AD", "PSP", "DI", "SGI"]);
  print(modulos);

  // Utilizamos el método map para procesar
  // cada uno de los elementos del conjunto
  // (En este caso los convertimos a minúscula)
  var modulos2=modulos.map((item) {
    return item.toString().toLowerCase();
    });

    print (modulos2);
}
```

Disponemos de más documentación sobre colecciones e iterables en:

El artículo [*Top 10 métodos para manipular colecciones en Dart*](https://www.tecnoblog.org/desarrollo/dart-manipular-colecciones-top-10-metodos/), en Tecnoblog.org.

El codelab de Dart sobre iterables: <https://dart.dev/codelabs/iterables>


<br>
<br>

# <a name="_apartado6"></a>6. Programación Orientada a Objetos

La orientación a objetos es de gran importancia en Dart, y sobre todo en Flutter, ya que en estos conceptos se basará todo el diseño de interfaces mediante *widgets*.

## Clases y constructores

La sintaxis básica para crear una clase en Dart es bastante parecida a otros lenguajes, como Java:

```dart
class NombreClase {
    Tipo1? propiedad1;
    Tipo2? propiedad2; 
    ...

    // Constructor (opcional)
    NombreClase(Tipo1 arg1, Tipo2 arg2,...){
        propiedad1=arg1; 
        propiedad2=arg2; 
        ...
    }
}

```

Veamos algunos detalles. Por un lado, el **constructor** de la clase es opcional. En caso de que éste no se declare, Dart utiliza un constructor predeterminado sin argumentos. 

Si incorporamos un constructor a la clase, este se trata de un método con el mismo nombre que la clase y sin tipos, tal y como se hace en Java. 

Fijémonos que en el ejemplo hemos definido las propiedades como *nullables*. En caso de no hacerlo así, el compilador nos daría el error *`Non-nullable instance field 'nombre_propiedad' must be initialized`* indicando que es necesario inicializar esta propiedad. Estos valores iniciales los podemos dar en la misma definición de las propiedades.

```dart
class NombreClase {
    Tipo1? propiedad1 = valor_inicial_1;
    Tipo2? propiedad2 = valor_inicial_2; 
    ...
}
```


### **Instanciación de objetos**
Con el fin de crear un objeto de la clase anterior, podríamos hacerlo con:

```dart
NombreClase object = NombreClase(param1, param2);
```

Aunque podemos usar la palabra clave `new` (`new NombreClase(param1, param2)`), esta es opcional, y cuando trabajamos con Flutter, se recomienda no utilizarla.

Por otra parte, si intentamos imprimir el objeto (`print(objeto);`) nos dirá que es una instancia de `NombreClase`. Si lo que queremos es que nos muestre el contenido, deberíamos sobreescribir el método `toString` de la siguiente manera:

```dart
    @override 
    String toString() {
      return 'Propiedad1: $propiedad1, Propiedad2: $propiedad2';
    }
```


Hay que decir que, en Dart, la anotación `@override` también es opcional, y podríamos omitirla.

Por otro lado, en expresiones como la anterior debemos tener especial cuidado si optamos por utilizar el `this`. Aunque no es recomendable, si utilizamos este habría que hacer uso de las claves para delimitar el alcance del $, de la siguiente manera:

```dart
return 'Propiedad1: ${this.propiedad1}, Propiedad2: ${this.propiedad2}';
```

Si sólo empleáramos `$this.propiedad1` o `$this.propedad2` estaríamos intentando imprimir la misma clase (`$this`), por lo que se invocaría a este método de forma recursiva, entrando pues en un bucle infinito.

Un ejemplo más completo de lo que hemos explicado podría ser el siguiente:

```dart
class Persona {
    String? nombre;
    String? apellidos; 

    Persona(String arg1, String arg2){
        nombre=arg1;
        apellidos=arg2;
    }

  @override 
  String toString() {
    return 'Nombre: $nombre, Apellidos: $apellidos';
  }   
}

void main (){
  Persona objeto=Persona("Luke", "Skywalker");
  print(objeto.toString()); 
  // print(objeto);
}
```

Puede comprobar su funcionamiento en el siguiente Gist: <https://dartpad.dev/?id=89e4c3eb89cf029ee444d8e4f5a5b841>.

<iframe
  src="https://dartpad.dev/embed-inline.html?id=89e4c3eb89cf029ee444d8e4f5a5b841"
  width="100%"
  height="500px"
  frameborder="0">
</iframe>

### **Simplificación del constructor**
El constructor se puede simplificar de la siguiente manera:

```dart
NombreClase(this.propiedad1, this.propiedad2);
```

Con lo cual, además, conseguimos que las propiedades se inicialicen en la misma definición, de manera que no sea necesario declarar éstas como *nullables*.

Para el ejemplo de la clase *Persona* tendríamos:

```dart
Persona(this.nombre, this.apellidos);
```

Actualmente, ésta es la forma más habitual de implementar constructores sencillos en Dart, ya que reduce considerablemente la cantidad de código necesario.


### **Constructores con paso de argumento por nombre**
También es bastante habitual pasar los parámetros de inicialización del constructor por nombre, en lugar de hacerlo de forma posicional. Esto lo conseguimos con las llaves `{}`:

```dart
NombreClase({
    required this.propiedad1,
    required this.propiedad2
    });
```

El uso de la palabra reservada `required` indica la obligatoriedad de incluir el argumento, de manera que evitemos valores nulos. Si no utilizáramos el `required`, sería necesario bien indicar que es una propiedad *nullable* o indicarle un valor predeterminado, bien sea en su definición o bien en los parámetros del constructor:

```dart
class NombreClase{
    ...
    Tipo? propiedad1; // Propiedad Nullable
    Tipo propiedad2=valor; // Con valor predeterminado
    Tipo propiedad3;
    ...
    NombreClase({
        this.propiedad1, 
        this.propiedad2,
        this.propiedad3=valor // Valor predeterminado al constructor
    });
}
```

Cuando definimos una propiedad como no nulable y no vamos a inicializarla en la misma declaración, podemos hacer uso de la palabra reservada late:

```dart
late Tipo propiedad;
```

para indicar que esta propiedad se inicializará más adelante. Si el compilador detecta su uso antes de la inicialización nos dará un error. Esto nos permite declarar variables, pero inicializarlas más tarde (por ejemplo, en el constructor)

Sea como sea, de esta manera, cuando creamos un objeto lo haremos con:

```dart
NombreClase objecto=NombreClase(
    propiedad1: valor1,
    propiedad2: valor2,
    ...
)
```

Y no importa el orden en que ponemos los argumentos, ya que lo que cuenta ahora es el nombre.

```dart
Pais({
  required this.nombre,
  this.capital,
  this.poblacion,
  this.imagen,
});
```

Este tipo de constructores es muy frecuente en Flutter.

### **Múltiples constructores con nombre (named constructor)**

Dart no soporta sobrecarga de constructores. Para posibilitar la construcción de objetos mediante diferentes métodos se utilizan los constructores con nombre, que también aportan mayor claridad a las declaraciones. Para definir un constructor con nombre hacemos uso del punto para separar al constructor del nombre:

```dart
NombreClase.constructor_con_nombre1(lista_argumentos_1){...}

NomClase.constructor_con_nombre2(lista_argumentos_2){...}
```

Veremos un ejemplo de uso concreto de estos constructores en el siguiente apartado.

### **Inicialización con diccionario**
Uno de los aspectos más interesantes y comunes en Dart es la creación de objetos a partir de un diccionario o JSON. Por ejemplo:

```dart
final objetoJSON={
    propiedad1: valor1,
    propiedad2: valor2
}
```


Para crear el objeto, podemos crear un constructor con nombre que se inicialice a partir de un JSON, de la siguiente manera:

```dart
class NombreClase{
    ...
    NombreClase.fromJSON( Map <Tipo1, Tipo2> objetoJSON){
        propiedad1=objetoJSON['propiedad1'] ?? "valor_por_defecto1",
        propiedad2=objetoJSON['propiedad2'] ?? "valor_por_defecto2";
        ...
        }
    ...
}
```

Veamos los detalles:

- El constructor `NombreClase.fromJSON` recibe un diccionario (`Map`) como argumento, que se utilizará para inicializar las propiedades de la instancia.
  
- En la declaración del mapa como argumento, definimos los tipos de la clave y el valor (`<Tipo1, Tipo2>`). Si no se indica, Dart infiere los tipos directamente.
  
- Dentro del constructor, asignamos valores a las propiedades obteniéndolas del JSON. En caso de que no se encuentre la propiedad en el JSON, con el operador ?? podemos asignar valores por defecto.

También hemos comentado que un constructor con nombre aporta claridad a las definiciones. En este caso, hemos hecho uso de un nombre que indica explícitamente que se utiliza un JSON para crear el objetivo (`.fromJSON`), pero este nombre podría ser cualquiera.

Para crear un objeto de esta manera, ya podemos hacerlo con:

```dart
NombreClase miObjeto = NombreClase.fromJSON(objetoJSON)
```

### Ejemplo

Siguiendo el ejemplo de la definición de personas, podríamos hacer uso de un constructor con nombre de la siguiente forma:

```dart
class Persona {
  ...

  Persona.fromJSON(Map<String, dynamic> objetoJSON) {
    nombre = objetoJSON['nombre'];
    apellidos = objetoJSON['apellidos'];
    anyoNacimiento = objetoJSON['anyoNacimiento'];
    especie = objetoJSON['especie'] ?? "Humana";
  }

  ...

}

void main() {
  ...

   Map <String, dynamic>  myJSON={
    "nombre": "Han", 
    "apellidos":"Solo"
    };

  Persona p3=Persona.fromJSON(myJSON);
  print (p3.toString());
}

```

Disponemos del ejemplo completo al siguiente Gist: <https://dartpad.dev/?id=f7ed2afe29db34a283a786dc6eac2898>.

<iframe
  src="https://dartpad.dev/embed-inline.html?id=f7ed2afe29db34a283a786dc6eac2898"
  width="100%"
  height="500px"
  frameborder="0">
</iframe>


### **Listas de inicializadores o de inicialización**

Otra forma en que nos podemos encontrar los constructores en Dart es haciendo uso de listas de inicializadores, consistente en una lista de inicializaciones, separadas por comas que se ejecutan antes del código del constructor. Por ejemplo, el constructor Persona.fromJSON del apartado anterior, podrían haberse expresado con listas de inicialización de la siguiente forma:

```dart
Persona.fromJSON(Map <String, dynamic> objecteJSON):
    nombre = objetoJSON['nombre'],
    apellidos = objetoJSON['apellidos'],
    anyoNacimiento = objetoJSON['anyoNacimiento'],
    especie = objetoJSON['especie'] ?? "Humana",

```

Como vemos, la única cosa que hemos hecho es eliminar las llaves que definían el bloque, y hacer uso de los dos puntos para indicar la lista separada por comas de inicializadores.

### **Métodos de acceso**

Dart no contempla palabras reservadas como `public` o `private`. De manera predeterminada, toda propiedad que declaramos será pública. Si lo que queremos es que ésta sea privada, lo indicaremos a su nombre, haciendo que éste comience por el guión bajo `_`.

```dart
class NombreClase{
  Tipo _propietatPrivada;
}
```

Ahora bien, hay que tener en cuenta que este nivel de privacidad es en el ámbito de la librería, o lo que en Kotlin o Java sería un paquete, y representaría la aplicación.

Así pues, desde cualquier clase de nuestra aplicación tendremos acceso a las propiedades del resto de clases de la misma, bien sean públicas o privadas.

Entonces, ¿tiene sentido utilizar modificadores de aceso? Aunque son menos frecuentes, los métodos de acceso pueden emplearse con el fin de obtener propiedades derivadas, o para establecer valores a partir de estas propiedades derivadas.

Para crear *getters* y *setters*, lo haremos de la siguiente forma:

```dart
tipoRetorno get nombrePropiedadDerivada {
    return calculo_de_la_propiedad;
}

set nombrePropiedadDerivada (Tipo parametro){
    // Actualitzación de las propiedades internas
}
```

Por ejemplo, si en la clase Persona queremos añadir un campo derivado que sea la edad, podríamos definir los métodos `get` y `set` de la siguiente forma:

```dart
class Persona {
  // Declaración de propiedades
  String? nombre;
  int? anyoNacimiento;
  ...

   int get edad{
    // Obtenemos la fecha actual, instanciamos un objecto DateTime
    DateTime currentTime = DateTime.now();  

    // El año se encuentra en la propiedad year del objeto currentTime
    return currentTime.year-(anyoNacimiento ?? 0);
  }

  set edad (int edad){
    // Establecemos el año de nacimiento a partir de la edad
    this.anyoNacimiento=DateTime.now().year-edat;
  }
  ...
}
```

En estos métodos hemos hecho uso de la clase [*DateTime*](https://api.dart.dev/stable/2.18.5/dart-core/DateTime-class.html) que representa datos referentes al tiempo. Con `DateTime.now()` obtenemos el instante actual, a partir del cual podemos obtener el año con la propiedad `year`.

En este caso, lo que hacemos es *definir* un método `set` y otro `get` que, haciendo uso del año actual y el año de nacimiento, gestionan una *propiedad derivada* que es la edad, de manera que con un objeto de tipo `Persona` podríamos hacer uso de edad como si se tratara de una propiedad de la misma clase:

```dart
p.edat=40;

print(p.edat);
```

<br>

## Herencia
Para que una clase pueda heredarse, necesita tener un constructor vacío, sin argumentos, que será el constructor predeterminado que usarán las subclases. **El resto de constructores, no se heredarán.**

Cuando una superclase no dispone de un constructor sin argumentos, las subclases deberán invocar explícitamente alguno de los constructores disponibles mediante la palabra reservada `super`.

```dart
class SuperClase{
  String propiedad1;

  // Constructor por defecto con lista de inicialización.
  SuperClase():propiedad1="Valor per defecto en la superclase";

  // Constructor con nombre (no se hereda)
  SuperClase.fromString(String s): this.propiedad1=s;
}
```

Para definir una subclase, haremos uso de la palabra `extends`:

```dart
class SubClase extends SuperClase {
  // Los constructores no se heredan
}
```

Con ello podemos crear instancias de la subclase con:

```dart
// Instancia de la subclase
SubClase sc1=SubClase();
print("Propiedad 1 de la subclase: ${sc1.propietat1}");
```

Lo que no podemos hacer, por ejemplo, es utilizar el constructor con nombre fromString en la subclase:

```dart
// Error, el constructor fromString no se hereda!
SubClase sc2=SubClase.fromString("Prueba"); 
```

Pero lo que sí podemos hacer, es definir al constructor en la subclase e invocar al constructor de la superclase:

```dart
class SubClass2 extends SuperClase {
  // Constructor con nombre que llama al constructor
  // con nombre de la clase padre.
  SubClase2.fromString(String s): super.fromString(s);
}
```

Ahora sí podemos invocar:
```dart
SubClase sc2=SubClase.fromString("Prueba");
```
<br>

## Clases abstractas
Como sabemos, las clases abstractas no pueden ser instanciadas, y sirven para definir subclases, que deben implementar necesariamente los métodos indicados en la clase abstracta. Para indicar una clase abstracta, utilizamos la palabra clave `abstract`. Por ejemplo:

```dart
abstract class Figura{
  int posx;
  int posy;

  void calculaArea(){
    print('Cálculo por defecto');
  }
}

class Rectangulo extends Figura {
  int base;
  int altura;

  @override // Opcional
  void calculaArea() {
    print (this.base*this.altura);
  }
}
```

<br>

## Interfaces y Mixins

Dart introduce el concepto de *interfaz implícita*, consistente en que cualquier clase puede usarse de interfaz. Para declarar que una clase implementa los métodos de otra clase, se utiliza la palabra reservada `implements`.

```dart
class ClaseQueImplementaInterface implements ClaseQueHaceDeInterface{
  // Implementación de los métodos de la clase que hace de interfaz
}
```

Dart, como la mayoría de lenguajes, tampoco soporta la herencia múltiple. Además, y a diferencia de la mayoría de ellos, tampoco suelen usarse las interfaces como aproximación a este tipo de herencia.

El mecanismo que introduce Dart para crear clases que serían una combinación de otros son los ***mixins***, un concepto más cercano al de heréncia múltiple que el de las interfaces.

Un *`mixin`* podría definirse como una clase que deriva de otra, pero combinada con otras clases. Para definir un *mixin* hacemos uso de la palabra reservada `with`.

Por ejemplo, si tenemos definidas las claseS A, B y C, con los métodos fA(), fB() y fC() respectivamente:

```dart
class A{
  void fA(){
    print ("En A");
  }
}

class B{
  void fB(){
    print ("En B");
  }
}

class C{
  void fC(){
    print ("En C");
  }
}
```

Podemos definir el *mixin* claseMixta como una clase derivada de la clase A, pero *mezclada con* las clases B y C:

```dart
mixin ClaseMixta implements A, B, C {}
```

Lo que indica que *ClaseMixta* deriva de la clase A, pero donde tendremos accesibles también las propiedades y métodos de las clases B y C, de manera que podemos hacer lo siguiente:

```dart
ClaseMixta m=ClaseMixta();

m.fA();
m.fB();
m.fC();
```
<br>

Importante

Flutter está basado completamente en clases y objetos. Los widgets, las pantallas, los temas visuales y gran parte de las estructuras del framework se representan mediante clases Dart. Por este motivo, comprender correctamente conceptos como constructores, herencia, composición y objetos es fundamental para trabajar con Flutter.

<br>
<br>

# <a name="_apartado7"></a> 7. Programación Asíncrona

En este apartado vamos a abordar uno de los aspectos más complejos y a la vez interesantes del lenguaje Dart: **la programación asíncrona**. 

Complejo porque supone un cambio en la concepción tradicional de la programación concurrente, basada en hilos, e interesante porque juega un papel fundamental en la programación reactiva de Flutter.

## Programación Asíncrona en Dart

El asincronismo hace referencia a un modelo de programación donde es posible que determinadas operaciones devuelvan el control de la ejecución al programa que las ha invocado antes de haber terminado. 

Los lenguajes de programación ofrecen diferentes tipos de mecanismos para tratar esta programación, como puedan ser los threads en Java o las corrutinas en Kotlin, entre muchos otros.

### **Future**
Dart y Flutter hacen uso de la clase *`Future`* y *`async/await`* para trabajar funciones de forma asíncrona.

Los *Futures* definen tipos de datos asociados a tareas asíncronas, que no se resuelven de forma inmediata. Un ejemplo bastante habitual de este tipo de tareas consiste en las peticiones que realizamos a un servidor, que sabemos que obtendrán respuesta en algún momento, pero no sabemos cuándo.

Para ver un ejemplo que simule una función asíncrona, definiremos la siguiente:

```dart
Future<String> funcionAsincrona(){
 return Future.delayed(Duration(seconds: 1), (){
   print("Estamos en función asíncrona");
   return 'Valor de retorno';
 });
}
```

Esta función devuelve un objeto de tipo `Future` al cabo de un segundo, que contendrá un `String`. O siendo más precisos, nos devuelve un objeto de tipo *Future*, que al cabo de un segundo lanzará una función que nos devuelve un *String*.

Para simular la pausa, hemos utilizado el método **`delayed`** de la clase **`Future`**. Este método recibe un objeto de tipo `Duration` como primer argumento, y una función de *callback sin argumentos* como segundo. Observe que dentro de esta función de callback se realiza también un return.

La clase [Duration](https://api.dart.dev/stable/2.18.5/dart-core/Duration-class.html) representa una duración, o lo que es lo mismo, la diferencia entre dos instantes de tiempo. Con el fin de crear un objeto de tipo `Duration`, hacemos uso de su constructor, al que le podemos proporcionar diferentes argumentos por nombre (hours, minutes, seconds..). En el ejemplo, se ha puesto una duración de un segundo, haciendo uso del argumento `seconds`.

Vamos a ver el funcionamiento mediante el siguiente programa:

```dart
void main(){
  print("Inicio");
  var a=funcionAsincrona(); 
  print(a);
  print("Final");
}
```

El resultado que se nos mostrará por pantalla será:

```
Inicio
Instance of 'Future<String>'
Final
Estamos en funcioAsincrona
```

Como era de esperar, lo primero que muestra es el texto *Inicio*, correspondiente al primer `print` del programa. Después, se invoca a la función asíncrona y se muestra el resultado que ésta devuelve: `Instance of Future<String>`. Es decir, un objeto de tipo Future, que contendrá *en un futuro* un `String`.

Para obtener realmente el valor, debemos esperar a que éste se *resuelva*, haciendo uso del método **then** de la clase Future:

```dart
  Future<String> a = funcionAsincrona();

  a.then((String data) {
    print(data);
  });
```

Este método `then` se invocará cuando la función asíncrona devuelva el valor, y recibirá, ahora sí, un dato de tipo `String` con el resultado de función. Se suele decir que la variable a se *resuelve* en este momento.

Si lo añadimos al ejemplo: 

```dart
void main(){
  print("Inicio");

  Future<String> a=funcionAsincrona(); 

  print(a);

  a.then( ( String data ) {
    print(data);
  } );

  print("Final");
}
```

Veremos que la salida es:

```
Inicio
Instance of '_Future<String>'
Final
Estamos en funcioAsincrona
Valor de retorno
```

Como vemos, la ejecución del programa ha seguido su camino, y la función se ha ejecutado y resuelto de forma asíncrona, pero ahora ya tenemos acceso al resultado.

### **Async/Await**

Cuando se desea que una función asíncrona tenga un comportamiento síncrono, podemos hacer uso de la palabra clave `await`. De esta manera, cuando se invoca una función asíncrona, le estamos indicando a Dart que se espere a la finalización de la misma, en lugar de seguir su ejecución.

Esto se indicaría de la siguiente forma:

```dart
String a = await funcionAsincrona();
print(a);
```

De esta manera, en la misma llamada, esperaríamos la finalización de la función asíncrona (la haríamos síncrona), y el cambio más importante, **ya recibiríamos directamente el String que devuelve la función, en lugar del Future que recibimos antes**.

Además, cuando utilizamos un `await` dentro de una función (incluso la función `main`), ésta debe declararse como `async`, de la siguiente manera:

```dart
void main() async {
  print("Inicio");

  String a=await funcionAsincrona(); 
  print(a);

  print("Final");
}
```

Con esto el resultado ya será el esperado en un comportamiento síncrono:

```
Inicio
Estamos en funcioAsincrona
Valor de retorno
Final
```

```
Sin await:

Future<String> f = funcion();

Con await:

String valor = await funcion();
```

`await` no elimina el asincronismo. La operación sigue siendo asíncrona, pero permite escribir el código de forma más parecida a una secuencia síncrona.

Las peticiones HTTP son uno de los ejemplos más habituales de operaciones asíncronas, ya que la aplicación debe esperar a que el servidor responda. Por este motivo, en la siguiente unidad utilizaremos `Future` y `async/await` para acceder a APIs REST.


### **Tras el asincronismo en Dart: El evento Loop o Bucle de eventos**

Cuando iniciamos una aplicación en Dart (y por extensión en Flutter), se crea un proceso nuevo, o un *Isolate* en terminología más propia de Dart. Este hilo será único, de manera que las operaciones se realizan una tras otra. Además, mientras se está efectuando una operación, ésta no será interrumpida por ningún otro proceso.

En este contexto, cabe preguntarnos cómo gestiona Dart la concurrencia, teniendo en cuenta, además, que cuando trabajamos con Flutter nos encontraremos en un entorno completamente dirigido por eventos.

La respuesta se encuentra en el bucle de eventos o *Event Loop*, el secuenciador de código de Dart.

Cuando creamos un proceso o *Isolate* de Dart se realizan las siguientes operaciones:

1. Se inicializan dos colas FIFO: *MicroTask* y *Event*, que almacenarán tareas a llevar a cabo con diferentes prioridades.
1. Se ejecuta el método main()
1. Una vez finalizado el main, se lanza el Event Loop, que irá ejecutando de forma ordenada las tareas de las colas.

El funcionamiento de este Event Loop es el que podemos ver en el siguiente diagrama de flujo:

![Flujo](./images/imagen2.png)

Básicamente, el proceso de Dart no finaliza mientras quedan tareas pendientes en alguna de las colas.

La principal diferencia entre ambas colas es la prioridad, ya que la cola de microtareas tiene preferencia respecto a la de eventos. Esta cola de microtareas suele utilizarse para acciones internas muy cortas que deben ejecutarse de forma asíncrona después de finalizar cierta operación, y antes de devolver el control al bucle de eventos. Por otro lado, los eventos se lanzan cuando la cola de microtareas está vacía, y quedan eventos pendientes.

Generalmente, trabajaremos con eventos, como pueda ser la lectura de un fichero, la recepción de la respuesta a una petición de red, o la lectura de la base de datos.

Veamos el siguiente ejemplo, donde, se generarán dos tareas, una que será un evento de temporizador (`Future.delayed`), que se dispara a los 0 ms, y la otra una microtarea programada mediante la función `scheduleMicrotask` de la librería `async`:

```dart
import 'dart:async';

void main() {
  print("Inicio");
  Future.delayed(
      Duration(milliseconds: 0), 
      () => print("Hola desde la cola de eventos")
  );

  scheduleMicrotask(
      () => print("Hola desde la cola de microtareas")
  );

  print("Final");

}
```

El resultado de la ejecución de este programa es:

```
Inicio
Final
Hola desde la cola de microtareas
Hola desde la cola de eventos
```

Disponemos de información adicional sobre el Evento Loop en los siguientes artículos:

- [Modos de ejecución de código en Flutter](https://medium.com/comunidad-flutter/modos-de-ejecuci%C3%B3n-de-c%C3%B3digo-en-flutter-f7941030e3a1)
- [El bucle de eventos y el dardo](https://dart.cn/articles/archive/event-loop)

Además, también tenéis a vuestra disposición el siguiente *codelab* sobre *Futures* y *Async/Await* de la documentación oficial de Dart: <https://dart.dev/codelabs/async-await>

### Nota

Aunque el funcionamiento interno del Event Loop resulta interesante para comprender el comportamiento de Dart, en la mayoría de aplicaciones trabajaremos únicamente con `Future`, `then` y `async/await`, **sin necesidad de interactuar directamente con las colas de eventos y microtareas**.

<br>

## Streams
Los *Streams* fueron introducidos por el equipo de Flutter en la Google I/O de 2018, y constituyen el principal componente de la programación reactiva en Flutter.

Cuando hablamos de programación reactiva nos referimos a la propagación de los cambios en el estado de la aplicación con el fin de mantener la coherencia de la misma. Así, la aplicación *reacciona* a los cambios a medida que ocurren, y evita tener que realitar las actualizaciones de estado de forma manual.

### Atención

De momento vamos a dejar apartados los Streams, para no cargar un tema que ya es potente con lo visto hasta aquí.

Los retomaremos en el futuro.

<br>
<br>

# <a name="_apartado8"></a>8. Proyectos en Dart 

## Proyectos con Dart
Hasta ahora hemos desarrollado programas con Dart que consistían con un único fichero, y que ejecutábamos con el orden la herramienta de la línea de órdenes dart.

Cuando nuestro programa crece y debemos dividir su funcionalidad en diversos ficheros, nos surge la necesidad de generar un proyecto *Dart* completo, de manera que nos permita también indicar dependencias de terceros y más opciones de configuración. Para ello, utilizaremos la suborden `create` del orden `dart`.

Si ejecutamos directamente `dart create` podremos ver las diferentes opciones que nos ofrece. En nuestro caso, y a modo de ejemplo que continuaremos en el siguiente apartado, crearemos un proyecto sencillo de consola que llamaremos `info_provincies` (recuerde que, en Dart, los proyectos no pueden tener mayúsculas). Para ello, dentro de la carpeta donde queramos almacenar nuestros proyectos, escribiremos la orden:

```
dart create -t console-simple proyecto_ejemplo
```

Esto nos generará una estructura de proyecto Dart habitual en la carpeta `proyecto_ejemplo`, donde lo que más nos interesa es el fichero con las propiedades del proyecto (*pubspec.yaml*) y el directorio con el código fuente (*bin* en el caso de Dart).

Si consultamos la carpeta generada veremos que contiene el siguiente contenido:

```
proyecto_ejemplo
├── analysis_options.yaml
├── bin
│   └── proyecto_ejemplo.dart
├── CHANGELOG.md
├── pubspec.lock
├── pubspec.yaml
└── README.md
```

Donde además del `pubspec` y la carpeta `bin` encontramos un fichero para el control de cambios (`changelog`) un fichero readme o un .`gitignore`, entre otros.

Cuando trabajamos con Flutter, veremos que la estructura del proyecto es muy parecida, ya que un proyecto Flutter también es un proyecto Dart. La principal diferencia que encontraremos será que el código fuente estará ubicado en la carpeta `lib` en lugar de `bin`.

### **Paquetes y librerías: El gestor pub**

Dart hace uso de *paquetes* con el fin de gestionar software compartido, como puedan ser las bibliotecas u otros paquetes de utilidades.

El gestor de paquetes que utiliza Dart es `pub`, y nos permite cargar paquetes desde el sistema de ficheros locales o repositorios *Git*. No obstante, generalmente haremos uso del repositorio de paquetes público *pub.dev*. El gestor *pub* se encargará también de gestionar y descargar las dependencias entre paquetes, teniendo en cuenta la versión del SDK.

La mayoría de los IDE que permiten trabajar con Dart ofrecen soporte para utilizar *pub*, y permiten crear, descargar, actualizar o publicar paquetes. VSCode nos permite interactuar con el sistema *pub* a través de la extensión de *Dart*, así como añadir nuevas dependencias mediante la extensión *Pubspec Assist*.

Con el fin de añadir dependencias a un proyecto, podemos directamente editar este fichero *pubspec.yaml*, o bien utilizar el orden dart pub add.

Por ejemplo, añadiremos al proyecto `proyecto_ejemplo` la dependencia de la [librería http](https://pub.dev/packages/http), que utilizaremos en el siguiente apartado, y que se encarga de realizar y gestionar peticiones HTTP en la web. Para ello, tenemos varias opciones:

- **Opción 1. Añadir la librería desde la línea de órdenes**

Desde dentro del directorio del proyecto haríamos:

```
dart pub add http
```

Con lo que se nos afianza la línea siguiente al fichero `pubspec.yaml`, dentro de la sección `dependencies`:

```dart
http: ^1.2.2
```

- **Opción 2. Modificar el fichero `pubspec.yaml` directamente**

```dart
dependencies:
  http: ^1.2.2
```

- **Opción 3. Añadir la dependencia haciendo uso de la extensión Pubspec Assist**

Desde VSCode, podemos añadir la dependencia haciendo uso de la extensión Pubspec Assit. Para ello, activamos la paleta de órdenes de VSCode (con `Ctrl + Shift + P` en GNU/Linux y Windows o `Command+Shift+P` en Mac), y buscando el orden *Pubspec Assit: Add/update dependencies*.

Si nos encontramos en un directorio donde tengamos el fichero *pubspec.yaml*, nos pedirá qué extensión queremos instalar. Indicamos `http` y automáticamente se nos añadirá la dependencia al fichero.

**Descarga de librerías**

Cuando añadimos una dependencia desde la línea de órdenes (con dart pub get), y si hemos editado, siga como sea el fichero *pubspec.yaml* desde VSCode, el paquete se descarga automáticamente.

En caso de que hayamos modificado el fichero con otro editor, o bien que hemos obtenido un proyecto que no tiene todavía las dependencias descargadas, podemos descargarlas e instalarlas manualmente con el orden dart pub get (en Flutter, posteriormente, utilizaremos flutter pub get):

```
$ dart pub get
Resolving dependencies... 
Got dependencies!
```

Tal y como se indica en la [documentación oficial de Dart](https://dart.dev/tools/pub/cmd/pub-get#the-system-package-cache), y a diferencia de otras plataformas como nodejs o Java, las dependencias no se guardan en el mismo proyecto, sino en una *caché* de paquetes del sistema.

La idea es que, como hay varios paquetes que pueden utilizar la misma versión de una dependencia, ésta sólo se descargue una vez, y quede almacenada en esta memoria del sistema.

Si examinamos algún proyecto de Dart, veremos que hay un directorio oculto llamado `.dart\tool` que contiene un fichero `package\config.json`. Este fichero contiene información sobre las librerías que necesita el proyecto, las versiones, y en qué ubicación de esta *caché* se encuentran. La ubicación más habitual de la misma está en el directorio `~/.pub-cache/hosted/pub.dartlang.org/` de nuestra carpeta personal.

<br>
<br>

# <a name="_apartado9"></a>9. Peticiones HTTP

En este apartado realizaremos con Dart algunas consultas a la Web, utilizando la librería HTTP que instalamos en el apartado anterior.

## La librería [HTTP](https://pub.dev/packages/http)

En el apartado anterior ya hemos visto cómo incorporar la librería HTTP a nuestro proyecto, la cual nos permitirá llevar a cabo peticiones HTTP a cualquier recurso de red, haciendo uso de *Futures*.

La librería HTTP, internamente define un conjunto de clases y funciones de alto nivel para el consumo de recursos HTTP, como puedan ser las funciones `get()`, `post()`, `patch()`, `put()` o `delete()`, entre muchas otras.

La forma más sencilla de utilizar la biblioteca es importándola a nuestro código con:

```dart
import 'package:http/http.dart';
```

y hacer uso directamente de estas funciones de nivel superior (no asociadas a ningún objeto).

Otra opción bastante frecuente es definir un espacio de nombres como un *alias* bajo el cual referenciar toda la librería. Para ello, la importaremos de la siguiente forma:

```dart
import 'package:http/http.dart' as http;
```

De manera que accedemos a las funcionalidades que se nos ofrecen como si se trataran métodos del espacio de nombres *http*: `http.get()`, `http.post()`, etc.

## Ejemplo de uso

Vamos a utilizar la API REST que luego aplicaremos en nuestra práctica, que nos permite obtener información sobre continentes y países.

Concretamente, utilizaremos las siguientes rutas:

- [https://api-paises-uagm.onrender.com/continentes](https://api-paises-uagm.onrender.com/continentes), que devuelve el listado de continentes disponibles junto con una imagen representativa de cada uno.

- [https://api-paises-uagm.onrender.com/paises/$continente](https://api-paises-uagm.onrender.com/paises/$continente), que devuelve la lista de países pertenecientes al continente indicado.

- [https://api-paises-uagm.onrender.com/infopais/$pais](https://api-paises-uagm.detallada sobre el país solicitado.

A continuación, veremos, a modo de ejemplo, cómo obtendríamos el listado de continentes disponibles.

Para ello, en nuestro proyecto podemos editar el fichero `bin/proyecto_ejemplo.dart` y añadir el siguiente código:

```dart
// Importamos las librerías necesarias
import 'dart:convert'; // Para realizar conversiones entre tipos de datos
import 'package:http/http.dart' as http; // Para realizar peticiones HTTP

void main(List<String> args) {
  // Definimos el endpoint o dirección del recurso:
  String url =
      'https://api-paises-uagm.onrender.com/continentes';

  // Lanzamos una petición GET mediante el método http.get:
  Future<http.Response> response = http.get(Uri.parse(url));

  // Esta nos devuelve un Future, que habrá que procesar
  // con el método then:
  response.then((data) {

    // El Future se resuelve con un objeto Response,
    // que contiene el código de estado de la petición
    // y el cuerpo de la respuesta.

    if (data.statusCode == 200) {

      String body = utf8.decode(data.bodyBytes);
      final bodyJSON = jsonDecode(body) as List;

      // Mostramos el contenido recibido
      print(bodyJSON.toString());
    }
  });
}
```

Si ahora ejecutamos el proyecto con `dart run`, obtendremos el listado de continentes proporcionado por la API.

Aunque el código está bastante comentado, conviene hacer algunas puntualizaciones:

- Observemos que hemos importado dos librerías: **convert** y **http**. La librería **convert** forma parte de la biblioteca estándar de Dart, por lo que no ha sido necesario descargarla. Por este motivo se importa mediante `dart:`. Por otro lado, la librería **http** sí se ha descargado como paquete externo, de ahí que se importe mediante `package:`.

- Cuando realizamos la petición GET (`http.get()`), obtenemos un objeto de tipo `Future`, que procesamos mediante el método `then`. Este `Future` se resolverá con un objeto de tipo `Response`, que contiene, entre otras, las propiedades `statusCode` y `body`.

- Cuando el código de estado es **200 (OK)**, significa que la petición se ha completado correctamente y que disponemos de una respuesta válida. Otros códigos pueden indicar errores de cliente (4xx) o errores del servidor (5xx).

- Para descodificar el JSON recibido realizamos dos pasos. Primero descodificamos la respuesta en UTF-8 para evitar problemas con caracteres especiales:

```dart
String body = utf8.decode(data.bodyBytes);
```

Posteriormente convertimos el contenido recibido en una estructura de datos Dart mediante `jsonDecode()`:

```dart
final bodyJSON = jsonDecode(body) as List;
```

En este caso realizamos una conversión a `List`, ya que la ruta `/continentes` devuelve una lista de elementos.

Si intentáramos obtener el JSON directamente a partir de `data.body`:

```dart
final bodyJSON = jsonDecode(data.body) as List;
```

podríamos encontrarnos con problemas de codificación en determinados caracteres especiales o acentuados. Por este motivo se recomienda realizar previamente la conversión mediante `utf8.decode(data.bodyBytes)`.

<br>

## Ejemplo con async/await

En el ejemplo anterior, la respuesta HTTP se nos devuelve mediante un objeto de tipo *Future*. Si lo que queremos es esperar directamente a obtener la respuesta, sin utilizar el método `then()`, podemos hacer uso de la palabra reservada `await`:

```dart
var response = await http.get(Uri.parse(url));
```

Esto nos obliga, a su vez, a declarar la función que contiene el `await` como asíncrona mediante la palabra reservada `async`.

De esta manera, ya podemos trabajar directamente con la respuesta obtenida. El código completo quedaría:

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

void main(List<String> args) async {

  String url =
      'https://api-paises-uagm.onrender.com/continentes';

  // Lanzamos la petición GET.
  // Ahora response será de tipo Response y no un Future.
  http.Response response = await http.get(Uri.parse(url));

  if (response.statusCode == 200) {

    String body = utf8.decode(response.bodyBytes);
    final bodyJSON = jsonDecode(body) as List;

    print(bodyJSON.toString());
  }
}
```

Observemos la principal diferencia respecto al ejemplo anterior:

```dart
var response = await http.get(Uri.parse(url));
```

Al utilizar `await`, el programa espera a que finalice la petición HTTP antes de continuar con la siguiente instrucción. Además, la variable `response` ya no contiene un objeto de tipo `Future<Response>`, sino directamente un objeto de tipo `Response`.

Este mecanismo resulta especialmente útil cuando queremos escribir código asíncrono de forma más legible y cercana a una secuencia de instrucciones tradicional.

En la práctica de esta unidad encontraremos ambos enfoques:

- Utilizando el método `then()`, para procesar el resultado de un `Future` mediante una función de callback.

- Utilizando `async/await`, para obtener directamente el resultado de la operación asíncrona.

Ambas técnicas son equivalentes, y la elección de una u otra dependerá del estilo de programación utilizado y de las necesidades concretas de cada aplicación.