# Pruebas de Software

Las pruebas de software son una práctica fundamental para garantizar la calidad, confiabilidad y mantenibilidad de las aplicaciones. Más que una simple verificación de que el código funciona, las pruebas son una disciplina que ayuda a prevenir errores, documentar el comportamiento del sistema y facilitar el mantenimiento a largo plazo.

## ¿Qué son las Pruebas de Software?

Las pruebas de software son el proceso de evaluar y verificar que un sistema de software funciona según lo esperado. Incluyen una variedad de técnicas y enfoques para identificar defectos, validar funcionalidades y asegurar la calidad del producto final.

### Importancia de las Pruebas:

1. **Detección temprana de errores**: Identificar problemas antes de que lleguen a producción
2. **Documentación viva**: Las pruebas describen cómo debe comportarse el sistema
3. **Confianza en los cambios**: Facilitar refactorizaciones y nuevas funcionalidades
4. **Mejora de la calidad**: Forzar pensamiento sobre casos límite y errores
5. **Reducción de costos**: Corregir errores temprano es más económico que en producción

## Pirámide de Pruebas

La pirámide de pruebas es un modelo que describe la distribución óptima de diferentes tipos de pruebas en un sistema:

```
        ▲
        │      Pruebas End-to-End
        │         (10-20%)
        │
    Pruebas de Integración
        (20-30%)
        │
        │      Pruebas Unitarias
        │        (70-80%)
        ▼
```

### 1. Pruebas Unitarias

Prueban unidades individuales de código (funciones, métodos, clases) de forma aislada.

#### Características:
- **Rápidas**: Se ejecutan en milisegundos
- **Aisladas**: No dependen de sistemas externos
- **Específicas**: Prueban una sola funcionalidad
- **Automatizadas**: Se ejecutan sin intervención manual

#### Ejemplo:
```javascript
// Función a probar
function calcularImpuesto(monto, tasa) {
    if (monto < 0) throw new Error("Monto no puede ser negativo");
    return monto * tasa;
}

// Prueba unitaria
describe('calcularImpuesto', () => {
    test('debe calcular correctamente el impuesto', () => {
        expect(calcularImpuesto(100, 0.15)).toBe(15);
    });
    
    test('debe lanzar error para montos negativos', () => {
        expect(() => calcularImpuesto(-10, 0.15)).toThrow("Monto no puede ser negativo");
    });
});
```

### 2. Pruebas de Integración

Prueban la interacción entre múltiples componentes o sistemas.

#### Características:
- **Moderadamente rápidas**: Segundos a minutos
- **Interacción real**: Componentes trabajan juntos
- **Alcance medio**: Prueban flujos completos pero limitados

#### Ejemplo:
```javascript
// Prueba de integración entre servicio y repositorio
describe('ServicioUsuario', () => {
    test('debe crear usuario y guardarlo en base de datos', async () => {
        const servicio = new ServicioUsuario(mockRepositorio);
        const datosUsuario = { nombre: 'Juan', email: 'juan@test.com' };
        
        const usuario = await servicio.crearUsuario(datosUsuario);
        
        expect(mockRepositorio.guardar).toHaveBeenCalledWith(expect.objectContaining(datosUsuario));
        expect(usuario.id).toBeDefined();
    });
});
```

### 3. Pruebas End-to-End (E2E)

Prueban flujos completos del usuario desde la interfaz hasta el backend.

#### Características:
- **Lentas**: Minutos para ejecutarse
- **Completas**: Prueban todo el sistema
- **Realistas**: Simulan uso real del usuario

#### Ejemplo:
```javascript
// Prueba E2E con Puppeteer
describe('Flujo de Compra', () => {
    test('usuario puede completar una compra', async () => {
        await page.goto('/productos');
        await page.click('.producto:first-child .agregar-carrito');
        await page.click('.carrito');
        await page.click('.proceder-compra');
        await page.fill('#nombre', 'Juan Pérez');
        await page.fill('#tarjeta', '1234567890123456');
        await page.click('.confirmar-compra');
        
        await expect(page).toHaveText('.mensaje-exito', 'Compra completada');
    });
});
```

