# Buenas Prácticas en el Desarrollo de Software

Las buenas prácticas en el desarrollo de software son principios, técnicas y metodologías que ayudan a crear código de calidad, mantenible y eficiente. Estas prácticas no solo mejoran el producto final, sino que también facilitan el trabajo en equipo y reducen el costo de mantenimiento a largo plazo.

## 📚 Contenido de esta Sección

1. [Código Limpio](./Codigo_Limpio.md) - Escribir código legible y mantenible
2. [Pruebas de Software](./Pruebas_Software.md) - Garantizar la calidad y confiabilidad
3. [Control de Versiones](./Control_Versiones.md) - Gestionar cambios y colaboración

## ¿Por Qué las Buenas Prácticas son Cruciales para Trainees/Juniors?

### Impacto Directo en tu Carrera
**Como desarrollador junior, seguir buenas prácticas te ayudará a:**
1. **Sobrevivir al período de prueba** - Los equipos valoran a quienes escriben código limpio
2. **Aprender más rápido** - Código bien estructurado es más fácil de entender
3. **Evitar errores costosos** - Pequeños descuidos pueden causar grandes problemas
4. **Ganar confianza de tu equipo** - Demuestras profesionalismo y responsabilidad
5. **Crecer hacia roles senior** - Las buenas prácticas son base para el liderazgo técnico

### Datos que te Motivarán:
- **Desarrolladores que siguen buenas prácticas** son promovidos **40% más rápido**
- **Código sin buenas prácticas** cuesta **3-5x más** de mantener
- **Bugs encontrados tarde** cuestan **100x más** que bugs encontrados temprano
- **Equipos con buenas prácticas** entregan **2-3x más rápido**

## Código Limpio: Tu Primera Impresión Profesional

### Nombres Significativos: La Base de Todo

#### Regla de Oro: El código se lee más veces de las que se escribe

**Mal (confuso para todos):**
```javascript
let d = ['Ana', 'Carlos', 'María'];
let x = 25;
let f = (n) => n * 2;
```

**Bien (claro para ti y para otros):**
```javascript
let nombresEstudiantes = ['Ana', 'Carlos', 'María'];
let edadMinima = 25;
let calcularDoble = (numero) => numero * 2;
```

#### Guía Práctica de Nomenclatura:

**Variables (sustantivos):**
```javascript
// Bueno
let usuarioActual = 'juan.perez';
let totalProductos = 150;
let esAutenticado = true;

// Malo
let usr = 'juan.perez';
let tp = 150;
let flag = true;
```

**Funciones (verbos + sustantivo):**
```javascript
// Bueno
function obtenerUsuarioPorId(id) { }
function calcularTotalFactura(productos) { }
function validarEmail(email) { }

// Malo
function user(id) { }
function calc(items) { }
function check(e) { }
```

**Clases (PascalCase, sustantivos):**
```javascript
// Bueno
class GestorUsuarios { }
class ServicioAutenticacion { }
class CalculadoraImpuestos { }

// Malo
class user { }
class auth { }
class calc { }
```

### Funciones y Métodos: Pequeñas y Enfocadas

#### Regla Práctica: Una función = una responsabilidad

**Mal (hace demasiadas cosas):**
```javascript
function procesarPedido(pedido) {
    // Validar datos
    if (!pedido.email || !pedido.productos) {
        throw new Error('Datos inválidos');
    }
    
    // Calcular total
    let total = 0;
    for (let p of pedido.productos) {
        total += p.precio * p.cantidad;
    }
    
    // Guardar en base de datos
    database.save(pedido);
    
    // Enviar email
    emailService.send(pedido.email, 'Pedido confirmado');
    
    // Actualizar inventario
    for (let p of pedido.productos) {
        inventory.reduce(p.id, p.cantidad);
    }
    
    return { success: true, total: total };
}
```

**Bien (dividido en funciones pequeñas):**
```javascript
function procesarPedido(pedido) {
    validarPedido(pedido);
    let total = calcularTotalPedido(pedido);
    guardarPedido(pedido);
    enviarConfirmacionPedido(pedido);
    actualizarInventario(pedido);
    
    return { success: true, total: total };
}

function validarPedido(pedido) {
    if (!pedido.email || !pedido.productos) {
        throw new Error('Datos inválidos');
    }
}

function calcularTotalPedido(pedido) {
    return pedido.productos.reduce((total, p) => 
        total + p.precio * p.cantidad, 0);
}

function guardarPedido(pedido) {
    database.save(pedido);
}

function enviarConfirmacionPedido(pedido) {
    emailService.send(pedido.email, 'Pedido confirmado');
}

function actualizarInventario(pedido) {
    pedido.productos.forEach(p => 
        inventory.reduce(p.id, p.cantidad));
}
```

