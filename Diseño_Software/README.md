# Diseño de Software

El diseño de software es el proceso de **planificar y estructurar** una aplicación antes de escribir el código. Piensa en ello como los **planos arquitectónicos** para construir una casa: sin buenos planos, la casa será débil, difícil de mantener, y costosa de reparar.

## 📚 Contenido de esta Sección

1. [Principios SOLID](./SOLID_Principles.md) - Cinco principios fundamentales de diseño orientado a objetos
2. [Patrones de Diseño](./Patrones_Diseno.md) - Soluciones reutilizables a problemas comunes
3. [Arquitectura de Software](./Arquitectura_Software.md) - Estructuración a gran escala de aplicaciones

## 🏗️ ¿Por Qué es Importante el Diseño de Software?

### 🎯 Analogía: Construir una Casa
Imagina que quieres construir una casa:

**❌ Sin diseño (solo empezar a construir):**
- Pones las paredes donde te parece
- No planeas dónde irán los baños
- La electricidad queda en lugares extraños
- Si quieres añadir una habitación, tienes que demoler paredes
- La casa es ineficiente, fea y peligrosa

**✅ Con buen diseño (planos arquitectónicos):**
- Sabes exactamente dónde irá cada habitación
- La electricidad y plomería están bien planeadas
- Es fácil añadir habitaciones más tarde
- La casa es segura, eficiente y bonita
- El mantenimiento es sencillo

### 💡 Beneficios Reales en Programación:
1. **Ahorro de tiempo**: Menos tiempo corrigiendo errores
2. **Código más limpio**: Más fácil de leer y entender
3. **Facilidad para cambios**: Añadir nuevas funcionalidades sin romper lo existente
4. **Trabajo en equipo**: Varios desarrolladores pueden trabajar juntos sin chocar
5. **Menos estrés**: Sabes qué hacer y cómo hacerlo

## 🎓 Conceptos Fundamentales para Principiantes

### 🧩 Modularidad: Divide y Vencerás
**¿Qué es?** Dividir un problema grande en piezas pequeñas y manejables.

**Analogía:** En lugar de intentar construir una casa entera de una vez, construyes:
- Los cimientos primero
- Luego las paredes
- Después el techo
- Finalmente la decoración

Cada pieza es independiente pero trabaja con las demás.

**En código:**
```javascript
// Mal: Todo junto en una función gigante
function procesarPedidoCompleto(pedido) {
    // Validar datos (50 líneas)
    // Calcular precio (30 líneas)
    // Guardar en base de datos (40 líneas)
    // Enviar email (25 líneas)
    // Actualizar inventario (35 líneas)
    // Total: 180 líneas en una función
}

// Bien: Dividido en módulos pequeños
function validarPedido(pedido) { /* 20 líneas */ }
function calcularPrecio(pedido) { /* 15 líneas */ }
function guardarPedido(pedido) { /* 20 líneas */ }
function enviarConfirmacion(pedido) { /* 10 líneas */ }
function actualizarInventario(pedido) { /* 15 líneas */ }

function procesarPedidoCompleto(pedido) {
    validarPedido(pedido);
    let precio = calcularPrecio(pedido);
    guardarPedido(pedido);
    enviarConfirmacion(pedido);
    actualizarInventario(pedido);
}
```

### 🔌 Acoplamiento: Qué Tan Conectados Están los Componentes
**¿Qué es?** Mide cuánto dependen unas piezas de otras.

**Analogía:**
- **Alto acoplamiento**: Como si tu teléfono, televisor y nevera dejaran de funcionar si se va la luz (todo depende de una sola cosa)
- **Bajo acoplamiento**: Como si cada aparato funcionara independientemente con su propia batería

**En código:**
```javascript
// Alto acoplamiento (mal)
class Usuario {
    constructor() {
        this.baseDeDatos = new MySQLDatabase("localhost"); // Dependencia directa
    }
    
    guardar() {
        this.baseDeDatos.insert(this); // Solo funciona con MySQL
    }
}

// Bajo acoplamiento (bien)
class Usuario {
    constructor(repositorio) { // Inyección de dependencia
        this.repositorio = repositorio;
    }
    
    guardar() {
        this.repositorio.guardar(this); // Funciona con cualquier repositorio
    }
}

// Puede usar MySQL, PostgreSQL, MongoDB, etc.
let usuarioMySQL = new Usuario(new MySQLRepositorio());
let usuarioMongo = new Usuario(new MongoRepositorio());
```