## Principios de Pruebas Efectivas

### FIRST (Pruebas Limpias)

Las buenas pruebas siguen el acrónimo FIRST:

#### F - Fast (Rápidas)
- Se ejecutan rápidamente
- No bloquean el proceso de desarrollo
- Permiten ejecución frecuente

#### I - Independent (Independientes)
- No dependen de otras pruebas
- Se pueden ejecutar en cualquier orden
- No comparten estado entre sí

#### R - Repeatable (Repetibles)
- Producen el mismo resultado en cualquier entorno
- No dependen de datos externos variables
- Se pueden ejecutar múltiples veces

#### S - Self-Validating (Autovalidantes)
- Tienen resultado booleano claro (pasan o fallan)
- No requieren inspección manual
- Proporcionan feedback inmediato

#### T - Timely (Oportunas)
- Se escriben en el momento adecuado
- En TDD, antes del código de producción
- Just-In-Time para otros enfoques

### TDD (Test-Driven Development)

Desarrollo guiado por pruebas: escribir pruebas antes del código.

#### Ciclo Red-Green-Refactor:
1. **Red**: Escribir una prueba que falle
2. **Green**: Escribir el mínimo código para pasar la prueba
3. **Refactor**: Mejorar el código manteniendo las pruebas

#### Beneficios:
- Diseño mejorado por necesidad de testabilidad
- Cobertura de prueba garantizada
- Confianza en refactorizaciones
- Documentación viva del comportamiento

### AAA (Arrange-Act-Assert)

Estructura clara para escribir pruebas:

#### Arrange (Organizar)
Configurar el estado inicial y los datos de prueba:
```javascript
const calculadora = new Calculadora();
const a = 5;
const b = 3;
```

#### Act (Actuar)
Ejecutar la funcionalidad a probar:
```javascript
const resultado = calculadora.sumar(a, b);
```

#### Assert (Afirmar)
Verificar que el resultado es el esperado:
```javascript
expect(resultado).toBe(8);
```

## Tipos de Pruebas

### 1. Pruebas Funcionales

Verifican que el software cumple con los requisitos funcionales.

#### Subtipos:
- **Pruebas de aceptación**: Validar que el sistema cumple con criterios de aceptación
- **Pruebas de regresión**: Asegurar que nuevas funcionalidades no rompen lo existente
- **Pruebas de humo**: Verificación rápida de funcionalidades críticas

### 2. Pruebas No Funcionales

Verifican aspectos no relacionados directamente con funcionalidades.

#### Subtipos:
- **Pruebas de rendimiento**: Evaluar velocidad y eficiencia
- **Pruebas de carga**: Verificar comportamiento bajo estrés
- **Pruebas de seguridad**: Identificar vulnerabilidades
- **Pruebas de usabilidad**: Evaluar experiencia del usuario

### 3. Pruebas Manuales vs Automatizadas

#### Pruebas Manuales:
- Ejecutadas por personas
- Flexibles y adaptables
- Buenas para exploración y UX
- Costosas a largo plazo

#### Pruebas Automatizadas:
- Ejecutadas por herramientas
- Rápidas y repetibles
- Ideales para regresión
- Requieren mantenimiento

## Estrategias de Cobertura

### Cobertura de Código
Medir qué porcentaje del código es ejecutado por las pruebas.

#### Métricas importantes:
- **Cobertura de líneas**: Porcentaje de líneas ejecutadas
- **Cobertura de ramas**: Porcentaje de caminos condicionales cubiertos
- **Cobertura de funciones**: Porcentaje de funciones llamadas

#### Objetivo recomendado:
- **80-90%** de cobertura general
- **100%** en código crítico
- Calidad sobre cantidad

### Pruebas de Mutación
Técnica avanzada que introduce cambios pequeños en el código para verificar que las pruebas los detectan.

## Buenas Prácticas de Pruebas

### 1. Nombres Descriptivos

