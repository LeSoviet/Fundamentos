# Variables y Tipos de Datos

Las variables y los tipos de datos son los bloques fundamentales de cualquier lenguaje de programación. Comprender cómo funcionan es esencial para escribir código efectivo y evitar errores comunes.

## ¿Qué es una Variable?

Una variable es un nombre simbólico que representa un valor almacenado en la memoria de la computadora. Piensa en una variable como una caja etiquetada donde puedes guardar información.

### Características de las Variables:
- **Nombre (identificador)**: El nombre que usas para referirte a la variable
- **Valor**: La información almacenada en la variable
- **Tipo de datos**: La categoría de información que puede almacenar
- **Dirección de memoria**: La ubicación física donde se almacena el valor

## Tipos de Datos Primitivos

Los tipos de datos primitivos son los más básicos que proporciona un lenguaje de programación:

### Números
- **Enteros (integers)**: Números sin parte decimal (..., -2, -1, 0, 1, 2, ...)
- **Punto flotante (float/double)**: Números con parte decimal (3.14, -0.001, 2.0)

### Texto
- **Caracteres (char)**: Un solo carácter ('a', 'B', '5', '@')
- **Cadenas (strings)**: Secuencia de caracteres ("Hola", "Programación", "123")

### Booleanos
- **Booleanos (boolean)**: Valores lógicos que pueden ser verdadero (true) o falso (false)

### Valores Especiales
- **Nulo (null/nil/None)**: Representa la ausencia de valor
- **Indefinido (undefined)**: Valor no asignado aún

## Declaración y Asignación

### Declaración
Crear una variable sin darle un valor inicial:
```javascript
// Ejemplo en JavaScript
let edad;
let nombre;
```

### Asignación
Darle un valor a una variable:
```javascript
edad = 25;
nombre = "Carlos";
```

### Declaración y Asignación Simultánea
```javascript
let edad = 25;
let nombre = "Carlos";
const PI = 3.14159;
```

## Alcance (Scope) de las Variables

El alcance determina dónde en el programa una variable es accesible:

### Variables Globales
- Declaradas fuera de cualquier función
- Accesibles desde cualquier parte del programa
- Deben usarse con cuidado para evitar efectos secundarios

### Variables Locales
- Declaradas dentro de una función o bloque
- Solo accesibles dentro de ese contexto
- Se destruyen cuando termina el bloque

### Variables de Bloque
- Declaradas con `let` o `const` en JavaScript
- Solo accesibles dentro del bloque donde se declaran
- Más seguras que las variables de función

## Convenciones de Nombres

### Buenas Prácticas:
1. **Usa nombres descriptivos**: `edadUsuario` es mejor que `e`
2. **Sigue un estándar**: camelCase, snake_case, PascalCase
3. **Evita abreviaturas confusas**: `usrNm` es peor que `userName`
4. **Usa sustantivos para variables**: `contador`, `listaEstudiantes`

### Ejemplos de Convenciones:
```javascript
// camelCase (más común en JavaScript)
let firstName = "Juan";
let lastName = "Pérez";
let userAge = 30;

// snake_case (más común en Python)
let first_name = "Juan";
let last_name = "Pérez";
let user_age = 30;

// PascalCase (más común para clases)
let FirstName = "Juan";
let LastName = "Pérez";
```

## Tipos de Datos Compuestos

### Arreglos/Arrays
Colecciones ordenadas de elementos:
```javascript
let numeros = [1, 2, 3, 4, 5];
let nombres = ["Ana", "Luis", "Carlos"];
let mixto = [1, "Hola", true, 3.14];
```

### Objetos/Diccionarios
Colecciones de pares clave-valor:
```javascript
let persona = {
    nombre: "Ana",
    edad: 25,
    ciudad: "Madrid"
};
```

## Conversión de Tipos

### Conversión Implícita
El lenguaje convierte automáticamente tipos cuando es necesario:
```javascript
let resultado = "5" + 3;  // "53" (string)
let resultado2 = "5" - 3; // 2 (número)
```

### Conversión Explícita
Convertir manualmente entre tipos:
```javascript
let numero = parseInt("5");     // 5 (entero)
let decimal = parseFloat("3.14"); // 3.14 (flotante)
let texto = String(123);        // "123" (string)
let booleano = Boolean(1);      // true (booleano)
```

## Errores Comunes y Cómo Evitarlos

### 1. Usar Variables No Declaradas
```javascript
// Mal
console.log(nombre); // Error: nombre is not defined

// Bien
let nombre = "Carlos";
console.log(nombre); // "Carlos"
```

### 2. Confusión entre Null y Undefined
```javascript
let variable1 = null;      // Intencionalmente vacío
let variable2;             // No asignado (undefined)
let variable3 = undefined; // Explícitamente undefined
```

### 3. Problemas de Tipado
```javascript
// Mal
let edad = "25"; // String en lugar de número
let resultado = edad + 5; // "255" en lugar de 30

// Bien
let edad = 25; // Número
let resultado = edad + 5; // 30
```

## Buenas Prácticas

### 1. Inicializa Variables
```javascript
// Bien
let contador = 0;
let nombre = "";
let esActivo = false;
```

### 2. Usa const para Valores Constantes
```javascript
const PI = 3.14159;
const DIAS_SEMANA = 7;
```

### 3. Evita Variables Globales
```javascript
// Preferible
function calcularArea(radio) {
    const PI = 3.14159;
    return PI * radio * radio;
}
```

### 4. Usa Nombres Claros y Consistentes
```javascript
// Bien
let studentCount = 25;
let maxStudents = 30;
let isActive = true;

// Mal
let x = 25;
let y = 30;
let z = true;
```

## Ejercicios Prácticos

### Ejercicio 1: Calculadora de Edad
```javascript
// Crea variables para almacenar:
// - Año actual
// - Año de nacimiento
// - Calcula y muestra la edad
```

### Ejercicio 2: Conversor de Temperatura
```javascript
// Crea variables para:
// - Temperatura en Celsius
// - Convertir a Fahrenheit (F = C × 9/5 + 32)
// - Mostrar ambos valores
```

### Ejercicio 3: Perfil de Usuario
```javascript
// Crea un objeto con información de usuario:
// - Nombre
// - Edad
// - Correo electrónico
// - Lista de hobbies (array)
```

## Recursos Adicionales

- Documentación oficial del lenguaje que estés usando
- Libro: "You Don't Know JS" - Tipos y Gramática
- Curso: "Programming Foundations: Fundamentals" en LinkedIn Learning
- Artículo: "JavaScript Data Types and Data Structures" en MDN Web Docs

---

*"Comprender las variables y tipos de datos es como aprender el alfabeto antes de escribir una novela. Es fundamental para todo lo que vendrá después."*