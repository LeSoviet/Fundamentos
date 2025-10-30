# Variables y Tipos de Datos

Las variables y los tipos de datos son los bloques fundamentales de cualquier lenguaje de programación. Comprender cómo funcionan es esencial para escribir código efectivo y evitar errores comunes.

## ¿Qué es una Variable?



Una variable es un nombre simbólico que representa un valor almacenado en la memoria de la computadora. Piensa en una variable como una **caja etiquetada** donde puedes guardar información.

### 🎯 Analogía para principiantes:
Imagina que tienes varias cajas en tu cuarto:
- Una caja etiquetada "edad" contiene el número 25
- Una caja etiquetada "nombre" contiene el texto "María"
- Una caja etiquetada "esEstudiante" contiene un símbolo de ✓ (verdadero)

Cuando necesitas el valor, simplemente buscas la caja por su etiqueta.

### Características de las Variables:
- **Nombre (identificador)**: La etiqueta de la caja
- **Valor**: Lo que guardas dentro de la caja
- **Tipo de datos**: Qué tipo de cosas puedes guardar en esa caja
- **Dirección de memoria**: Dónde está físicamente la caja en el almacén

### 💡 Por qué son importantes las variables:
- **Memoria**: No necesitas recordar valores, solo los nombres
- **Flexibilidad**: Puedes cambiar el contenido cuando quieras
- **Claridad**: El código se entiende mejor con nombres descriptivos

## Tipos de Datos Primitivos

Los tipos de datos primitivos son los **bloques de construcción básicos** que proporciona un lenguaje de programación. Son como los diferentes tipos de LEGO que puedes usar.

### 🔢 Números
#### Enteros (integers)
Números sin parte decimal:
```javascript
let edad = 25;           // Edad de una persona
let cantidadProductos = 10; // Cuántos productos hay
let año = 2024;          // Año actual
let temperatura = -5;    // Puede ser negativo
```

**¿Cuándo usarlos?**
- Contar cosas (personas, productos, días)
- Edades, calificaciones, cantidades
- Índices de arrays

#### Punto flotante (float/double)
Números con parte decimal:
```javascript
let precio = 19.99;      // Precio de un producto
let altura = 1.75;       // Altura de una persona
let pi = 3.14159;        // Constante matemática
let temperatura = 36.5;  // Temperatura corporal
```

**¿Cuándo usarlos?**
- Mediciones, precios, porcentajes
- Cálculos científicos o financieros
- Cualquier cosa que necesite precisión decimal

### 📝 Texto
#### Caracteres (char)
Un solo carácter:
```javascript
let inicial = 'A';       // Primera letra de un nombre
let genero = 'M';        // Género (M/F)
let calificacion = 'A';  // Calificación en letra
```

#### Cadenas (strings)
Secuencia de caracteres:
```javascript
let nombre = "Ana García";     // Nombre completo
let direccion = "Calle 123 #45"; // Dirección
let email = "ana@email.com";    // Correo electrónico
let mensaje = "¡Hola mundo!";   // Mensaje de texto
```

**💡 Operaciones comunes con strings:**
```javascript
let nombre = "Carlos";
let apellido = "Rodríguez";

// Concatenar (unir)
let nombreCompleto = nombre + " " + apellido;
// "Carlos Rodríguez"

// Longitud
let longitud = nombre.length; // 6

// Convertir a mayúsculas
let mayusculas = nombre.toUpperCase(); // "CARLOS"

// Extraer parte del texto
let primerLetra = nombre[0]; // "C"
```

### ✅ Booleanos
Valores lógicos que pueden ser verdadero (true) o falso (false):
```javascript
let esMayorDeEdad = true;     // Tiene 18+ años
let tieneLicencia = false;    // No tiene licencia
let esEstudiante = true;      // Es estudiante
let estaActivo = false;       // Cuenta inactiva
```

**¿Cuándo usarlos?**
- Estados (activo/inactivo, abierto/cerrado)
- Permisos (tiene/no tiene acceso)
- Resultados de comparaciones