#### Checklist para Funciones:
- [ ] ¿Cabe en una pantalla? Si no, probablemente hace demasiado
- [ ] ¿Tiene un solo verbo en el nombre? Si tiene "y", probablemente hace múltiples cosas
- [ ] ¿Menos de 3 parámetros? Si no, considera agrupar en un objeto
- [ ] ¿Sin efectos secundarios? Si modifica algo externo, documentarlo claramente

### Comentarios: Cuándo y Cómo

#### Regla de Oro: Comenta el "por qué", no el "qué"

**Mal (obvio e innecesario):**
```javascript
// Incrementa el contador en 1
contador++;

// Recorre el array de usuarios
for (let usuario of usuarios) {
    // Imprime el nombre del usuario
    console.log(usuario.nombre);
}
```

**Bien (explica el por qué):**
```javascript
// Necesitamos incrementar el contador antes de validar
// porque la validación espera que el ID sea único
contador++;

// Iteramos sobre usuarios activos para enviar notificaciones
// Los usuarios inactivos fueron filtrados previamente
for (let usuario of usuariosActivos) {
    sendNotification(usuario.email, 'Nuevo mensaje disponible');
}
```

#### Tipos de Comentarios Útiles:

**1. Explicación de decisiones complejas:**
```javascript
// Usamos Bubble Sort porque el array es pequeño (<100 elementos)
// y para datasets pequeños es más rápido que QuickSort
function ordenarPequeñoArray(array) {
    // Implementación Bubble Sort
}
```

**2. Advertencias importantes:**
```javascript
// ⚠️ ADVERTENCIA: Esta función modifica el array original
// Si necesitas preservar el original, usa crearCopia() primero
function eliminarDuplicados(array) {
    // Modifica array directamente
}
```

**3. TODOs con contexto:**
```javascript
// TODO: Optimizar esta consulta cuando migremos a PostgreSQL
// Actualmente hace N+1 queries, afecta rendimiento con >1000 usuarios
// Fecha límite: Q2 2024, Responsable: equipo backend
function obtenerUsuariosConPedidos() {
    // Implementación actual
}
```

## Pruebas de Software

### Pirámide de Pruebas
- **Pruebas unitarias**: Mayor cantidad, menor alcance
- **Pruebas de integración**: Prueban interacciones entre componentes
- **Pruebas end-to-end**: Prueban flujos completos del usuario

### Principios de Pruebas
- **FIRST**: Fast, Independent, Repeatable, Self-validating, Timely
- **TDD**: Test-Driven Development (escribir pruebas antes del código)
- **Cobertura**: Apunta a una cobertura razonable (80-90%)
- **Mocking**: Usa mocks para aislar unidades bajo prueba

### Tipos de Pruebas
- **Unitarias**: Prueban unidades individuales de código
- **Integración**: Verifican la interacción entre componentes
- **Funcionales**: Validan que el software cumple con los requisitos
- **Regresión**: Aseguran que nuevas funcionalidades no rompen lo existente
- **Rendimiento**: Evalúan la eficiencia del sistema
- **Seguridad**: Identifican vulnerabilidades en el software

## 🔄 Control de Versiones

### Commits
- **Commits atómicos**: Cada commit debe representar un cambio lógico único
- **Mensajes descriptivos**: Explica qué cambió y por qué
- **Formato consistente**: Sigue una convención de mensajes (Conventional Commits)
- **Frecuencia**: Haz commits pequeños y frecuentes

### Ramas
- **Estrategias de ramificación**: Git Flow, GitHub Flow, Trunk Based Development
- **Nombres descriptivos**: Usa nombres que indiquen el propósito de la rama
- **Limpieza**: Elimina ramas que ya no se necesiten

### Revisiones de Código
- **Pull Requests**: Revisa el código de tus colegas antes de integrarlo
- **Checklist de revisión**: Sigue una lista de verificación consistente
- **Feedback constructivo**: Ofrece sugerencias respetuosas y útiles
- **Automatización**: Usa herramientas de linting y análisis estándar

## 🛡️ Seguridad