### 🎯 Cohesión: Qué Tan Enfocada Está una Pieza
**¿Qué es?** Mide cuán relacionadas están las partes dentro de un mismo componente.

**Analogía:**
- **Alta cohesión**: Una caja de herramientas donde cada herramienta tiene un propósito específico
- **Baja cohesión**: Una caja donde mezclas herramientas de cocina, jardinería y mecánica

**En código:**
```javascript
// Baja cohesión (mal)
class SistemaUsuarios {
    // Métodos para usuarios
    crearUsuario() { }
    eliminarUsuario() { }
    
    // Métodos para email (no relacionado)
    enviarEmail() { }
    validarEmail() { }
    
    // Métodos para reportes (no relacionado)
    generarReporteVentas() { }
    exportarPDF() { }
}

// Alta cohesión (bien)
class UsuarioService {
    // Solo métodos relacionados con usuarios
    crearUsuario() { }
    eliminarUsuario() { }
    actualizarUsuario() { }
    buscarUsuario() { }
}

class EmailService {
    // Solo métodos relacionados con email
    enviarEmail() { }
    validarEmail() { }
}

class ReporteService {
    // Solo métodos relacionados con reportes
    generarReporteVentas() { }
    exportarPDF() { }
}
```

### 📋 Abstracción: Ocultar Detalles Complejos
**¿Qué es?** Mostrar solo lo necesario y esconder los detalles complicados.

**Analogía:** Cuando conduces un coche:
- Solo necesitas saber usar el volante, pedales y cambios
- No necesitas saber cómo funciona el motor internamente
- El coche **abstrae** la complejidad del motor

**En código:**
```javascript
// Sin abstracción (complejo para el usuario)
let conexion = new DatabaseConnection();
conexion.connect("localhost", "user", "pass");
let resultado = conexion.query("SELECT * FROM usuarios WHERE id = ?", [1]);
conexion.close();

// Con abstracción (simple para el usuario)
class UsuarioRepositorio {
    constructor() {
        // Detalles de conexión ocultos
        this.db = new DatabaseConnection();
    }
    
    buscarPorId(id) {
        // Lógica compleja oculta
        return this.db.query("SELECT * FROM usuarios WHERE id = ?", [id]);
    }
}

// El usuario solo necesita esto:
let repo = new UsuarioRepositorio();
let usuario = repo.buscarPorId(1); // Simple y claro
```

## 🏗️ Principios Fundamentales del Diseño de Software

### SOLID Principles
Conjunto de cinco principios de diseño orientados a objetos:

1. **Single Responsibility Principle (SRP)**
   - Una clase debe tener una sola razón para cambiar
   - Cada clase debe tener una única responsabilidad

2. **Open/Closed Principle (OCP)**
   - Las entidades de software deben estar abiertas para extensión pero cerradas para modificación
   - Extiende funcionalidades sin modificar código existente

3. **Liskov Substitution Principle (LSP)**
   - Los objetos de una superclase deben poder ser reemplazados por objetos de una subclase sin afectar la corrección del programa

4. **Interface Segregation Principle (ISP)**
   - Muchas interfaces específicas son mejores que una interfaz general
   - Evita interfaces sobrecargadas

5. **Dependency Inversion Principle (DIP)**
   - Depende de abstracciones, no de implementaciones concretas
   - Módulos de alto nivel no deben depender de módulos de bajo nivel

### DRY (Don't Repeat Yourself)
Evita la duplicación de lógica, conocimiento o información:
- Reutiliza código mediante funciones, clases y módulos
- Centraliza configuraciones y constantes

### KISS (Keep It Simple, Stupid)
Mantén las cosas simples:
- Evita complejidad innecesaria
- Prefiere soluciones simples y directas

### YAGNI (You Aren't Gonna Need It)
No implementes funcionalidades hasta que sean necesarias:
- Evita sobreingeniería
- Implementa solo lo que se necesita ahora

## 📐 Patrones de Diseño

### Patrones Creacionales
Manejan la creación de objetos:

- **Singleton**: Garantiza una única instancia de una clase
- **Factory Method**: Define una interfaz para crear objetos
- **Abstract Factory**: Crea familias de objetos relacionados
- **Builder**: Construye objetos complejos paso a paso
- **Prototype**: Crea objetos copiando prototipos existentes

### Patrones Estructurales
Organizan las relaciones entre entidades:

- **Adapter**: Permite que interfaces incompatibles trabajen juntas
- **Bridge**: Separa abstracción de implementación
- **Composite**: Compone objetos en estructuras de árbol
- **Decorator**: Añade funcionalidades a objetos dinámicamente
- **Facade**: Proporciona una interfaz simplificada a un subsistema complejo

