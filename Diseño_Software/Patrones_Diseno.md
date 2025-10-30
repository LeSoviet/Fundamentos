# Patrones de Diseño

Los patrones de diseño son soluciones reutilizables a problemas comunes en el diseño de software. No son código terminado que puedas copiar y pegar, sino plantillas que describen cómo resolver un problema en un contexto determinado. Son esenciales para crear software mantenible, flexible y comprensible.

## ¿Qué son los Patrones de Diseño?

Los patrones de diseño son mejores prácticas formalizadas que un programador puede usar para resolver problemas comunes al diseñar una aplicación o sistema. Fueron popularizados por el libro "Design Patterns: Elements of Reusable Object-Oriented Software" de la "Gang of Four" (Erich Gamma, Richard Helm, Ralph Johnson, y John Vlissides).

### Beneficios de Usar Patrones de Diseño:

1. **Soluciones probadas**: Han sido probadas y refinadas por otros desarrolladores
2. **Comunicación común**: Proporcionan un vocabulario común entre desarrolladores
3. **Mantenibilidad**: Facilitan el mantenimiento del código
4. **Flexibilidad**: Hacen que el código sea más flexible y reutilizable
5. **Documentación implícita**: El uso de patrones documenta la intención del diseño

## Categorías de Patrones de Diseño

### 1. Patrones Creacionales
Estos patrones se enfocan en la creación de objetos, proporcionando mecanismos de creación flexibles y reutilizables.

### 2. Patrones Estructurales
Estos patrones se enfocan en la composición de clases y objetos para formar estructuras más grandes.

### 3. Patrones de Comportamiento
Estos patrones se enfocan en la comunicación entre objetos y la asignación de responsabilidades.

## Patrones Creacionales

### Singleton
Garantiza que una clase tenga solo una instancia y proporciona un punto de acceso global a ella.

#### Cuándo usar:
- Cuando necesitas exactamente una instancia de una clase
- Cuando esa instancia debe ser accesible desde cualquier parte del programa

#### Ejemplo:
```javascript
class Configuracion {
    constructor() {
        if (Configuracion.instance) {
            return Configuracion.instance;
        }
        
        this.config = {};
        Configuracion.instance = this;
        return this;
    }
    
    set(key, value) {
        this.config[key] = value;
    }
    
    get(key) {
        return this.config[key];
    }
}

// Uso
const config1 = new Configuracion();
const config2 = new Configuracion();
console.log(config1 === config2); // true
```

### Factory Method
Define una interfaz para crear un objeto, pero permite que las subclases decidan qué clase instanciar.

#### Cuándo usar:
- Cuando una clase no puede anticipar la clase de objetos que debe crear
- Cuando una clase quiere que sus subclases especifiquen los objetos que crea

#### Ejemplo:
```javascript
class Creador {
    crearProducto() {
        throw new Error("Método crearProducto debe ser implementado");
    }
    
    operacion() {
        const producto = this.crearProducto();
        return producto.operacion();
    }
}

class CreadorConcretoA extends Creador {
    crearProducto() {
        return new ProductoConcretoA();
    }
}

class CreadorConcretoB extends Creador {
    crearProducto() {
        return new ProductoConcretoB();
    }
}

class Producto {
    operacion() {
        throw new Error("Método operacion debe ser implementado");
    }
}

class ProductoConcretoA extends Producto {
    operacion() {
        return "Resultado del Producto A";
    }
}

class ProductoConcretoB extends Producto {
    operacion() {
        return "Resultado del Producto B";
    }
}

// Uso
const creadorA = new CreadorConcretoA();
console.log(creadorA.operacion()); // "Resultado del Producto A"
```

### Abstract Factory
Proporciona una interfaz para crear familias de objetos relacionados o dependientes sin especificar sus clases concretas.

#### Cuándo usar:
- Cuando el sistema debe ser independiente de cómo se crean y componen sus productos
- Cuando el sistema debe configurarse con una de múltiples familias de productos

