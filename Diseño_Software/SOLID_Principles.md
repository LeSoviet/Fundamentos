# Principios SOLID de Diseño de Software

SOLID es un acrónimo que representa cinco principios fundamentales de diseño orientado a objetos que ayudan a crear software más mantenible, flexible y comprensible. Estos principios fueron introducidos por Robert C. Martin ("Uncle Bob") y son esenciales para cualquier desarrollador que quiera escribir código de calidad.

## S - Single Responsibility Principle (Principio de Responsabilidad Única)

### Definición
Una clase debe tener una sola razón para cambiar, es decir, una sola responsabilidad.

### Explicación
Cada clase o módulo debe tener una única razón para existir y una única razón para cambiar. Si una clase tiene múltiples responsabilidades, los cambios en una responsabilidad podrían afectar negativamente a las otras.

### Ejemplo que VIOLA el principio:
```javascript
// Violación del SRP
class Usuario {
    constructor(nombre, email) {
        this.nombre = nombre;
        this.email = email;
    }
    
    // Responsabilidad 1: Gestión de datos del usuario
    guardarEnBaseDeDatos() {
        // Código para guardar en base de datos
    }
    
    // Responsabilidad 2: Envío de emails
    enviarEmailBienvenida() {
        // Código para enviar email
    }
    
    // Responsabilidad 3: Generación de reportes
    generarReporte() {
        // Código para generar reporte
    }
}
```

### Ejemplo que CUMPLE el principio:
```javascript
// Cumple con SRP
class Usuario {
    constructor(nombre, email) {
        this.nombre = nombre;
        this.email = email;
    }
    
    // Solo responsabilidad: datos del usuario
    getNombre() {
        return this.nombre;
    }
    
    getEmail() {
        return this.email;
    }
}

class UsuarioRepositorio {
    guardar(usuario) {
        // Código para guardar en base de datos
    }
}

class EmailService {
    enviarBienvenida(usuario) {
        // Código para enviar email
    }
}

class ReporteService {
    generarReporte(usuario) {
        // Código para generar reporte
    }
}
```

### Beneficios:
- Mayor cohesión
- Menor acoplamiento
- Más fácil de entender y mantener
- Más fácil de probar

## O - Open/Closed Principle (Principio Abierto/Cerrado)

### Definición
Las entidades de software (clases, módulos, funciones, etc.) deben estar abiertas para extensión pero cerradas para modificación.

### Explicación
Debes poder extender el comportamiento de una clase sin modificar su código fuente. Esto se logra mediante el uso de abstracciones como interfaces o clases abstractas.

### Ejemplo que VIOLA el principio:
```javascript
// Violación del OCP
class Calculadora {
    calcular(tipo, a, b) {
        if (tipo === "suma") {
            return a + b;
        } else if (tipo === "resta") {
            return a - b;
        } else if (tipo === "multiplicacion") {
            return a * b;
        }
        // Si queremos añadir división, tenemos que modificar esta clase
    }
}
```

### Ejemplo que CUMPLE el principio:
```javascript
// Cumple con OCP
class Operacion {
    calcular(a, b) {
        throw new Error("Método calcular debe ser implementado");
    }
}

class Suma extends Operacion {
    calcular(a, b) {
        return a + b;
    }
}

class Resta extends Operacion {
    calcular(a, b) {
        return a - b;
    }
}

class Multiplicacion extends Operacion {
    calcular(a, b) {
        return a * b;
    }
}

// Para añadir división, creamos una nueva clase sin modificar las existentes
class Division extends Operacion {
    calcular(a, b) {
        if (b === 0) throw new Error("División por cero");
        return a / b;
    }
}

class Calculadora {
    calcular(operacion, a, b) {
        return operacion.calcular(a, b);
    }
}
```

### Beneficios:
- Menos riesgo de introducir bugs
- Mayor reusabilidad
- Más fácil de mantener
- Mayor flexibilidad