### 🔧 Valores Especiales
#### Nulo (null/nil/None)
Representa la **ausencia intencional** de valor:
```javascript
let resultado = null;         // La búsqueda no encontró nada
let telefono = null;          // El usuario no proporcionó teléfono
let fechaCancelacion = null;  // No se ha cancelado aún
```

#### Indefinido (undefined)
Valor **no asignado** aún:
```javascript
let variableSinValor;         // undefined (declarada pero no asignada)
let objeto = {nombre: "Ana"};
let edad = objeto.edad;        // undefined (la propiedad no existe)
```

**🤔 Diferencia clave:**
- `null` = "Esta vacío intencionalmente"
- `undefined` = "No sé qué hay aquí aún"

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

## 📚 Ejercicios Prácticos Paso a Paso

### Ejercicio 1: Calculadora de Edad (Guía completa)
**Objetivo**: Crear un programa que calcule tu edad actual.

**Paso 1: Declarar variables necesarias**
```javascript
// Variables que necesitamos
let añoActual = 2024;
let añoNacimiento = 1995;
let edadCalculada;
```

**Paso 2: Realizar el cálculo**
```javascript
// Fórmula: edad = año actual - año de nacimiento
edadCalculada = añoActual - añoNacimiento;
```

**Paso 3: Mostrar el resultado**
```javascript
console.log("Tu edad es: " + edadCalculada + " años");
// Output: Tu edad es: 29 años
```

**💡 Desafío extra**: ¿Cómo harías que funcione con cualquier año actual?
```javascript
// Usando el objeto Date para obtener el año actual
let fechaActual = new Date();
let añoActual = fechaActual.getFullYear();
```

### Ejercicio 2: Conversor de Temperatura (Con validación)
**Objetivo**: Convertir Celsius a Fahrenheit con manejo de errores.

**Paso 1: Variables y constantes**
```javascript
let temperaturaCelsius = 25;  // Valor de entrada
const FORMULA_FAHRENHEIT = 9/5;  // Constante para la fórmula
let temperaturaFahrenheit;   // Resultado
let mensajeError = "";       // Para posibles errores
```

**Paso 2: Validación de entrada**
```javascript
if (typeof temperaturaCelsius !== 'number') {
    mensajeError = "Error: La temperatura debe ser un número";
} else if (temperaturaCelsius < -273.15) {
    mensajeError = "Error: Temperatura por debajo del cero absoluto";
}
```

**Paso 3: Cálculo y resultado**
```javascript
if (mensajeError === "") {
    // Fórmula: F = C × 9/5 + 32
    temperaturaFahrenheit = temperaturaCelsius * FORMULA_FAHRENHEIT + 32;
    console.log(`${temperaturaCelsius}°C = ${temperaturaFahrenheit}°F`);
} else {
    console.log(mensajeError);
}
```

### Ejercicio 3: Perfil de Usuario Completo
**Objetivo**: Crear un objeto usuario con diferentes tipos de datos.

**Paso 1: Estructura básica**
```javascript
let usuario = {
    // Datos personales (strings y números)
    nombre: "María González",
    edad: 28,
    altura: 1.65,
    
    // Contacto (strings)
    email: "maria@email.com",
    telefono: null,  // No proporcionó teléfono
    
    // Estado (booleanos)
    esEstudiante: true,
    tieneLicencia: false,
    cuentaActiva: true,
    
    // Preferencias (array y objeto)
    hobbies: ["leer", "nadar", "programar"],
    preferencias: {
        tema: "oscuro",
        idioma: "español",
        notificaciones: true
    }
};
```

**Paso 2: Acceder a diferentes tipos de datos**
```javascript
// Acceder a strings
console.log("Nombre: " + usuario.nombre);
console.log("Email: " + usuario.email);

// Acceder a números
console.log("Edad: " + usuario.edad + " años");
console.log("Altura: " + usuario.altura + " metros");

// Acceder a booleanos
if (usuario.esEstudiante) {
    console.log("📚 María es estudiante");
}

// Acceder a arrays
console.log("Hobbies:");
for (let hobby of usuario.hobbies) {
    console.log("- " + hobby);
}

// Acceder a objetos anidados
console.log("Idioma preferido: " + usuario.preferencias.idioma);
```