### Patrones de Comportamiento
Gestionan algoritmos y responsabilidades entre objetos:

- **Observer**: Define dependencias uno-a-muchos entre objetos
- **Strategy**: Define una familia de algoritmos intercambiables
- **Command**: Encapsula una solicitud como un objeto
- **State**: Permite que un objeto altere su comportamiento cuando cambia su estado
- **Template Method**: Define el esqueleto de un algoritmo en una operación

## 🗺️ Arquitectura de Software

### Arquitecturas Populares

#### Arquitectura en Capas (Layered Architecture)
Separa la aplicación en capas lógicas:
- Presentación
- Lógica de negocio
- Acceso a datos

#### Arquitectura Hexagonal (Ports and Adapters)
Separa el núcleo de la aplicación de los mecanismos externos:
- Puerto: interfaz definida por el núcleo
- Adaptador: implementación que conecta el puerto con mecanismos externos

#### Arquitectura Limpia (Clean Architecture)
Jerarquía de dependencias que apunta hacia el centro:
- Entidades
- Casos de uso
- Adaptadores de interfaz
- Frameworks y drivers

#### Microservicios
Arquitectura distribuida donde la aplicación se divide en servicios pequeños e independientes:
- Alta cohesión
- Bajo acoplamiento
- Escalabilidad independiente

## 🧱 Componentes y Modularidad

### Cohesión y Acoplamiento
- **Alta cohesión**: Elementos dentro de un módulo están estrechamente relacionados
- **Bajo acoplamiento**: Módulos tienen pocas dependencias entre sí

### Separación de Preocupencias
Divide un programa en secciones distintas donde cada sección aborda una preocupación separada:
- Interfaz de usuario
- Lógica de negocio
- Acceso a datos

### Inversión de Control (IoC)
Transfiere el control de objetos o porciones de un programa a un contenedor o framework:
- Inyección de dependencias
- Contenedores de inversión de control

## 🛠️ Herramientas de Diseño

### Diagramas UML
Lenguaje estándar para visualizar el diseño de sistemas:
- Diagramas de clases
- Diagramas de secuencia
- Diagramas de componentes
- Diagramas de despliegue

### Prototipado
Creación de versiones preliminares para probar conceptos:
- Prototipos de baja fidelidad
- Prototipos de alta fidelidad

### Modelado de Dominio
Representación visual del espacio del problema:
- Diagramas de entidad-relación
- Mapas de contexto

## 📈 Cómo Mejorar tus Habilidades de Diseño

1. **Estudia ejemplos de buen diseño**
   - Analiza código de proyectos exitosos
   - Lee libros sobre arquitectura de software

2. **Practica el diseño antes de codificar**
   - Dibuja diagramas antes de escribir código
   - Usa papel y lápiz para bosquejar ideas

3. **Participa en revisiones de diseño**
   - Recibe retroalimentación de colegas
   - Aprende de diferentes perspectivas

4. **Refactoriza continuamente**
   - Mejora el diseño a medida que aprendes
   - Elimina deuda técnica

5. **Aprende de errores**
   - Analiza diseños fallidos
   - Entiende qué salió mal y por qué

## 🎯 Ejercicios Prácticos para Principiantes

### Ejercicio 1: Diseñar un Sistema de Gestión de Tareas
**Objetivo**: Aplicar modularidad y cohesión para crear un sistema simple.

**📋 Requisitos:**
- Crear tareas (título, descripción, fecha límite)
- Marcar tareas como completadas
- Listar tareas pendientes
- Eliminar tareas