## L - Liskov Substitution Principle (Principio de Sustitución de Liskov)

### Definición
Los objetos de una superclase deben poder ser reemplazados por objetos de una subclase sin afectar la corrección del programa.

### Explicación
Las subclases deben poder sustituir a sus clases base sin cambiar el comportamiento esperado del programa. Las subclases deben cumplir con el contrato definido por la clase base.

### Ejemplo que VIOLA el principio:
```javascript
// Violación del LSP
class Rectangulo {
    constructor(ancho, alto) {
        this.ancho = ancho;
        this.alto = alto;
    }
    
    setAncho(ancho) {
        this.ancho = ancho;
    }
    
    setAlto(alto) {
        this.alto = alto;
    }
    
    getArea() {
        return this.ancho * this.alto;
    }
}

class Cuadrado extends Rectangulo {
    constructor(lado) {
        super(lado, lado);
    }
    
    setAncho(ancho) {
        // Violación: cambia el comportamiento esperado
        this.ancho = ancho;
        this.alto = ancho; // Ambos deben ser iguales
    }
    
    setAlto(alto) {
        // Violación: cambia el comportamiento esperado
        this.ancho = alto; // Ambos deben ser iguales
        this.alto = alto;
    }
}

// Código que espera un Rectangulo
function testRectangulo(rectangulo) {
    rectangulo.setAncho(10);
    rectangulo.setAlto(5);
    console.log(rectangulo.getArea()); // Espera 50, pero con Cuadrado da 25
}
```

### Ejemplo que CUMPLE el principio:
```javascript
// Cumple con LSP
class Forma {
    getArea() {
        throw new Error("Método getArea debe ser implementado");
    }
}

class Rectangulo extends Forma {
    constructor(ancho, alto) {
        super();
        this.ancho = ancho;
        this.alto = alto;
    }
    
    getArea() {
        return this.ancho * this.alto;
    }
}

class Cuadrado extends Forma {
    constructor(lado) {
        super();
        this.lado = lado;
    }
    
    getArea() {
        return this.lado * this.lado;
    }
}

// Ahora cada clase maneja su propio comportamiento
function testForma(forma) {
    console.log(forma.getArea()); // Comportamiento predecible
}
```

### Beneficios:
- Mayor predictibilidad del código
- Menos errores al usar polimorfismo
- Mejor diseño de jerarquías de clases

## I - Interface Segregation Principle (Principio de Segregación de Interfaces)

### Definición
Muchas interfaces específicas son mejores que una interfaz general.

### Explicación
Los clientes no deben verse obligados a depender de métodos que no utilizan. Es mejor tener varias interfaces pequeñas y específicas que una interfaz grande y general.

### Ejemplo que VIOLA el principio:
```javascript
// Violación del ISP
class Maquina {
    imprimir() { }
    escanear() { }
    fax() { }
    copiar() { }
}

class ImpresoraBasica extends Maquina {
    imprimir() {
        // Implementación real
    }
    
    // ¿Qué hacemos con estos métodos?
    escanear() {
        throw new Error("No soportado");
    }
    
    fax() {
        throw new Error("No soportado");
    }
    
    copiar() {
        throw new Error("No soportado");
    }
}
```

### Ejemplo que CUMPLE el principio:
```javascript
// Cumple con ISP
class Imprimible {
    imprimir() {
        throw new Error("Método imprimir debe ser implementado");
    }
}

class Escaneable {
    escanear() {
        throw new Error("Método escanear debe ser implementado");
    }
}

class Faxable {
    fax() {
        throw new Error("Método fax debe ser implementado");
    }
}

class Copiable {
    copiar() {
        throw new Error("Método copiar debe ser implementado");
    }
}

// Implementaciones específicas
class ImpresoraBasica extends Imprimible {
    imprimir() {
        // Implementación real
        console.log("Imprimiendo...");
    }
}

class ImpresoraMultifuncion extends Imprimible {
    imprimir() {
        console.log("Imprimiendo...");
    }
    
    escanear() {
        console.log("Escaneando...");
    }
    
    fax() {
        console.log("Enviando fax...");
    }
    
    copiar() {
        console.log("Copiando...");
    }
}
```