**Paso 3: Modificar datos**
```javascript
// Cambiar valores
usuario.edad = 29;  // Cumplió años
usuario.telefono = "555-1234";  // Ahora proporcionó teléfono
usuario.hobbies.push("viajar");  // Añadir nuevo hobby

console.log("Usuario actualizado:", usuario);
```

## 🎯 Mini-Proyecto: Sistema de Calificaciones

**Objetivo**: Crear un sistema que gestione calificaciones de estudiantes.

```javascript
// Variables del sistema
let nombreEstudiante = "Carlos Rodríguez";
let calificaciones = [85, 92, 78, 95, 88];  // Array de números
let asignaturas = ["Matemáticas", "Historia", "Ciencias", "Literatura", "Arte"];
let aprobado = true;  // Booleano
let mensajeFinal = "";  // String para el resultado

// Cálculos
let sumaCalificaciones = 0;
for (let calificacion of calificaciones) {
    sumaCalificaciones += calificacion;
}

let promedio = sumaCalificaciones / calificaciones.length;
aprobado = promedio >= 70;  // Se aprueba con 70 o más

// Mensaje final
if (aprobado) {
    mensajeFinal = `✅ ${nombreEstudiante} ha aprobado con ${promedio.toFixed(2)}`;
} else {
    mensajeFinal = `❌ ${nombreEstudiante} necesita mejorar. Promedio: ${promedio.toFixed(2)}`;
}

console.log(mensajeFinal);

// Reporte detallado
console.log("\n📊 Reporte de Calificaciones:");
for (let i = 0; i < asignaturas.length; i++) {
    console.log(`${asignaturas[i]}: ${calificaciones[i]}`);
}
```

## 🔍 Tips para Principiantes

### 1. **Nombra variables pensando en el futuro**
```javascript
// Mal (confuso en 6 meses)
let x = 25;
let y = "Carlos";
let z = true;

// Bien (claro siempre)
let edadUsuario = 25;
let nombreUsuario = "Carlos";
let usuarioActivo = true;
```

### 2. **Inicializa siempre tus variables**
```javascript
// Riesgoso (puede causar errores)
let contador;
if (condicion) {
    contador = 0;
}
console.log(contador * 2);  // Error si condición es false

// Seguro
let contador = 0;  // Valor inicial
if (condicion) {
    contador = 10;
}
console.log(contador * 2);  // Siempre funciona
```

### 3. **Usa el tipo de dato correcto**
```javascript
// Error común
let precio = "19.99";  // String en lugar de número
let total = precio + 5;  // "19.995" en lugar de 24.99

// Correcto
let precio = 19.99;  // Número
let total = precio + 5;  // 24.99 ✅
```

### 4. **Aprovecha las constantes**
```javascript
// Para valores que no cambian
const PI = 3.14159;
const MESES_AÑO = 12;
const DIAS_SEMANA = 7;
const IVA_GENERAL = 0.16;

// Esto evita errores y hace el código más claro
```

## 🚀 Próximos Pasos

Una vez que domines las variables y tipos de datos:
1. **Practica con estructuras de control** (if, for, while)
2. **Aprende a crear funciones** para reutilizar código
3. **Explora estructuras de datos más complejas** (mapas, sets)
4. **Intenta resolver problemas pequeños** usando todo lo aprendido

**Recuerda**: Las variables son el fundamento de todo en programación. ¡Dominarlas te abrirá las puertas a todo lo demás!

## Recursos Adicionales

- Documentación oficial del lenguaje que estés usando
- Libro: "You Don't Know JS" - Tipos y Gramática
- Curso: "Programming Foundations: Fundamentals" en LinkedIn Learning
- Artículo: "JavaScript Data Types and Data Structures" en MDN Web Docs

---

*"Comprender las variables y tipos de datos es como aprender el alfabeto antes de escribir una novela. Es fundamental para todo lo que vendrá después."*