**🏗️ Paso 1: Identificar los componentes**
Piensa en las diferentes "cajas" que necesitas:
```javascript
// Componente 1: Manejar los datos de las tareas
class Tarea {
    constructor(titulo, descripcion, fechaLimite) {
        this.titulo = titulo;
        this.descripcion = descripcion;
        this.fechaLimite = fechaLimite;
        this.completada = false;
        this.fechaCreacion = new Date();
    }
    
    marcarComoCompletada() {
        this.completada = true;
        this.fechaCompletado = new Date();
    }
}

// Componente 2: Gestionar la lista de tareas
class GestorTareas {
    constructor() {
        this.tareas = []; // Array para guardar todas las tareas
    }
    
    agregarTarea(tarea) {
        this.tareas.push(tarea);
    }
    
    obtenerTareasPendientes() {
        return this.tareas.filter(tarea => !tarea.completada);
    }
    
    eliminarTarea(id) {
        this.tareas = this.tareas.filter(tarea => tarea.id !== id);
    }
}

// Componente 3: Interfaz de usuario (consola para simplificar)
class TareaUI {
    constructor(gestorTareas) {
        this.gestor = gestorTareas;
    }
    
    mostrarMenu() {
        console.log("=== Sistema de Tareas ===");
        console.log("1. Crear tarea");
        console.log("2. Ver tareas pendientes");
        console.log("3. Completar tarea");
        console.log("4. Salir");
    }
    
    crearTarea() {
        let titulo = prompt("Título de la tarea:");
        let descripcion = prompt("Descripción:");
        let fechaLimite = prompt("Fecha límite (YYYY-MM-DD):");
        
        let tarea = new Tarea(titulo, descripcion, fechaLimite);
        this.gestor.agregarTarea(tarea);
        console.log("✅ Tarea creada exitosamente");
    }
}

// Componente 4: Programa principal
class App {
    constructor() {
        this.gestor = new GestorTareas();
        this.ui = new TareaUI(this.gestor);
    }
    
    iniciar() {
        console.log("🚀 Iniciando Sistema de Tareas...");
        // Lógica principal de la aplicación
    }
}

// Punto de entrada
let app = new App();
app.iniciar();
```

**🤔 Preguntas para reflexionar:**
1. ¿Por qué separamos `Tarea`, `GestorTareas`, `TareaUI` y `App`?
2. ¿Qué pasaría si quisiéramos cambiar la interfaz de consola a web?
3. ¿Cómo haríamos para guardar las tareas en un archivo en lugar de memoria?

### Ejercicio 2: Refactorizar Código Mal Diseñado
**Objetivo**: Identificar problemas de diseño y aplicar principios SOLID.

**❌ Código con problemas:**
```javascript
class ProcesadorPedidos {
    procesarPedido(pedido) {
        // Validación (responsabilidad 1)
        if (!pedido.email || !pedido.productos) {
            console.log("Pedido inválido");
            return false;
        }
        
        // Cálculo de precio (responsabilidad 2)
        let total = 0;
        for (let producto of pedido.productos) {
            total += producto.precio * producto.cantidad;
        }
        
        // Guardar en base de datos (responsabilidad 3)
        // Simulación de guardado
        console.log("Guardando pedido en BD...");
        
        // Enviar email (responsabilidad 4)
        console.log("Enviando email a: " + pedido.email);
        
        // Actualizar inventario (responsabilidad 5)
        console.log("Actualizando inventario...");
        
        return true;
    }
}
```

**✅ Tu misión**: Refactoriza este código aplicando:
1. **Single Responsibility**: Divide la clase en clases más pequeñas
2. **Open/Closed**: Haz que sea fácil añadir nuevos tipos de validación
3. **Dependency Inversion**: Inyecta dependencias en lugar de crearlas

**💡 Pista**: Crea clases como:
- `ValidadorPedidos`
- `CalculadoraPrecios`
- `PedidoRepositorio`
- `EmailService`
- `InventarioService`

### Ejercicio 3: Diseñar un Sistema Simple con Patrones
**Objetivo**: Aplicar patrones de diseño básicos.

**📋 Scenario**: Necesitas crear un sistema que genere diferentes tipos de reportes:
- Reporte PDF
- Reporte Excel  
- Reporte HTML

**🏗️ Aplica estos patrones:**

1. **Factory Method**: Para crear los diferentes reportes
2. **Strategy**: Para diferentes formatos de exportación
3. **Template Method**: Para la estructura base de generación

```javascript
// Paso 1: Interfaz base
class ReporteGenerator {
    generar(datos) {
        this.prepararDatos(datos);
        this.crearContenido();
        this.exportar();
    }
    
    prepararDatos(datos) {
        console.log("Preparando datos...");
        this.datos = datos;
    }
    
    // Métodos abstractos que cada tipo implementará
    crearContenido() {
        throw new Error("Debe implementar crearContenido");
    }
    
    exportar() {
        throw new Error("Debe implementar exportar");
    }
}

// Paso 2: Implementaciones concretas
class PDFReporte extends ReporteGenerator {
    crearContenido() {
        console.log("Creando contenido PDF...");
    }
    
    exportar() {
        console.log("Exportando a PDF...");
    }
}

// Paso 3: Factory para crear reportes
class ReporteFactory {
    static crear(tipo) {
        switch(tipo) {
            case 'pdf':
                return new PDFReporte();
            case 'excel':
                return new ExcelReporte();
            case 'html':
                return new HTMLReporte();
            default:
                throw new Error("Tipo de reporte no soportado");
        }
    }
}

// Uso
let reportePDF = ReporteFactory.crear('pdf');
reportePDF.generar({titulo: "Ventas", datos: [1,2,3]});
```