#### Ejemplo:
```javascript
// Interfaces abstractas
class FabricaAbstracta {
    crearSilla() {}
    crearMesa() {}
}

class FabricaModerna extends FabricaAbstracta {
    crearSilla() {
        return new SillaModerna();
    }
    
    crearMesa() {
        return new MesaModerna();
    }
}

class FabricaVictoriana extends FabricaAbstracta {
    crearSilla() {
        return new SillaVictoriana();
    }
    
    crearMesa() {
        return new MesaVictoriana();
    }
}

// Productos
class Silla {
    sentarse() {}
}

class SillaModerna extends Silla {
    sentarse() {
        return "Sentado en una silla moderna";
    }
}

class SillaVictoriana extends Silla {
    sentarse() {
        return "Sentado en una silla victoriana";
    }
}

class Mesa {
    usar() {}
}

class MesaModerna extends Mesa {
    usar() {
        return "Usando una mesa moderna";
    }
}

class MesaVictoriana extends Mesa {
    usar() {
        return "Usando una mesa victoriana";
    }
}

// Uso
function cliente(fabrica) {
    const silla = fabrica.crearSilla();
    const mesa = fabrica.crearMesa();
    
    console.log(silla.sentarse());
    console.log(mesa.usar());
}

const fabricaModerna = new FabricaModerna();
cliente(fabricaModerna);
```

## Patrones Estructurales

### Adapter
Permite que objetos con interfaces incompatibles puedan colaborar entre sí.

#### Cuándo usar:
- Cuando quieres usar una clase existente pero su interfaz no es compatible con la que necesitas
- Cuando quieres crear una clase reutilizable que coopere con clases que no tienen interfaces compatibles

#### Ejemplo:
```javascript
// Interfaz objetivo
class ReproductorAudio {
    reproducir(tipo, nombre) {}
}

// Clase existente con interfaz incompatible
class ReproductorMP3 {
    reproducirMP3(nombre) {
        console.log(`Reproduciendo archivo MP3: ${nombre}`);
    }
}

// Adaptador
class AdaptadorMP3 extends ReproductorAudio {
    constructor() {
        super();
        this.reproductorMP3 = new ReproductorMP3();
    }
    
    reproducir(tipo, nombre) {
        if (tipo === "mp3") {
            this.reproductorMP3.reproducirMP3(nombre);
        }
    }
}

// Uso
const adaptador = new AdaptadorMP3();
adaptador.reproducir("mp3", "cancion.mp3");
```

### Decorator
Añade nuevas funcionalidades a objetos colocando estos objetos dentro de objetos especiales decoradores que contienen las funcionalidades.

#### Cuándo usar:
- Para añadir funcionalidades a objetos de forma dinámica sin afectar el comportamiento de otros objetos de la misma clase
- Cuando la extensión mediante subclases no es práctica

#### Ejemplo:
```javascript
class Componente {
    operacion() {}
}

class ComponenteConcreto extends Componente {
    operacion() {
        return "Componente base";
    }
}

class Decorador extends Componente {
    constructor(componente) {
        super();
        this.componente = componente;
    }
    
    operacion() {
        return this.componente.operacion();
    }
}

class DecoradorConcretoA extends Decorador {
    operacion() {
        return `Decorador A(${super.operacion()})`;
    }
}

class DecoradorConcretoB extends Decorador {
    operacion() {
        return `Decorador B(${super.operacion()})`;
    }
}

// Uso
let componente = new ComponenteConcreto();
console.log(componente.operacion()); // "Componente base"

componente = new DecoradorConcretoA(componente);
console.log(componente.operacion()); // "Decorador A(Componente base)"

componente = new DecoradorConcretoB(componente);
console.log(componente.operacion()); // "Decorador B(Decorador A(Componente base))"
```

### Facade
Proporciona una interfaz simplificada para una biblioteca, framework o cualquier conjunto complejo de clases.

#### Cuándo usar:
- Para proporcionar una interfaz simple a un subsistema complejo
- Para estructurar un sistema en capas
- Para reducir dependencias entre subsistemas

#### Ejemplo:
```javascript
// Subsistema complejo
class CPU {
    freeze() { console.log("CPU freeze"); }
    jump(position) { console.log(`CPU jump to ${position}`); }
    execute() { console.log("CPU execute"); }
}

class Memoria {
    cargar(position, data) { console.log(`Memoria cargar en ${position}: ${data}`); }
}

class DiscoDuro {
    leer(lba, size) { 
        console.log(`Disco leer LBA: ${lba}, Size: ${size}`);
        return "datos del disco";
    }
}

// Facade
class ComputadoraFacade {
    constructor() {
        this.cpu = new CPU();
        this.memoria = new Memoria();
        this.disco = new DiscoDuro();
    }
    
    iniciar() {
        this.cpu.freeze();
        const datos = this.disco.leer(0, 1024);
        this.memoria.cargar(0, datos);
        this.cpu.jump(0);
        this.cpu.execute();
    }
}

// Uso
const computadora = new ComputadoraFacade();
computadora.iniciar();
```

## Patrones de Comportamiento

### Observer
Define una dependencia uno-a-muchos entre objetos de forma que cuando un objeto cambia de estado, todos sus dependientes son notificados automáticamente.