### Beneficios:
- Mayor flexibilidad
- Menos métodos innecesarios
- Mejor mantenibilidad
- Menos acoplamiento

## D - Dependency Inversion Principle (Principio de Inversión de Dependencias)

### Definición
1. Los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambos deben depender de abstracciones.
2. Las abstracciones no deben depender de detalles. Los detalles deben depender de abstracciones.

### Explicación
Depende de abstracciones (interfaces, clases abstractas) en lugar de implementaciones concretas. Esto facilita el cambio de implementaciones sin afectar el código que las usa.

### Ejemplo que VIOLA el principio:
```javascript
// Violación del DIP
class MySQLDatabase {
    guardar(usuario) {
        // Código específico para MySQL
        console.log("Guardando en MySQL");
    }
}

class UsuarioService {
    constructor() {
        // Dependencia directa de una implementación concreta
        this.database = new MySQLDatabase();
    }
    
    guardarUsuario(usuario) {
        this.database.guardar(usuario);
    }
}
```

### Ejemplo que CUMPLE el principio:
```javascript
// Cumple con DIP
class DatabaseInterface {
    guardar(usuario) {
        throw new Error("Método guardar debe ser implementado");
    }
}

class MySQLDatabase extends DatabaseInterface {
    guardar(usuario) {
        // Código específico para MySQL
        console.log("Guardando en MySQL");
    }
}

class PostgreSQLDatabase extends DatabaseInterface {
    guardar(usuario) {
        // Código específico para PostgreSQL
        console.log("Guardando en PostgreSQL");
    }
}

class UsuarioService {
    constructor(database) {
        // Depende de una abstracción, no de una implementación concreta
        this.database = database;
    }
    
    guardarUsuario(usuario) {
        this.database.guardar(usuario);
    }
}

// Uso
const mysqlDB = new MySQLDatabase();
const usuarioService = new UsuarioService(mysqlDB);
usuarioService.guardarUsuario(usuario);

// Fácil de cambiar a otra implementación
const postgresDB = new PostgreSQLDatabase();
const otroUsuarioService = new UsuarioService(postgresDB);
```

### Beneficios:
- Mayor flexibilidad
- Más fácil de testear
- Menor acoplamiento
- Más fácil de mantener

## Aplicando SOLID en la Práctica

### Consejos para Implementar SOLID:

1. **Comienza con SRP**: Identifica responsabilidades claras en tus clases
2. **Usa abstracciones**: Define interfaces para dependencias externas
3. **Favorece la composición sobre la herencia**: Combina objetos en lugar de extender clases
4. **Diseña para la extensibilidad**: Piensa en cómo se podrían añadir nuevas funcionalidades
5. **Prueba con ejemplos reales**: Verifica que tus abstracciones funcionen en la práctica

### Herramientas que Ayudan:

- **Inyección de Dependencias**: Frameworks que facilitan el DIP
- **Testing**: Las pruebas unitarias te ayudan a identificar violaciones de principios
- **Code Reviews**: Revisar código con colegas ayuda a identificar problemas de diseño
- **Refactorización continua**: Mejora el diseño a medida que aprendes

## Recursos Adicionales

- Libro: "Clean Architecture" de Robert C. Martin
- Libro: "Agile Principles, Patterns, and Practices in C#" de Robert C. Martin
- Artículo: "SOLID Principles Explained" en medium.com
- Curso: "SOLID Principles: Introducing Software Architecture" en Pluralsight

---

*"Los principios SOLID no son reglas absolutas, sino guías que te ayudan a escribir código más mantenible y flexible. La clave es aplicarlos con sentido común y entender cuándo pueden ser beneficiosos."*