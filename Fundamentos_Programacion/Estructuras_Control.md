# Estructuras de Control

Las estructuras de control son bloques de programación que permiten controlar el flujo de ejecución de un programa. Son fundamentales para tomar decisiones, repetir acciones y controlar cómo se ejecuta el código.

## Condicionales

Las estructuras condicionales permiten ejecutar diferentes bloques de código basados en condiciones lógicas.

### If/Else
La estructura más básica de control de flujo:

```javascript
if (condicion) {
    // Código si la condición es verdadera
} else {
    // Código si la condición es falsa
}
```

#### Ejemplo:
```javascript
let edad = 18;

if (edad >= 18) {
    console.log("Eres mayor de edad");
} else {
    console.log("Eres menor de edad");
}
```

### If/Else If/Else
Para múltiples condiciones:

```javascript
if (condicion1) {
    // Código si condicion1 es verdadera
} else if (condicion2) {
    // Código si condicion2 es verdadera
} else {
    // Código si ninguna condición es verdadera
}
```

#### Ejemplo:
```javascript
let calificacion = 85;

if (calificacion >= 90) {
    console.log("A");
} else if (calificacion >= 80) {
    console.log("B");
} else if (calificacion >= 70) {
    console.log("C");
} else {
    console.log("F");
}
```

### Operador Ternario
Una forma concisa de if/else para asignaciones simples:

```javascript
let resultado = condicion ? valorSiVerdadero : valorSiFalso;
```

#### Ejemplo:
```javascript
let edad = 20;
let mensaje = edad >= 18 ? "Mayor de edad" : "Menor de edad";
console.log(mensaje);
```

### Switch/Case
Para múltiples condiciones basadas en el valor de una expresión:

```javascript
switch (expresion) {
    case valor1:
        // Código si expresion === valor1
        break;
    case valor2:
        // Código si expresion === valor2
        break;
    default:
        // Código si ningún caso coincide
}
```

#### Ejemplo:
```javascript
let diaSemana = 3;

switch (diaSemana) {
    case 1:
        console.log("Lunes");
        break;
    case 2:
        console.log("Martes");
        break;
    case 3:
        console.log("Miércoles");
        break;
    case 4:
        console.log("Jueves");
        break;
    case 5:
        console.log("Viernes");
        break;
    default:
        console.log("Fin de semana");
}
```

## Bucles (Loops)

Los bucles permiten repetir bloques de código múltiples veces.

### For Loop
Ideal cuando conoces el número de iteraciones:

```javascript
for (inicialización; condición; incremento) {
    // Código a repetir
}
```

#### Ejemplo:
```javascript
// Imprimir números del 1 al 5
for (let i = 1; i <= 5; i++) {
    console.log(i);
}
```

### While Loop
Repite mientras una condición sea verdadera:

```javascript
while (condicion) {
    // Código a repetir
}
```

#### Ejemplo:
```javascript
let contador = 1;

while (contador <= 5) {
    console.log(contador);
    contador++;
}
```

### Do-While Loop
Similar a while, pero garantiza al menos una ejecución:

```javascript
do {
    // Código a repetir
} while (condicion);
```

#### Ejemplo:
```javascript
let numero;

do {
    numero = Math.floor(Math.random() * 10) + 1;
    console.log(numero);
} while (numero !== 7);
```

### For...of Loop
Para iterar sobre elementos de colecciones (arrays, strings):

```javascript
for (elemento of coleccion) {
    // Código para cada elemento
}
```

#### Ejemplo:
```javascript
let frutas = ["manzana", "banana", "naranja"];

for (let fruta of frutas) {
    console.log(fruta);
}
```

### For...in Loop
Para iterar sobre propiedades de objetos:

```javascript
for (propiedad in objeto) {
    // Código para cada propiedad
}
```

#### Ejemplo:
```javascript
let persona = {
    nombre: "Ana",
    edad: 25,
    ciudad: "Madrid"
};

for (let propiedad in persona) {
    console.log(propiedad + ": " + persona[propiedad]);
}
```

## Control de Flujo Avanzado

### Break
Termina la ejecución de un bucle o switch:

```javascript
for (let i = 1; i <= 10; i++) {
    if (i === 5) {
        break; // Sale del bucle cuando i es 5
    }
    console.log(i);
}
// Imprime: 1, 2, 3, 4
```

### Continue
Salta a la siguiente iteración del bucle:

```javascript
for (let i = 1; i <= 10; i++) {
    if (i % 2 === 0) {
        continue; // Salta los números pares
    }
    console.log(i);
}
// Imprime: 1, 3, 5, 7, 9
```

### Etiquetas (Labels)
Para controlar bucles anidados:

