# Funciones y Procedimientos

Las funciones y procedimientos son bloques de código reutilizables que realizan tareas específicas. Son fundamentales para escribir código limpio, mantenible y eficiente.

## ¿Qué es una Función?

Una función es un bloque de código con nombre que realiza una tarea específica y puede devolver un valor. Las funciones ayudan a:
- Evitar la repetición de código
- Organizar el programa en partes lógicas
- Facilitar el mantenimiento y la depuración
- Mejorar la legibilidad del código

### Componentes de una Función:
1. **Nombre**: Identificador único de la función
2. **Parámetros**: Valores de entrada que recibe la función
3. **Cuerpo**: Código que se ejecuta cuando se llama a la función
4. **Valor de retorno**: Resultado que devuelve la función (opcional)

## Declaración de Funciones

### Funciones con Valor de Retorno
```javascript
function nombreFuncion(parametro1, parametro2) {
    // Código de la función
    return valor;
}
```

#### Ejemplo:
```javascript
function sumar(a, b) {
    return a + b;
}

let resultado = sumar(5, 3); // resultado = 8
```

### Procedimientos (Funciones sin Retorno)
```javascript
function nombreProcedimiento(parametro1, parametro2) {
    // Código de la función
    // No tiene return o return vacío
}
```

#### Ejemplo:
```javascript
function mostrarMensaje(nombre) {
    console.log("Hola, " + nombre + "!");
}

mostrarMensaje("Ana"); // Imprime: Hola, Ana!
```

## Parámetros y Argumentos

### Parámetros Formales
Variables definidas en la declaración de la función:
```javascript
function saludar(nombre, edad) { // nombre y edad son parámetros
    console.log(`Hola ${nombre}, tienes ${edad} años`);
}
```

### Argumentos Reales
Valores pasados cuando se llama a la función:
```javascript
saludar("Carlos", 25); // "Carlos" y 25 son argumentos
```

### Tipos de Parámetros

#### Parámetros por Defecto
```javascript
function saludar(nombre, titulo = "Sr./Sra.") {
    console.log(`Hola ${titulo} ${nombre}`);
}

saludar("Ana"); // Hola Sr./Sra. Ana
saludar("Luis", "Dr."); // Hola Dr. Luis
```

#### Parámetros Rest
Para aceptar un número variable de argumentos:
```javascript
function sumarTodos(...numeros) {
    let suma = 0;
    for (let num of numeros) {
        suma += num;
    }
    return suma;
}

console.log(sumarTodos(1, 2, 3, 4)); // 10
```

#### Parámetros con Desestructuración
```javascript
function mostrarPersona({nombre, edad}) {
    console.log(`Nombre: ${nombre}, Edad: ${edad}`);
}

let persona = {nombre: "Ana", edad: 25};
mostrarPersona(persona); // Nombre: Ana, Edad: 25
```

## Ámbito (Scope) de las Funciones

### Ámbito Local
Variables definidas dentro de una función solo existen dentro de esa función:
```javascript
function calcular() {
    let resultado = 10; // Solo existe dentro de calcular()
    return resultado * 2;
}

// console.log(resultado); // Error: resultado is not defined
```

### Ámbito Global
Variables definidas fuera de funciones son accesibles desde cualquier lugar:
```javascript
let PI = 3.14159; // Variable global

function calcularArea(radio) {
    return PI * radio * radio; // Accede a la variable global
}
```

### Cierre (Closure)
Función que recuerda el ámbito donde fue creada:
```javascript
function crearContador() {
    let contador = 0;
    
    return function() {
        contador++;
        return contador;
    };
}

let contar = crearContador();
console.log(contar()); // 1
console.log(contar()); // 2
```

## Tipos de Funciones

### Funciones Declaradas
```javascript
function multiplicar(a, b) {
    return a * b;
}
```

### Funciones Expresadas
```javascript
let dividir = function(a, b) {
    return a / b;
};
```

### Funciones Flecha (Arrow Functions)
```javascript
let restar = (a, b) => a - b;

let saludar = nombre => `Hola, ${nombre}!`;

let calcularCuadrado = numero => {
    let resultado = numero * numero;
    return resultado;
};
```

### Funciones Anónimas
Funciones sin nombre, comúnmente usadas como callbacks:
```javascript
setTimeout(function() {
    console.log("Han pasado 2 segundos");
}, 2000);

// Con función flecha
setTimeout(() => {
    console.log("Han pasado 2 segundos");
}, 2000);
```

## Funciones de Orden Superior

Funciones que reciben otras funciones como parámetros o devuelven funciones:

### Funciones como Parámetros
```javascript
function operar(a, b, operacion) {
    return operacion(a, b);
}

let suma = (x, y) => x + y;
let multiplicacion = (x, y) => x * y;

console.log(operar(5, 3, suma)); // 8
console.log(operar(5, 3, multiplicacion)); // 15
```