### Principios de Seguridad
- **Principio del menor privilegio**: Otorga solo los permisos necesarios
- **Validación de entradas**: Nunca confíes en los datos del usuario
- **Prevención de inyecciones**: Protege contra SQL injection, XSS, etc.
- **Gestión de contraseñas**: Usa hashing seguro y políticas robustas

### Buenas Prácticas de Seguridad
- **HTTPS**: Usa siempre conexiones seguras
- **Autenticación**: Implementa mecanismos robustos de autenticación
- **Autorización**: Verifica permisos en cada solicitud
- **Logging**: Registra eventos de seguridad relevantes
- **Actualizaciones**: Mantén dependencias actualizadas

## 📊 Rendimiento

### Optimización
- **Premature optimization**: No optimices antes de medir
- **Cuellos de botella**: Identifica problemas reales con profiling
- **Algoritmos eficientes**: Elige estructuras de datos y algoritmos apropiados
- **Caching**: Usa caching estratégicamente para mejorar el rendimiento

### Monitoreo
- **Métricas clave**: Tiempo de respuesta, tasa de errores, uso de recursos
- **Alertas**: Configura alertas para problemas críticos
- **Logs**: Implementa logging estructurado y útil
- **Instrumentación**: Mide lo que importa para el negocio

## 🏗️ Arquitectura y Diseño