Los nombres de las pruebas deben describir claramente qué se está probando y qué se espera:

```javascript
// Mal
test('test1', () => { });

// Bien
test('debe calcular correctamente el impuesto para montos positivos', () => { });
test('debe lanzar error cuando el monto es negativo', () => { });
```

### 2. Datos de Prueba Realistas

Usar datos que representen escenarios reales:

```javascript
// Datos de prueba bien estructurados
const usuariosTestData = {
    usuarioValido: { nombre: 'Juan Pérez', email: 'juan@test.com' },
    usuarioInvalido: { nombre: '', email: 'invalido' },
    administrador: { nombre: 'Admin', email: 'admin@empresa.com', rol: 'admin' }
};
```

### 3. Mocks y Stubs Apropiados

Usar dobles de prueba para aislar unidades bajo prueba:

```javascript
// Mock para servicio externo
const mockEmailService = {
    enviar: jest.fn().mockResolvedValue(true)
};

// Stub para datos de prueba
const stubUsuario = {
    id: 1,
    nombre: 'Juan',
    email: 'juan@test.com'
};
```

### 4. Pruebas Independientes

Cada prueba debe poder ejecutarse por sí sola:

```javascript
// Cada test configura su propio estado
describe('Servicio de Usuarios', () => {
    beforeEach(() => {
        // Configuración limpia para cada test
        database.clear();
    });
    
    test('debe crear usuario correctamente', () => {
        // Test independiente
    });
    
    test('debe validar email único', () => {
        // Otro test independiente
    });
});
```

## Herramientas de Pruebas

### Frameworks de Pruebas

#### JavaScript/Node.js:
- **Jest**: Framework completo con mocking integrado
- **Mocha**: Framework flexible con múltiples assertion libraries
- **Jasmine**: Framework BDD con sintaxis limpia

#### Python:
- **pytest**: Framework moderno y poderoso
- **unittest**: Librería estándar de Python

#### Java:
- **JUnit**: Framework estándar para Java
- **TestNG**: Framework más avanzado

### Herramientas de Pruebas E2E

- **Cypress**: Para aplicaciones web modernas
- **Puppeteer**: Control de Chrome/Chromium programático
- **Selenium**: Automatización multi-navegador
- **Playwright**: Automatización moderna multi-navegador

### Análisis de Cobertura

- **Istanbul/nyc**: Para JavaScript
- **Coverage.py**: Para Python
- **JaCoCo**: Para Java

## Integración con CI/CD

Las pruebas deben ser parte del pipeline de integración continua:

### Pipeline típico:
1. **Pruebas unitarias**: Ejecutadas en cada commit
2. **Pruebas de integración**: Ejecutadas en merges a develop
3. **Pruebas E2E**: Ejecutadas en merges a main
4. **Análisis de calidad**: Verificación de cobertura y estándares

### Configuración ejemplo (GitHub Actions):
```yaml
name: CI
on: [push]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Instalar dependencias
      run: npm ci
    - name: Ejecutar pruebas unitarias
      run: npm test -- --coverage
    - name: Verificar cobertura
      run: npm run coverage:check
```

## Métricas y Monitoreo

### Métricas clave:
- **Tiempo de ejecución**: Velocidad del conjunto de pruebas
- **Tasa de fallos**: Porcentaje de builds que fallan por pruebas
- **Cobertura de código**: Porcentaje de código cubierto
- **Flakiness**: Pruebas que fallan intermitentemente

### Dashboards:
- Visualización de tendencias de pruebas
- Alertas para regresiones
- Métricas de rendimiento de pruebas

## Recursos Adicionales

- Libro: "Test Driven Development: By Example" de Kent Beck
- Libro: "Working Effectively with Legacy Code" de Michael Feathers
- Curso: "Testing JavaScript" en testingjavascript.com
- Sitio web: martinfowler.com/testing

---

*"Las pruebas no son una actividad adicional en el desarrollo de software, son una inversión en la calidad y mantenibilidad futura de tu código. Un sistema bien probado es un sistema confiable."*