### Funciones que Devuelven Funciones
```javascript
function crearMultiplicador(factor) {
    return function(numero) {
        return numero * factor;
    };
}

let duplicar = crearMultiplicador(2);
let triplicar = crearMultiplicador(3);

console.log(duplicar(5)); // 10
console.log(triplicar(5)); // 15
```

## Recursión

Función que se llama a sí misma:

### Ejemplo: Cálculo de Factorial
```javascript
function factorial(n) {
    // Caso base
    if (n <= 1) {
        return 1;
    }
    
    // Caso recursivo
    return n * factorial(n - 1);
}

console.log(factorial(5)); // 120
```

### Ejemplo: Serie de Fibonacci
```javascript
function fibonacci(n) {
    // Casos base
    if (n <= 1) {
        return n;
    }
    
    // Caso recursivo
    return fibonacci(n - 1) + fibonacci(n - 2);
}

console.log(fibonacci(6)); // 8
```

## Buenas Prácticas

### 1. Nombres Descriptivos
```javascript
// Mal
function calc(x, y) {
    return x * y;
}

// Bien
function calcularAreaRectangulo(ancho, alto) {
    return ancho * alto;
}
```

### 2. Funciones Pequeñas y Enfocadas
```javascript
// Mal - función hace demasiadas cosas
function procesarUsuario(usuario) {
    validarUsuario(usuario);
    guardarUsuario(usuario);
    enviarEmail(usuario);
    registrarActividad(usuario);
}

// Bien - funciones pequeñas y específicas
function validarUsuario(usuario) { /* solo validación */ }
function guardarUsuario(usuario) { /* solo guardado */ }
function enviarEmail(usuario) { /* solo envío de email */ }
function registrarActividad(usuario) { /* solo registro */ }
```

### 3. Evitar Efectos Secundarios
```javascript
// Mal - modifica variable global
let total = 0;

function agregar(numero) {
    total += numero; // Efecto secundario
    return total;
}

// Bien - sin efectos secundarios
function sumar(a, b) {
    return a + b; // Solo devuelve resultado
}
```

### 4. Manejo de Errores
```javascript
function dividirSeguro(dividendo, divisor) {
    if (divisor === 0) {
        throw new Error("No se puede dividir por cero");
    }
    return dividendo / divisor;
}

try {
    let resultado = dividirSeguro(10, 0);
} catch (error) {
    console.log("Error:", error.message);
}
```

## Errores Comunes y Cómo Evitarlos

### 1. No Retornar Valores Esperados
```javascript
// Mal
function calcularImpuesto(monto) {
    if (monto > 1000) {
        return monto * 0.15;
    }
    // Olvidar return para otros casos
}

// Bien
function calcularImpuesto(monto) {
    if (monto > 1000) {
        return monto * 0.15;
    }
    return monto * 0.10; // Valor por defecto
}
```

### 2. Modificar Parámetros
```javascript
// Mal
function procesarArray(arr) {
    arr.push("nuevo"); // Modifica el array original
    return arr;
}

// Bien
function procesarArray(arr) {
    let copia = [...arr]; // Crear copia
    copia.push("nuevo");
    return copia;
}
```

### 3. Profundidad de Recursión Excesiva
```javascript
// Mal - sin límite de recursión
function contarAtras(n) {
    console.log(n);
    contarAtras(n - 1); // Sin caso base
}

// Bien - con caso base
function contarAtras(n) {
    if (n <= 0) return; // Caso base
    console.log(n);
    contarAtras(n - 1);
}
```

## Ejercicios Prácticos

### Ejercicio 1: Calculadora Modular
```javascript
// Crea funciones separadas para:
// - Suma, resta, multiplicación, división
// - Una función principal que reciba operación y números
// - Manejo de errores para división por cero
```

### Ejercicio 2: Validador de Contraseñas
```javascript
// Crea funciones para:
// - Verificar longitud mínima
// - Verificar presencia de mayúsculas
// - Verificar presencia de números
// - Combinar todas las validaciones
```

### Ejercicio 3: Transformador de Texto
```javascript
// Crea funciones para:
// - Convertir a mayúsculas
// - Convertir a minúsculas
// - Capitalizar primera letra
// - Invertir cadena
// - Componer transformaciones
```

## Recursos Adicionales

- Documentación oficial del lenguaje de programación que estés usando
- Libro: "Clean Code" de Robert C. Martin (capítulo sobre funciones)
- Curso: "JavaScript Functions" en freeCodeCamp
- Artículo: "Functional Programming Principles" en MDN Web Docs

---

*"Las funciones son como herramientas en un cinturón: cuanto mejor organizadas y más especializadas sean, más eficiente será tu trabajo como programador."*