```javascript
externo: for (let i = 1; i <= 3; i++) {
    for (let j = 1; j <= 3; j++) {
        if (i === 2 && j === 2) {
            break externo; // Sale del bucle externo
        }
        console.log(`i: ${i}, j: ${j}`);
    }
}
```

## Patrones Comunes de Uso

### Validación de Entrada
```javascript
let edad;

do {
    edad = prompt("Ingresa tu edad:");
    edad = parseInt(edad);
} while (isNaN(edad) || edad < 0 || edad > 120);

console.log("Edad válida: " + edad);
```

### Búsqueda en Arrays
```javascript
let numeros = [3, 7, 1, 9, 4];
let buscar = 9;
let encontrado = false;

for (let i = 0; i < numeros.length; i++) {
    if (numeros[i] === buscar) {
        encontrado = true;
        break;
    }
}

console.log(encontrado ? "Encontrado" : "No encontrado");
```

### Filtrado de Datos
```javascript
let edades = [15, 22, 17, 30, 12, 25];
let mayoresEdad = [];

for (let edad of edades) {
    if (edad >= 18) {
        mayoresEdad.push(edad);
    }
}

console.log(mayoresEdad); // [22, 30, 25]
```

## Buenas Prácticas

### 1. Mantén las Condiciones Simples
```javascript
// Mal
if (edad >= 18 && edad <= 65 && tieneLicencia && !estaSuspendido) {
    // Código
}

// Bien
let esEdadValida = edad >= 18 && edad <= 65;
let puedeConducir = tieneLicencia && !estaSuspendido;

if (esEdadValida && puedeConducir) {
    // Código
}
```

### 2. Evita Condiciones Negativas Complejas
```javascript
// Mal
if (!(edad < 18 || !tienePermiso)) {
    // Código
}

// Bien
if (edad >= 18 && tienePermiso) {
    // Código
}
```

### 3. Usa Switch para Múltiples Condiciones
```javascript
// Mal
if (rol === "admin") {
    // Código para admin
} else if (rol === "editor") {
    // Código para editor
} else if (rol === "lector") {
    // Código para lector
} else {
    // Código por defecto
}

// Bien
switch (rol) {
    case "admin":
        // Código para admin
        break;
    case "editor":
        // Código para editor
        break;
    case "lector":
        // Código para lector
        break;
    default:
        // Código por defecto
}
```

### 4. Evita Bucles Anidados Profundos
```javascript
// Considera refactorizar si tienes más de 2-3 niveles de anidamiento
// Usa funciones auxiliares para simplificar
```

## Errores Comunes y Cómo Evitarlos

### 1. Bucle Infinito
```javascript
// Mal
let i = 0;
while (i < 10) {
    console.log(i);
    // Olvidar incrementar i
}

// Bien
let i = 0;
while (i < 10) {
    console.log(i);
    i++; // No olvidar incrementar
}
```

### 2. Comparación de Tipos
```javascript
// Mal
if (edad == "18") { // Comparación débil
    // Código
}

// Bien
if (edad === 18) { // Comparación estricta
    // Código
}
```

### 3. Olvidar Break en Switch
```javascript
// Mal
switch (opcion) {
    case 1:
        console.log("Opción 1");
    case 2: // Se ejecutará también
        console.log("Opción 2");
        break;
}

// Bien
switch (opcion) {
    case 1:
        console.log("Opción 1");
        break;
    case 2:
        console.log("Opción 2");
        break;
}
```

## Ejercicios Prácticos

### Ejercicio 1: Calculadora Simple
```javascript
// Crea una calculadora que:
// - Pida dos números
// - Pida una operación (+, -, *, /)
// - Use switch para realizar la operación
// - Maneje división por cero
```

### Ejercicio 2: FizzBuzz
```javascript
// Imprime números del 1 al 100
// - Si es múltiplo de 3, imprime "Fizz"
// - Si es múltiplo de 5, imprime "Buzz"
// - Si es múltiplo de ambos, imprime "FizzBuzz"
// - Si no, imprime el número
```

### Ejercicio 3: Validador de Contraseña
```javascript
// Crea un validador que verifique:
// - Longitud mínima de 8 caracteres
// - Al menos una mayúscula
// - Al menos un número
// - Al menos un carácter especial
// Usa bucles y condicionales
```

## Recursos Adicionales

- Documentación oficial del lenguaje de programación que estés usando
- Libro: "Clean Code" de Robert C. Martin (capítulo sobre estructuras de control)
- Curso: "Programming Foundations: Fundamentals" en LinkedIn Learning
- Tutorial: "JavaScript Loops and Conditionals" en freeCodeCamp

---

*"Las estructuras de control son como las señales de tráfico del código: te guían por el camino correcto y evitan accidentes en la ejecución de tu programa."*