### Principios de Diseño
- **SOLID**: Sigue los principios SOLID para diseño orientado a objetos
- **DRY**: No te repitas (Don't Repeat Yourself)
- **KISS**: Mantén las cosas simples (Keep It Simple, Stupid)
- **YAGNI**: No lo vas a necesitar (You Aren't Gonna Need It)

### Modularidad
- **Bajo acoplamiento**: Reduce dependencias entre módulos
- **Alta cohesión**: Mantiene funcionalidades relacionadas juntas
- **Separación de preocupaciones**: Divide el sistema en capas lógicas
- **Reusabilidad**: Diseña componentes reutilizables

## 📋 Documentación

### Tipos de Documentación
- **Documentación de código**: Comentarios y documentación en el código
- **Documentación técnica**: Arquitectura, APIs, configuraciones
- **Documentación de usuario**: Guías de usuario, tutoriales
- **Documentación de procesos**: Procedimientos del equipo, estándares

### Buenas Prácticas
- **Mantén actualizada**: La documentación obsoleta es peor que ninguna
- **Accesible**: Haz que la documentación sea fácil de encontrar y navegar
- **Automatizada**: Genera documentación automáticamente cuando sea posible
- **Ejemplos**: Incluye ejemplos prácticos de uso

## 🛠️ Herramientas y Automatización

### Integración Continua/Entrega Continua (CI/CD)
- **Automatización**: Automatiza pruebas, construcción y despliegue
- **Feedback rápido**: Detecta problemas lo antes posible
- **Despliegues frecuentes**: Pequeños despliegues reducen riesgos
- **Ambientes consistentes**: Mantén consistencia entre ambientes

### Análisis Estático
- **Linting**: Detecta errores de estilo y posibles bugs
- **Análisis de calidad**: Evalúa complejidad, duplicados, etc.
- **Seguridad**: Escanea vulnerabilidades en dependencias
- **Cobertura**: Mide cobertura de pruebas automáticamente

## 🎯 Ejercicios Prácticos para Implementar Buenas Prácticas

### 📝 Ejercicio 1: Refactorización de Código (Semana 1)
**Objetivo**: Transformar código "malo" en código "limpio".

**Código inicial para refactorizar:**
```javascript
// Código MALO que debes mejorar
function proc(d) {
    let r = 0;
    for (let i = 0; i < d.length; i++) {
        if (d[i].age >= 18 && d[i].active) {
            r += d[i].salary;
        }
    }
    return r;
}
```

**✅ Tu misión**: Aplica las siguientes mejoras:
1. **Nombres descriptivos**: Cambia `proc`, `d`, `r`, `i`
2. **Funciones pequeñas**: Divide si es necesario
3. **Comentarios útiles**: Explica el propósito
4. **Validación**: Añade validación de entradas

**Solución esperada:**
```javascript
/**
 * Calcula el total de salarios de empleados activos y mayores de edad
 * @param {Array} empleados - Lista de objetos empleado
 * @returns {number} Total de salarios calculados
 */
function calcularTotalSalariosEmpleadosActivos(empleados) {
    validarArrayEmpleados(empleados);
    
    return empleados
        .filter(empleado => esEmpleadoActivoYMayorEdad(empleado))
        .reduce((total, empleado) => total + empleado.salary, 0);
}

function validarArrayEmpleados(empleados) {
    if (!Array.isArray(empleados)) {
        throw new Error('Se espera un array de empleados');
    }
}

function esEmpleadoActivoYMayorEdad(empleado) {
    return empleado.age >= 18 && empleado.active;
}
```

### 🧪 Ejercicio 2: Escribiendo tu Primera Prueba (Semana 2)
**Objetivo**: Aprender a escribir pruebas unitarias básicas.

**Función que debes probar:**
```javascript
function calcularDescuento(precioOriginal, porcentajeDescuento) {
    if (precioOriginal <= 0) {
        throw new Error('El precio debe ser mayor a 0');
    }
    if (porcentajeDescuento < 0 || porcentajeDescuento > 100) {
        throw new Error('El descuento debe estar entre 0 y 100');
    }
    
    return precioOriginal * (1 - porcentajeDescuento / 100);
}
```

**✅ Escribe pruebas para estos casos:**
1. **Caso normal**: 100 con 10% descuento = 90
2. **Borde**: 0.01 con 50% descuento = 0.005
3. **Error**: Precio negativo debe lanzar error
4. **Error**: Descuento > 100 debe lanzar error
5. **Límite**: 100 con 0% descuento = 100
6. **Límite**: 100 con 100% descuento = 0

**Plantilla de prueba (Jest):**
```javascript
describe('calcularDescuento', () => {
    // Escribe tus pruebas aquí
    test('debe calcular descuento correctamente', () => {
        expect(calcularDescuento(100, 10)).toBe(90);
    });
    
    // Completa con los otros casos...
});
```

### 🔄 Ejercicio 3: Commits Profesionales (Semana 3)
**Objetivo**: Aprender a escribir mensajes de commit efectivos.

**❌ Commits MALOS (evita estos):**
```
git commit -m "arreglar bug"
git commit -m "cambios"
git commit -m "fix"
git commit -m "working"
git commit -m "asdfghjkl"
```

**✅ Commits BUENOS (emula estos):**
```
feat: añadir validación de email en formulario de registro
fix: resolver error 500 en endpoint de usuarios cuando email es nulo
docs: actualizar README con instrucciones de instalación
refactor: optimizar función de cálculo de impuestos
test: añadir pruebas para servicio de autenticación
chore: actualizar dependencias de seguridad
```

**Ejercicio práctico:**
1. Crea un pequeño proyecto con 3-4 commits
2. Cada commit debe seguir el formato: `tipo: descripción`
3. La descripción debe responder: ¿Qué cambió? ¿Por qué?

### 📊 Ejercicio 4: Code Review Practice (Semana 4)
**Objetivo**: Aprender a dar feedback constructivo.

**Código para revisar:**
```javascript
function getUsers() {
    let users = [];
    // Get users from database
    db.query('SELECT * FROM users', (err, result) => {
        if (err) {
            console.log('Error getting users');
            return [];
        }
        users = result;
    });
    return users;
}
```

**✅ Escribe un comentario de review constructivo:**
- Identifica 2-3 problemas específicos
- Sugiere mejoras concretas
- Mantén un tono respetuoso y útil

**Ejemplo de buen comentario:**
```
👍 **Bueno**: La función tiene un propósito claro.

💡 **Sugerencias**:
1. **Problema de asíncronía**: La función devuelve `users` antes de que la query termine. 
   Debería usar async/await o devolver una promesa.
2. **Manejo de errores**: En lugar de console.log, podríamos lanzar el error 
   para que el llamador pueda manejarlo.
3. **Naming**: `getUsersFromDatabase()` sería más específico.

¿Qué te parece si lo refactorizamos así?
```

## 🚀 Guía de Implementación Paso a Paso

### Mes 1: Fundamentos de Código Limpio

**Semana 1: Nomenclatura**
- [ ] Revisa todo tu código y renombra variables confusas
- [ ] Crea un cheat sheet de convenciones para tu equipo
- [ ] Pide feedback a un senior sobre tus nombres

**Semana 2: Funciones pequeñas**
- [ ] Identifica funciones >20 líneas y divídelas
- [ ] Crea una función que haga exactamente una cosa
- [ ] Practica el principio de "single responsibility"

**Semana 3: Comentarios efectivos**
- [ ] Elimina comentarios obvios de tu código
- [ ] Añade comentarios que expliquen "por qué"
- [ ] Documenta funciones complejas con JSDoc

**Semana 4: Formato consistente**
- [ ] Configura un linter (ESLint, Prettier)
- [ ] Establece reglas de formato para tu equipo
- [ ] Automatiza el formateo en cada commit

### Mes 2: Testing y Calidad

**Semana 5-6: Pruebas unitarias**
- [ ] Escribe tu primera prueba unitaria
- [ ] Alcanza 50% de cobertura en un módulo pequeño
- [ ] Practica TDD en una función simple

**Semana 7-8: Integración continua**
- [ ] Configura GitHub Actions o similar
- [ ] Automatiza pruebas en cada push
- [ ] Configura linting automático

### Mes 3: Colaboración y Procesos

**Semana 9-10: Control de versiones**
- [ ] Domina las operaciones básicas de Git
- [ ] Practica branching strategies
- [ ] Participa en code reviews reales

**Semana 11-12: Documentación**
- [ ] Documenta una API que creaste
- [ ] Escribe un README claro para un proyecto
- [ ] Crea guías de contribución para tu equipo

## 🎯 Checklist Diario de Buenas Prácticas

### Antes de Escribir Código:
- [ ] **¿Entiendo el requisito?** Si no, pregunto antes
- [ ] **¿Hay código existente similar?** Reuso en lugar de reinventar
- [ ] **¿Necesito una prueba primero?** TDD si es complejo

### Mientras Escribes Código:
- [ ] **¿Nombres son descriptivos?** Variables, funciones, clases
- [ ] **¿Funciones son pequeñas?** <20 líneas, 1 responsabilidad
- [ ] **¿Estoy copiando código?** Si sí, extraigo a función
- [ ] **¿Necesito un comentario?** Explico el "por qué"

### Antes de Hacer Commit:
- [ ] **¿El código funciona?** Pruebas pasando
- [ ] **¿Seguí las convenciones?** Linting aprobado
- [ ] **¿Mensaje de commit es claro?** Qué y por qué
- [ ] **¿Añadí pruebas?** Cubro casos nuevos

### Antes de Pedir Review:
- [ ] **¿Auto-revisé mi código?** Problemas obvios corregidos
- [ ] **¿La PR es pequeña?** <300 líneas idealmente
- [ ] **¿Descripción es clara?** Contexto y cambios
- [ ] **¿Pruebas están actualizadas?** Todo funciona

## 📈 Métricas para Medir tu Progreso

### Métricas de Código Limpio:
- **Complejidad ciclomática**: <10 por función
- **Líneas por función**: <20 (idealmente <10)
- **Parámetros por función**: <3
- **Duplicación**: <3% del código total

### Métricas de Testing:
- **Cobertura de código**: >80%
- **Pruebas pasando**: 100%
- **Tiempo de pruebas**: <5 minutos

### Métricas de Colaboración:
- **Commits por día**: 3-5 (consistentes)
- **Tamaño de PR**: <300 líneas
- **Tiempo de review**: <24 horas
- **Issues cerrados**: >80% a tiempo

## 🏆 Proyecto Final de Buenas Prácticas

**Objetivo**: Crear un pequeño proyecto aplicando todo lo aprendido.

### Requisitos del Proyecto:
**Crea una API REST simple con:**
- CRUD para una entidad (ej: usuarios, tareas, productos)
- Validación de entradas
- Manejo de errores apropiado
- 80% de cobertura de pruebas
- Documentación completa
- CI/CD configurado
- Code reviews implementados

### Criterios de Evaluación:
- **Calidad de código**: ¿Sigue principios de clean code?
- **Testing**: ¿Las pruebas son útiles y completas?
- **Documentación**: ¿Es clara y actualizada?
- **Proceso**: ¿Usa Git profesionalmente?
- **Colaboración**: ¿Sería fácil para otro desarrollador contribuir?

### Entregables:
1. **Repositorio Git** con commits profesionales
2. **README** completo con instrucciones
3. **Documentación de API** (OpenAPI/Swagger)
4. **Suite de pruebas** con buena cobertura
5. **CI/CD** configurado y funcionando
6. **Pull Request template** y guías de contribución

**Recuerda**: Las buenas prácticas no son reglas rígidas, sino herramientas para escribir código que tú y otros puedan entender y mantener fácilmente. ¡La práctica constante es la clave!