## 🚀 Guía de Aprendizaje para Principiantes

### 📅 Semana 1-2: Fundamentos
- **Día 1-2**: Entiende modularidad (ejercicios de dividir funciones grandes)
- **Día 3-4**: Practica cohesión y acoplamiento
- **Día 5-7**: Aprende abstracción con ejemplos simples

### 📅 Semana 3-4: Principios SOLID
- **Día 1-3**: Single Responsibility y Open/Closed
- **Día 4-5**: Liskov Substitution e Interface Segregation
- **Día 6-7**: Dependency Inversion y práctica general

### 📅 Semana 5-6: Patrones Básicos
- **Día 1-3**: Patrones creacionales (Singleton, Factory)
- **Día 4-6**: Patrones estructurales (Adapter, Decorator)
- **Día 7**: Patrones de comportamiento (Strategy, Observer)

### 📅 Semana 7-8: Arquitectura Simple
- **Día 1-3**: Arquitectura en capas
- **Día 4-5**: Principios de Clean Architecture
- **Día 6-7**: Práctica con un proyecto pequeño

## 🎯 Checklist de Diseño para Principiantes

Antes de escribir código, pregúntate:

### ✅ Modularidad
- [ ] ¿He dividido el problema en piezas pequeñas?
- [ ] ¿Cada pieza tiene una responsabilidad clara?
- [ ] ¿Puedo probar cada pieza por separado?

### ✅ Acoplamiento
- [ ] ¿Mis clases dependen de detalles específicos?
- [ ] ¿Puedo cambiar una pieza sin afectar a las demás?
- [ ] ¿Estoy inyectando dependencias en lugar de crearlas?

### ✅ Cohesión  
- [ ] ¿Cada clase tiene un propósito bien definido?
- [ ] ¿Están relacionados todos los métodos de una clase?
- [ ] ¿No tengo "clases God" que hagan de todo?

### ✅ Abstracción
- [ ] ¿Estoy ocultando detalles complejos?
- [ ] ¿La interfaz es simple de usar?
- [ ] ¿Los usuarios no necesitan conocer la implementación interna?

## 🔍 Errores Comunes de Principiantes y Cómo Evitarlos

### 🚫 Error 1: "Clases God"
**Problema**: Crear clases que hacen todo
```javascript
// Mal
class SistemaCompleto {
    // 500 líneas que hacen todo
}
```
**Solución**: Divide en clases pequeñas y enfocadas

### 🚫 Error 2: Acoplamiento Fuerte
**Problema**: Todo depende de todo
```javascript
// Mal
class Usuario {
    constructor() {
        this.db = new MySQLDatabase(); // Dependencia directa
        this.email = new GmailService();  // Otra dependencia directa
    }
}
```
**Solución**: Inyecta dependencias

### 🚫 Error 3: No Pensar en Cambios Futuros
**Problema**: Código rígido que no se puede modificar
```javascript
// Mal
if (tipo === "pdf") {
    // 100 líneas de código PDF
} else if (tipo === "excel") {
    // 100 líneas de código Excel
}
```
**Solución**: Usa patrones como Factory o Strategy

## 🏆 Proyecto Final de Diseño

**Objetivo**: Diseñar y codificar un sistema pequeño aplicando todo lo aprendido

### 📋 Requisitos del Proyecto:
Crea un **Sistema de Biblioteca** con:
- Gestión de libros (título, autor, ISBN)
- Gestión de usuarios (nombre, email, tipo)
- Sistema de préstamos (fechas, devoluciones)
- Generación de reportes (libros prestados, usuarios morosos)
- Persistencia de datos (en archivo para simplificar)

### 🎯 Criterios de evaluación:
- **Modularidad**: ¿Está bien dividido en componentes?
- **SOLID**: ¿Aplica los principios correctamente?
- **Patrones**: ¿Usa patrones apropiados?
- **Extensibilidad**: ¿Es fácil añadir nuevas funcionalidades?
- **Legibilidad**: ¿Es fácil de entender y mantener?

**Recuerda**: El buen diseño no es sobre escribir código complejo, sino sobre escribir código **simple que funcione bien y sea fácil de cambiar**.