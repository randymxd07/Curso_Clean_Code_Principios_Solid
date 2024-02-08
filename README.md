# Curso de Clean Code y Principios SOLID

Esta es una guia basada en el curso de *Clean Code y Principios SOLID* de Fernando Herrera, en el que se enseñan conceptos y principios muy importantes para mantener el código lo más limpio posible y mantenible en el tiempo.

Este curso cubre una amplia gama de temas relacionados con la escritura de código limpio y la aplicación de principios sólidos de diseño de software. Desde técnicas para mejorar la legibilidad del código hasta pautas para estructurar proyectos de manera eficiente, este curso ofrece una sólida base para desarrolladores de todos los niveles.

El repositorio incluye:

* Ejemplos de código utilizados en el curso.
* Ejemplos de código generados usPando ChatGPT.
* Recursos adicionales recomendados por el instructor.

Para sacar el máximo provecho de este repositorio, se recomienda tener conocimientos básicos de programación y estar familiarizado con un lenguaje de programación, en esta guia se estara utilizando TypeScript, pero esto todo esto aplica para cualquier lenguaje de programacion.

**Autor:** *Randy Martínez* - Desarrollador Semi Senior.

**Inspirado Por:** *Fernando Herrera* - Desarrollador Senior y Instructor en Udemy.

# Índice