#### Cuándo usar:
- Cuando un cambio en un objeto requiere cambiar otros objetos, y no sabes cuántos objetos necesitan ser cambiados
- Cuando un objeto debe ser capaz de notificar a otros objetos sin hacer suposiciones sobre quiénes son esos objetos

#### Ejemplo:
```javascript
class Sujeto {
    constructor() {
        this.observadores = [];
    }
    
    agregarObservador(observador) {
        this.observadores.push(observador);
    }
    
    eliminarObservador(observador) {
        const index = this.observadores.indexOf(observador);
        if (index > -1) {
            this.observadores.splice(index, 1);
        }
    }
    
    notificar(evento) {
        this.observadores.forEach(observador => {
            observador.actualizar(evento);
        });
    }
}

class SujetoConcreto extends Sujeto {
    constructor() {
        super();
        this.estado = null;
    }
    
    getEstado() {
        return this.estado;
    }
    
    setEstado(estado) {
        this.estado = estado;
        this.notificar(estado);
    }
}

class Observador {
    actualizar(evento) {}
}

class ObservadorConcreto extends Observador {
    constructor(nombre) {
        super();
        this.nombre = nombre;
    }
    
    actualizar(evento) {
        console.log(`${this.nombre} recibió notificación: ${evento}`);
    }
}

// Uso
const sujeto = new SujetoConcreto();
const observador1 = new ObservadorConcreto("Observador 1");
const observador2 = new ObservadorConcreto("Observador 2");

sujeto.agregarObservador(observador1);
sujeto.agregarObservador(observador2);

sujeto.setEstado("Nuevo estado");
```

### Strategy
Define una familia de algoritmos, encapsula cada uno, y los hace intercambiables. Permite que el algoritmo varíe independientemente de los clientes que lo usan.

#### Cuándo usar:
- Cuando muchos algoritmos relacionados difieren solo en la forma en que realizan cierto comportamiento
- Cuando necesitas variar un algoritmo en tiempo de ejecución
- Cuando hay muchos condicionales complejos que determinan qué algoritmo usar

#### Ejemplo:
```javascript
class Estrategia {
    ejecutar(datos) {}
}

class EstrategiaConcretaA extends Estrategia {
    ejecutar(datos) {
        return `Estrategia A procesó: ${datos.sort().join(', ')}`;
    }
}

class EstrategiaConcretaB extends Estrategia {
    ejecutar(datos) {
        return `Estrategia B procesó: ${datos.reverse().join(', ')}`;
    }
}

class Contexto {
    constructor(estrategia) {
        this.estrategia = estrategia;
    }
    
    setEstrategia(estrategia) {
        this.estrategia = estrategia;
    }
    
    ejecutarEstrategia(datos) {
        return this.estrategia.ejecutar(datos);
    }
}

// Uso
const datos = [3, 1, 4, 1, 5, 9, 2, 6];
const contexto = new Contexto(new EstrategiaConcretaA());
console.log(contexto.ejecutarEstrategia([...datos])); // Orden ascendente

contexto.setEstrategia(new EstrategiaConcretaB());
console.log(contexto.ejecutarEstrategia([...datos])); // Orden descendente
```

## Cómo Elegir el Patrón Adecuado

### Preguntas para Guiar tu Elección:

1. **¿Estás creando objetos?** → Considera patrones creacionales
2. **¿Estás componiendo objetos?** → Considera patrones estructurales
3. **¿Estás tratando con comunicación entre objetos?** → Considera patrones de comportamiento
4. **¿Necesitas flexibilidad en tiempo de ejecución?** → Considera Strategy, State, o Command
5. **¿Necesitas notificaciones automáticas?** → Considera Observer
6. **¿Tienes interfaces incompatibles?** → Considera Adapter

### Consejos Prácticos:

- **No fuerces el uso de patrones**: Usa patrones solo cuando resuelven un problema real
- **Empieza simple**: No añadas complejidad innecesaria
- **Refactoriza hacia patrones**: A veces es mejor aplicar patrones durante la refactorización
- **Aprende a reconocer problemas**: Con la práctica, identificarás cuándo un patrón puede ayudar

## Recursos Adicionales

- Libro: "Design Patterns: Elements of Reusable Object-Oriented Software" (Gang of Four)
- Libro: "Head First Design Patterns" de Eric Freeman
- Sitio web: refactoring.guru/design-patterns
- Curso: "Design Patterns in JavaScript" en Udemy

---

*"Los patrones de diseño son como herramientas en un cinturón: cuanto mejor entiendas cuándo y cómo usar cada una, más efectivo serás como diseñador de software."*