* [1. Clean Code y Deuda Tecnica](#1-clean-code-y-deuda-tecnica)
  * [1.1. Nombres de Variables](#11-nombres-de-variables)
  * [1.2. Nombres de Funciones](#12-nombres-de-funciones)
  * [1.3. Principio DRY (Don't Repeat Yourself)](#13-principio-dry-dont-repeat-yourself)

* [2. Clean Code - Clases y Comentarios](#2-clean-code---clases-y-comentarios)
  * [2.1. Clases](#21-clases)
  * [2.2. Principio de Responsabilidad Unica](#22-principio-de-responsabilidad-unica)
  * [2.3. Comentarios](#23-comentarios)
  * [2.4. Uniformidad en el Proyecto](#24-uniformidad-en-el-proyecto)

* [3. Acronimo STUPID](#3-acronimo-stupid)
  * [3.1. Singleton](#31-singleton)
  * [3.2. Tight Coupling](#32-tight-coupling)
  * [3.3. Units of Work](#33-units-of-work)
  * [3.4. Premature Optimization](#34-premature-optimization)
  * [3.5. Inconsistent](#35-inconsistent)
  * [3.6. Duplication](#36-duplication)

* [4. Principios SOLID](#4-principios-solid)
  * [4.1. Simple Responsability Principle (SRP)](#41-simple-responsability-principle-srp)
  * [4.2. Open / Closed Principle (OCP)](#42-open--closed-principle-ocp)
  * [4.3. Liskov Substitution Principle (LSP)](#43-liskov-substitution-principle-lsp)
  * [4.4. Interface Segregation Principle (ISP)](#44-interface-segregation-principle-isp)
  * [4.5. Dependency Inversion Principle (DIP)](#45-dependency-inversion-principle-dip)

# 1. Clean Code y Deuda Tecnica

Clean Code se refiere a la práctica de escribir código de software legible, comprensible y bien estructurado, siguiendo principios de diseño y programación que facilitan su mantenimiento y evolución. Por otro lado, la Deuda Técnica es el costo acumulado de tomar atajos o adoptar soluciones subóptimas durante el desarrollo, lo que puede resultar en una disminución de la calidad del código y una mayor dificultad para realizar cambios en el futuro. Gestionar la deuda técnica y mantener un código limpio son fundamentales para asegurar la calidad y la eficiencia a largo plazo en el desarrollo de software.

## 1.1. Nombres de Variables

Nombrar adecuadamente las variables es crucial para la claridad y la comprensión del código. Proporciona un contexto claro sobre qué representa cada variable y cómo se utiliza en el programa, lo que facilita su entendimiento para cualquier persona que lea el código, incluido el propio desarrollador en el futuro. Además, nombres descriptivos ayudan en la depuración, al identificar rápidamente la causa de los errores y en la documentación implícita del código, reduciendo la necesidad de explicaciones adicionales y fomentando buenas prácticas de programación.

```typescript
/**----------------------------------------------
 * BUENOS: Nombres descriptivos para variables
-------------------------------------------------*/

const userName: string = 'JohnDoe';

const numberOfItems: number = 10;

const isLoggedIn: boolean = true;

const userPreferences: UserPreferences = {
  darkMode: true,
  language: 'en'
};

/**--------------------------------------------------
 * MALOS: Nombres poco descriptivos para variables
-----------------------------------------------------*/

const x: string = 'JohnDoe'; // x no indica claramente qué representa

const a: number = 10; // a no proporciona información sobre el propósito de la variable

const flag: boolean = true; // flag es demasiado genérico y no indica su uso

const obj: any = {
    property1: 'value1',
    property2: 'value2'
}; // obj no describe el contenido del objeto de manera útil
```


## 1.2. Nombres de Funciones

Nombrar adecuadamente las funciones es esencial para la claridad y la organización del código. Proporciona una indicación clara de lo que hace cada función, permitiendo que otros desarrolladores comprendan rápidamente su propósito y cómo se integra en el sistema. Nombres descriptivos facilitan la identificación de funciones específicas durante el mantenimiento y la depuración del código, lo que mejora la eficiencia y reduce el tiempo necesario para realizar cambios. Además, una buena nomenclatura fomenta la coherencia en el diseño del software y contribuye a la legibilidad y mantenibilidad general del código.

```typescript
/**----------------------------------------------
 * BUENOS: Nombres descriptivos para funciones
-------------------------------------------------*/

// Función para calcular el área de un círculo
function calculateCircleArea(radius: number): number {
  return Math.PI * radius * radius;
}

// Función para validar una dirección de correo electrónico
function validateEmailAddress(email: string): boolean {
  // código para validar el formato del correo electrónico
}

// Función para obtener la suma de dos números
function addNumbers(a: number, b: number): number {
  return a + b;
}

// Función para cargar datos de usuario desde una API
async function fetchUserData(userId: string): Promise<UserData> {
  // código para obtener datos de usuario
}

// Función para actualizar la configuración del usuario
function updateUserSettings(userId: string, newSettings: UserSettings): void {
  // código para actualizar la configuración del usuario
}

/**--------------------------------------------------
 * MALOS: Nombres poco descriptivos para funciones
-----------------------------------------------------*/

// Nombre de función poco descriptivo
function doSomething(): void {
  // código
}

// Nombre de función poco claro sobre su propósito
function process(): void {
  // código
}

// Nombre de función que no indica su acción
function work(): void {
  // código
}

// Nombre de función demasiado genérico
function execute(input: any): void {
  // código
}

// Nombre de función que no describe lo que hace
function performAction(data: any): void {
  // código
}
```


## 1.3. Principio DRY (Don't Repeat Yourself)

La idea principal detrás del principio DRY es que cada pieza de conocimiento dentro de un sistema de software debería tener una representación única, no redundante y autoritativa dentro del sistema. Esto significa que el código, la lógica y los datos no deberían repetirse en múltiples lugares del sistema. En lugar de eso, deberían existir en un único lugar y ser referenciados según sea necesario.

**Ejemplo:**

Supongamos que estamos desarrollando una aplicación que gestiona empleados de una empresa. Cada empleado puede ser de tipo "gerente" o "trabajador", y ambos tienen propiedades comunes como el nombre, el salario y el método para calcular el salario anual. Podemos utilizar el principio DRY para evitar repetir estas propiedades y métodos comunes.

```typescript
// Definición de la interfaz base Employee
interface Employee {
  name: string;
  salary: number;
  calculateAnnualSalary(): number;
}

// Implementación de la clase Manager que implementa la interfaz Employee
class Manager implements Employee {

  constructor(public name: string, public salary: number) {}

  calculateAnnualSalary(): number {
    return this.salary * 12; // Suponiendo salario mensual
  }

}

// Implementación de la clase Worker que implementa la interfaz Employee
class Worker implements Employee {

  constructor(public name: string, public salary: number) {}

  calculateAnnualSalary(): number {
    return this.salary * 12; // Suponiendo salario mensual
  }
  
}

// Ejemplo de uso
const manager = new Manager("John Doe", 5000);
console.log("Gerente:");
console.log("Nombre:", manager.name);
console.log("Salario anual:", manager.calculateAnnualSalary());

const worker = new Worker("Jane Smith", 3000);
console.log("Trabajador:");
console.log("Nombre:", worker.name);
console.log("Salario anual:", worker.calculateAnnualSalary());
```

Hemos definido una interfaz Employee que especifica las propiedades y métodos comunes que deben implementar tanto los gerentes como los trabajadores. Creamos las clases Manager y Worker que implementan la interfaz Employee, proporcionando implementaciones concretas de los métodos y propiedades comunes.Luego, creamos instancias de Manager y Worker y utilizamos sus propiedades y métodos comunes, evitando la duplicación de código para estas características compartidas.

# 2. Clean Code - Clases y Comentarios

Clean Code promueve el concepto de "código autodocumentado", que significa que el código en sí mismo debería ser tan claro y expresivo que no requiera comentarios para entender su funcionamiento. Esto se logra escribiendo código con nombres descriptivos, estructuras simples y evitando la complejidad innecesaria. Los comentarios deberían utilizarse solo para aclarar decisiones de diseño o explicar situaciones excepcionales que no sean evidentes en el código.

## 2.1. Clases

En Clean Code, las clases deben ser pequeñas y tener una única responsabilidad, siguiendo el principio de Responsabilidad Única (SRP). Deben ser cohesivas, es decir, cada clase debe contener solo métodos y atributos relacionados con su responsabilidad. La cohesión y la encapsulación son principios importantes para diseñar clases eficientes y fáciles de entender. Se recomienda seguir convenciones de nombres claras y significativas para las clases y los métodos.

**Ejemplo de clases que no tienen responsabilidad unica:**

El siguiente código en TypeScript muestra un ejemplo de clases que representan a personas, usuarios y configuraciones de usuario. Sin embargo, viola el principio de responsabilidad única al hacer que las clases tengan múltiples responsabilidades, lo que puede conducir a un diseño poco mantenible y difícil de entender a medida que el código escala. Aquí hay algunos puntos a considerar:

**Principio de responsabilidad única:** Este principio establece que una clase debe tener una sola razón para cambiar. En este ejemplo, las clases User y UserSettings tienen múltiples responsabilidades, como gestionar información de usuario, credenciales y configuraciones de usuario. Es preferible dividir estas responsabilidades en clases separadas para tener un diseño más cohesivo y fácil de mantener.

**Herencia:** El uso extensivo de la herencia puede acoplar demasiado las clases, lo que puede dificultar la modificación y extensión del código en el futuro. En lugar de heredar propiedades y métodos de una clase base (Person en este caso), considere el uso de composición o interfaces para definir comportamientos comunes.

**Constructores sobrecargados:** Los constructores de las clases User y UserSettings tienen una lista larga de parámetros, lo que puede hacer que la creación de instancias sea confusa y propensa a errores. Considere utilizar objetos de opciones o una estructura de datos más compacta para inicializar las clases.

**Acoplamiento fuerte:** Existe un alto acoplamiento entre las clases User y UserSettings, ya que UserSettings hereda de User. Esto puede hacer que el código sea más difícil de mantener, ya que un cambio en una clase puede afectar inadvertidamente a la otra.

```typescript
// No aplicando el principio de responsabilidad única

type Gender = 'M'|'F';

class Person {

  constructor(
    public name: string, 
    public gender: Gender, 
    public birthdate: Date
  ){}

}

class User extends Person {
    
  public lastAccess: Date;

  constructor(
    public email: string,
    public role: string,
    name: string,
    gender: Gender,
    birthdate: Date,
  ) {
    super( name, gender, birthdate );
    this.lastAccess = new Date();
  }

  checkCredentials() {
    return true;
  }

}

class UserSettings extends User {
  
  constructor(
    public workingDirectory: string,
    public lastOpenFolder  : string,
    email                  : string,
    role                   : string,
    name                   : string,
    gender                 : Gender,
    birthdate              : Date
  ) {
    super(email, role, name, gender, birthdate );
  }

}

const userSettings = new UserSettings(
  '/usr/home',
  '/home',
  'fernando@google.com',
  'Admin',
  'Fernando',
  'M',
  new Date('1985-10-21')
);

console.log({ userSettings });
```

Si no se respeta el principio de responsabilidad única y se quiere hacer un cambio en una de las clases, es probable que se enfrenten dificultades significativas en términos de comprensión, mantenimiento y extensión del código. Es importante revisar y refactorizar el diseño del sistema para cumplir con los principios de diseño sólidos y mejorar la modularidad y la mantenibilidad del código.

## 2.2. Principio de Responsabilidad Unica

El principio de responsabilidad única (Single Responsibility Principle, SRP) es un principio de diseño de software propuesto por Robert C. Martin, que sugiere que cada clase o módulo debería tener una única responsabilidad. En otras palabras, una clase debe tener solo una razón para cambiar. Este principio promueve la cohesión y la modularidad en el diseño del software, lo que a su vez facilita el mantenimiento, la comprensión y la reutilización del código.

**Ejemplo:**

```typescript
// Aplicando el principio de responsabilidad única
// Priorizar la composición frente a la herencia!

type Gender = 'M'|'F';

interface PersonProps {
  birthdate : Date;
  gender    : Gender;
  name      : string;
}

class Person {

  public birthdate: Date;
  public gender   : Gender;
  public name     : string;

  constructor({ name, gender, birthdate }: PersonProps ){
    this.name      = name;
    this.gender    = gender;
    this.birthdate = birthdate;
  }

}

interface UserProps {
  email     : string;
  role      : string;
}

class User {
    
  public email      : string;
  public lastAccess : Date;
  public role       : string;

  constructor({
    email,
    role,
  }: UserProps ) {
    this.lastAccess = new Date();
    this.email = email;
    this.role  = role;
  }

  checkCredentials() {
    return true;
  }

}

interface SettingsProps {
  lastOpenFolder   : string;
  workingDirectory : string;
}

class Settings {

  public workingDirectory: string;
  public lastOpenFolder  : string;

  constructor({
    lastOpenFolder,
    workingDirectory,
  }: SettingsProps ) {
    this.lastOpenFolder   = lastOpenFolder;
    this.workingDirectory = workingDirectory;
  }

}

interface UserSettingsProps {
  birthdate        : Date;
  email            : string;
  gender           : Gender;
  lastOpenFolder   : string;
  name             : string;
  role             : string;
  workingDirectory : string;
}

class UserSettings {

  public person  : Person;
  public user    : User;
  public settings: Settings;

  constructor({
    name, gender, birthdate,
    email, role,
    lastOpenFolder, workingDirectory,
  }: UserSettingsProps ){
    this.person = new Person({ name, gender, birthdate });
    this.user = new User({ email, role });
    this.settings = new Settings({ lastOpenFolder, workingDirectory })
  }

}

const userSettings = new UserSettings({
  birthdate: new Date('1985-10-21'),
  email: 'fernando@google.com',
  gender: 'M',
  lastOpenFolder: '/home',
  name: 'Fernando',
  role: 'Admin',
  workingDirectory: '/usr/home',
});

console.log({ userSettings });
```

Agregar un campo a una clase que sigue el principio de responsabilidad única suele ser más fácil y menos arriesgado que hacerlo en una clase que viola este principio. Esto se debe a la claridad del contexto, el menor riesgo de efectos secundarios, la mejor separación de preocupaciones y la facilidad de mantenimiento que ofrece una clase con una única responsabilidad.

## 2.3. Comentarios

Los comentarios en el código deben ser usados con moderación. Un código limpio debería ser autoexplicativo en la medida de lo posible. Los comentarios deben explicar el porqué de las decisiones de diseño o implementación, en lugar de describir lo que el código hace. El "qué" debería ser evidente leyendo el código. Los comentarios deben mantenerse actualizados. Comentarios obsoletos o incorrectos pueden llevar a confusión y reducir la legibilidad del código. En lugar de comentarios largos, se prefieren nombres descriptivos de variables, métodos y clases.

**Ejemplos:**

Explicación de decisiones de diseño o implementación:

```typescript
// Uso de una interfaz en lugar de tipos anidados para mejorar la legibilidad y reutilización del código.
interface Usuario {
  nombre: string;
  edad: number;
  email: string;
}

function enviarCorreo(usuario: Usuario, mensaje: string) {
  // Implementación de envío de correo electrónico aquí...
}
```

Mantener actualizados los comentarios:

```typescript
// Función para calcular el área de un círculo.
function calcularAreaCirculo(radio: number) {

  // Fórmula para calcular el área de un círculo: A = π * r^2
  return Math.PI * radio ** 2;

}
```

Nombres descriptivos en lugar de comentarios largos:

```typescript
// Clase para representar un estudiante en un sistema de gestión escolar.
class Estudiante {

  nombre: string;
  edad: number;
  grado: string;

  constructor(nombre: string, edad: number, grado: string) {
    this.nombre = nombre;
    this.edad = edad;
    this.grado = grado;
  }

}
```

Comentarios explicativos solo cuando sea necesario:

```typescript
function validarEdad(edad: number): boolean {

  // Verificar si la edad es un número positivo.
  if (edad >= 0) {

    return true;

  } else {

    return false;

  }

}
```

Recuerda que en TypeScript, al igual que en JavaScript, el código debe ser claro y autoexplicativo en la medida de lo posible. Los comentarios deben usarse para proporcionar información adicional o explicar decisiones de diseño que no sean evidentes leyendo el código.

## 2.4. Uniformidad en el Proyecto

La uniformidad en un proyecto que sigue los principios de Clean Code es fundamental para garantizar la legibilidad y mantenibilidad del código. Clean Code se centra en escribir código claro, conciso y fácilmente comprensible, lo que facilita su colaboración y evolución a lo largo del tiempo. Aquí hay algunos puntos clave sobre la uniformidad en un proyecto que utiliza Clean Code:

**1. Convenciones de nomenclatura:** Es importante establecer convenciones de nomenclatura consistentes para variables, funciones, clases, métodos, etc. Esto ayuda a los desarrolladores a entender rápidamente el propósito y el uso de cada componente del código.

**2. Estilo de codificación:** Mantener un estilo de codificación uniforme en todo el proyecto ayuda a que el código sea más legible y coherente. Esto incluye aspectos como el uso de espacios en blanco, la indentación, la longitud de línea y el uso de comentarios.

**3. Patrones de diseño:** Al seguir patrones de diseño consistentes, se facilita la comprensión del código y se promueve la coherencia en la arquitectura del software.

**4. Consistencia en la estructura del código:** La estructura del código, como la organización de los archivos y la división en módulos o componentes, debe mantenerse uniforme en todo el proyecto. Esto ayuda a los desarrolladores a encontrar rápidamente la funcionalidad que están buscando.

**5. Reutilización de código:** Siguiendo los principios de Clean Code, se fomenta la reutilización de código en lugar de duplicarlo. Esto promueve la consistencia y reduce la redundancia en el proyecto.

**6. Pruebas unitarias consistentes:** Las pruebas unitarias son una parte integral de escribir un código limpio y de alta calidad. Mantener pruebas unitarias consistentes y actualizadas garantiza que el código funcione correctamente y que los cambios no introduzcan errores inesperados.

La uniformidad en un proyecto que sigue los principios de Clean Code es esencial para mantener la calidad del código a lo largo del tiempo, facilitar la colaboración entre desarrolladores y garantizar que el software sea fácilmente comprensible y mantenible.

# 3. Acronimo STUPID

El acrónimo *STUPID* es una forma de resumir algunas características no deseables en el diseño de software. Cada letra representa un concepto que se debe evitar al desarrollar programas de computadora de calidad. Aquí está el desglose:

**Acrónimos:**

* Singleton
* Tight Coupling (Acoplamiento Estrecho)
* Units of Work (Unidades de Trabajo)
* Premature Optimization (Optimización Prematura)
* Inconsistent (Inconsistente) 
* Duplication (Duplicación)

## 3.1. Singleton

Hace referencia al patrón de diseño Singleton, que implica tener una única instancia de una clase en un programa. Aunque puede ser útil en algunos casos, su uso excesivo puede provocar acoplamiento fuerte y dificultar las pruebas unitarias y el mantenimiento del código.

## 3.2. Tight Coupling:

Se refiere a la interdependencia excesiva entre componentes de un sistema de software. Un alto acoplamiento dificulta la reutilización de código, la modificación y la escalabilidad.

## 3.3. Units of Work

Se refiere a la falta de modularidad en el diseño, lo que significa que una pieza de código realiza demasiadas tareas diferentes. Esto puede dificultar la comprensión del código y aumentar la complejidad.

## 3.4. Premature Optimization

Es la práctica de intentar optimizar el código antes de que sea necesario. Esto puede conducir a un código más complejo y difícil de mantener sin proporcionar necesariamente mejoras significativas en el rendimiento.

## 3.5. Inconsistent

Hace referencia a la falta de coherencia en el diseño o la implementación del software. La inconsistencia puede dificultar la comprensión del código y aumentar la posibilidad de errores.

## 3.6. Duplication

Se refiere a la repetición innecesaria de código en un sistema. La duplicación aumenta el riesgo de errores y hace que el código sea más difícil de mantener.

# 4. Principios SOLID

Los principios SOLID son un conjunto de directrices para el diseño de software orientado a objetos que promueven la creación de código limpio, modular y fácil de mantener. Estos principios, introducidos por Robert C. Martin, también conocido como "Uncle Bob", proporcionan una base sólida para desarrollar sistemas de software robustos y adaptables a los cambios.

**Principios:**

* Simple Responsability Principle (SRP)
* Open / Closed Principle (OCP)
* Liskov Substitution Principle (LSP)
* Interface Segregation Principle (ISP)
* Dependency Inversion Principle (DIP)

## 4.1. Simple Responsability Principle (SRP)

Se trata de un principio que busca hacer que cada clase tenga una unica responsabilidad y que no dependa de otra, esto para evitar que cuando se hagan cambios en una clase otra sea afectada.

**Ejemplo:**

Supongamos que tenemos una clase llamada Empleado que maneja tanto la lógica relacionada con la gestión de empleados como la lógica relacionada con la generación de reportes. Esto violaría el principio de responsabilidad única. Para corregirlo, dividiremos esta clase en dos clases separadas: Empleado y GeneradorDeReportes.

```typescript
// Clase Empleado con una única responsabilidad
class Empleado {

  private nombre: string;
  private salario: number;

  constructor(nombre: string, salario: number) {
    this.nombre = nombre;
    this.salario = salario;
  }

  // Métodos relacionados con la gestión de empleados
  public getNombre(): string {
    return this.nombre;
  }

  public getSalario(): number {
    return this.salario;
  }

}

// Clase GeneradorDeReportes con una única responsabilidad
class GeneradorDeReportes {

  public generarReporteParaEmpleado(empleado: Empleado): string {
    // Lógica para generar el reporte del empleado
    return `Reporte del empleado ${empleado.getNombre()}: Salario - ${empleado.getSalario()}`;
  }

}

// Uso de las clases
const empleado = new Empleado("Juan", 3000);
const generadorDeReportes = new GeneradorDeReportes();

const reporteEmpleado = generadorDeReportes.generarReporteParaEmpleado(empleado);
console.log(reporteEmpleado);
```

En este ejemplo, la clase Empleado se encarga únicamente de la gestión de los datos de un empleado (nombre y salario), mientras que la clase GeneradorDeReportes se encarga exclusivamente de generar reportes para los empleados. Esto sigue el principio de responsabilidad única, ya que cada clase tiene una única razón para cambiar: cambios en la gestión de empleados y cambios en la generación de reportes, respectivamente.

## 4.2. Open / Closed Principle (OCP)

Se trata de un principio que busca que las clases puedan extender sus funcionalidades sin la necesidad de ser modificadas, osea que una clase debería permitir que su funcionalidad pueda ser extendida mediante la adición de nuevas funcionalidades (metodos), pero sin necesidad de modificar el código fuente de la clase original.

**Ejemplo:**

Supongamos que tenemos una clase Shape que representa diversas formas geométricas y queremos calcular el área de estas formas. Para cumplir con el principio OCP, diseñaremos nuestra implementación de manera que sea fácil de extender sin modificar la clase Shape:

```typescript
abstract class Shape {
  abstract calculateArea(): number;
}

class Rectangle extends Shape {

  constructor(private width: number, private height: number) {
    super();
  }

  calculateArea(): number {
    return this.width * this.height;
  }

}

class Circle extends Shape {

  constructor(private radius: number) {
    super();
  }

  calculateArea(): number {
    return Math.PI * Math.pow(this.radius, 2);
  }

}

// Podemos extender la funcionalidad sin modificar las clases existentes
class Square extends Shape {

  constructor(private sideLength: number) {
    super();
  }

  calculateArea(): number {
    return Math.pow(this.sideLength, 2);
  }

}

// Esta función utiliza polimorfismo para calcular el área de cualquier forma
function calculateTotalArea(shapes: Shape[]): number {

  let totalArea = 0;

  for (const shape of shapes) {
    totalArea += shape.calculateArea();
  }

  return totalArea;

}

// Ejemplo de uso
const rectangle = new Rectangle(5, 10);
const circle = new Circle(7);
const square = new Square(4);

const totalArea = calculateTotalArea([rectangle, circle, square]);
console.log("El área total es:", totalArea);
```

En este ejemplo, la clase Shape es una clase abstracta que define un método calculateArea() que debe ser implementado por sus subclases. Las clases Rectangle, Circle y Square extienden Shape y proporcionan su propia implementación del método calculateArea(). Esto significa que podemos agregar nuevas formas geométricas sin tener que modificar las clases existentes, cumpliendo así con el principio OCP.

## 4.3. Liskov Substitution Principle (LSP)

Se trata de un principio que busca que las clases que extiendan de una clase principal puedan implementar los metodos que tenga dicha clase principal y que si estoy implementando una de estas subclases puedo sustituirlas por la clase principal y viserversa si estoy implementando la clase principal puedo sustituirla por una de las subclases que se extienden o heredan de esta clase principal sin afectar el funcionamiento del programa.

**Ejemplo:**

Supongamos que tenemos una clase base Shape que representa una forma geométrica y una clase derivada Circle que representa un círculo. Queremos garantizar que la clase Circle pueda ser usada en lugar de la clase base Shape sin cambiar el comportamiento esperado:

```typescript
class Shape {

  protected _area: number;

  constructor() {
    this._area = 0;
  }

  get area(): number {
    return this._area;
  }

}

class Circle extends Shape {

  private _radius: number;

  constructor(radius: number) {
    super();
    this._radius = radius;
    this.calculateArea();
  }

  private calculateArea(): void {
    this._area = Math.PI * Math.pow(this._radius, 2);
  }

}

function calculateTotalArea(shapes: Shape[]): number {

  let totalArea: number = 0;

  shapes.forEach(shape => {
    totalArea += shape.area;
  });

  return totalArea;

}

// Uso de las clases
const shapes: Shape[] = [
  new Circle(5),
  new Circle(10),
  new Circle(15)
];

console.log("Área total de las formas:", calculateTotalArea(shapes));
```

En este ejemplo, la clase Circle hereda de Shape y no altera el comportamiento del método calculateTotalArea(). Podemos usar instancias de Circle en lugar de instancias de Shape sin afectar la funcionalidad del programa. Esto cumple con el principio de sustitución de Liskov.

## 4.4. Interface Segregation Principle (ISP)

Se trata de un principio que busca que las clases utilicen solo las interfaces que necesiten, puede que hayan clases que compartan interfaces pero siembre habra alguna propiedad que solo este disponible en una clase y en otra no por lo que se crea una interfaz con las propiedades que sean comunes para todas las clases y se crean interfaces especificas exclusivamente para las clases que son similares pero que manejan otro tipo de metodos o propiedades

**Ejemplo:**

El siguiente ejemplo es un buen caso de aplicación del Principio de Segregación de Interfaces (ISP). En este ejemplo, se tienen varias interfaces que representan diferentes capacidades de aves, como volar, correr y nadar. Cada clase que implementa estas interfaces lo hace según sus capacidades específicas, lo que garantiza que cada clase tenga solo los métodos relevantes para su funcionalidad.

```typescript
interface Bird {
  eat(): void;
}

interface FlyingBird {
  fly(): number;
}

interface RunningBird {
  run(): void;
}

interface SwimmerBird {
  swim(): void;
}

class Tucan implements Bird, FlyingBird {
  public fly() { return 100; }
  public eat() {}
}

class Humminbird implements Bird, FlyingBird {
  public fly() { return 200; }
  public eat() {}
}

class Ostrich implements Bird, RunningBird {
  public eat() {}
  public run() {}
}

class Penguin implements Bird, SwimmerBird {
  public eat() {}
  public swim() {}
}
```

Este ejemplo muestra cómo la aplicación del ISP puede conducir a un diseño de código más limpio y cohesivo, donde las clases están más enfocadas y tienen una mejor separación de responsabilidades.

## 4.5. Dependency Inversion Principle (DIP)

La inversión de dependencias se trata de organizar el código de manera que las partes de un sistema no dependan directamente unas de otras, sino que dependan de abstracciones comunes. En lugar de que los detalles dependan de la implementación específica, se depende de interfaces o clases abstractas que definen un comportamiento general.

En este principio se establece que los módulos de alto nivel no deben depender de los detalles de implementación de los módulos de bajo nivel, sino que ambos deben depender de abstracciones. Este principio promueve la modularidad y la flexibilidad del diseño al reducir el acoplamiento entre los componentes del sistema.

**Ejemplo con una Interfaz:**

Supongamos que estamos desarrollando un sistema de gestión de empleados, donde tenemos diferentes tipos de empleados (por ejemplo, permanentes y contratados) y queremos calcular sus salarios. Utilizaremos el principio de inversión de dependencias para asegurarnos de que el cálculo de salario no dependa directamente de las implementaciones concretas de los tipos de empleados.

```typescript
// Definimos una interfaz para el tipo de empleado
interface Empleado {
  calcularSalario(): number;
}

// Implementación para el tipo de empleado permanente
class EmpleadoPermanente implements Empleado {

  calcularSalario(): number {
    // Lógica específica para calcular el salario de un empleado permanente
    return 50000; // Ejemplo de salario fijo para empleado permanente
  }

}

// Implementación para el tipo de empleado contratado
class EmpleadoContratado implements Empleado {

  calcularSalario(): number {
    // Lógica específica para calcular el salario de un empleado contratado
    return 20000; // Ejemplo de salario fijo para empleado contratado
  }

}

// Clase principal que utiliza la interfaz Empleado para calcular los salarios
class GestorDeSalarios {

  calcularSalarioParaEmpleado(empleado: Empleado): number {
    return empleado.calcularSalario(); // No importa qué tipo de empleado sea, utilizamos la interfaz
  }

}

// Uso del código
const empleadoPermanente = new EmpleadoPermanente();
const empleadoContratado = new EmpleadoContratado();

const gestorSalarios = new GestorDeSalarios();
console.log("Salario del empleado permanente:", gestorSalarios.calcularSalarioParaEmpleado(empleadoPermanente));
console.log("Salario del empleado contratado:", gestorSalarios.calcularSalarioParaEmpleado(empleadoContratado));
```

En este ejemplo, hemos definido una interfaz Empleado que tiene un método calcularSalario(). Luego, tenemos dos clases concretas EmpleadoPermanente y EmpleadoContratado que implementan esta interfaz y proporcionan su propia lógica para calcular salarios.

Finalmente, tenemos una clase GestorDeSalarios que toma un objeto Empleado como entrada y llama al método calcularSalario() sin preocuparse por la implementación concreta del empleado. Esto demuestra cómo el cálculo de salarios depende de la interfaz Empleado, no de las implementaciones concretas de los tipos de empleados, siguiendo así el principio de inversión de dependencias.

**Ejemplo con una Clase Abstracta y Inyeccion de Dependencias:**

Supongamos que estamos desarrollando una aplicación de envío de mensajes que puede enviar mensajes a diferentes destinos, como correo electrónico, SMS o notificaciones push. Queremos asegurarnos de que el envío de mensajes no dependa directamente de las implementaciones concretas de los destinatarios, sino de una abstracción común.

```typescript
// Definimos una clase abstracta para el destinatario del mensaje
abstract class DestinatarioMensaje {
  abstract enviarMensaje(mensaje: string): void;
}

// Implementación para el destinatario de mensajes por correo electrónico
class DestinatarioEmail extends DestinatarioMensaje {

  enviarMensaje(mensaje: string): void {
    console.log(`Enviando correo electrónico: ${mensaje}`);
    // Lógica para enviar correo electrónico
  }

}

// Implementación para el destinatario de mensajes por SMS
class DestinatarioSMS extends DestinatarioMensaje {

  enviarMensaje(mensaje: string): void {
    console.log(`Enviando SMS: ${mensaje}`);
    // Lógica para enviar SMS
  }

}

// Implementación para el destinatario de mensajes por notificación push
class DestinatarioPush extends DestinatarioMensaje {

  enviarMensaje(mensaje: string): void {
    console.log(`Enviando notificación push: ${mensaje}`);
    // Lógica para enviar notificación push
  }

}

// Clase principal que utiliza la abstracción DestinatarioMensaje para enviar mensajes
// Acá se está haciendo la inyeccion de dependencias
class GestorMensajes {

  constructor(private destinatario: DestinatarioMensaje) {}

  enviarMensaje(mensaje: string): void {
    this.destinatario.enviarMensaje(mensaje); // Utilizamos la abstracción
  }

}

// Uso del código con inyección de dependencias
const gestorEmail = new GestorMensajes(new DestinatarioEmail());
gestorEmail.enviarMensaje("Hola, ¿cómo estás?");

const gestorSMS = new GestorMensajes(new DestinatarioSMS());
gestorSMS.enviarMensaje("¡Recuerda tu cita mañana!");

const gestorPush = new GestorMensajes(new DestinatarioPush());
gestorPush.enviarMensaje("Tienes una nueva solicitud de amistad.");
```

En este ejemplo, hemos definido una clase abstracta DestinatarioMensaje que tiene un método enviarMensaje(). Luego, tenemos tres clases concretas que implementan esta clase abstracta para enviar mensajes por correo electrónico, SMS y notificaciones push.

La clase GestorMensajes toma un objeto DestinatarioMensaje en su constructor (inyección de dependencias) y utiliza su método enviarMensaje() sin preocuparse por la implementación concreta del destinatario. Esto muestra cómo el envío de mensajes depende de la abstracción DestinatarioMensaje, no de las implementaciones concretas de los destinatarios, siguiendo así el principio de inversión de dependencias.