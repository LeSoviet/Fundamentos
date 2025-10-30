# Control de Versiones

El control de versiones es una práctica fundamental en el desarrollo de software que permite gestionar cambios en el código fuente, colaborar eficazmente en equipo y mantener un historial completo de todas las modificaciones realizadas en un proyecto. Es una herramienta esencial para cualquier desarrollador profesional.

## ¿Qué es el Control de Versiones?

El control de versiones es un sistema que registra los cambios realizados en archivos y directorios a lo largo del tiempo, permitiendo recuperar versiones específicas en cualquier momento. En el contexto del desarrollo de software, se utiliza principalmente para:

- **Seguimiento de cambios**: Mantener un historial completo de modificaciones
- **Colaboración**: Permitir que múltiples desarrolladores trabajen simultáneamente
- **Ramificación y fusión**: Desarrollar características en paralelo
- **Recuperación**: Volver a versiones anteriores cuando sea necesario

## Sistemas de Control de Versiones

### Sistemas Centralizados vs Distribuidos

#### Sistemas Centralizados (CVS, Subversion)
- **Repositorio único**: Un servidor central contiene todo el historial
- **Conexión requerida**: Se necesita conexión para la mayoría de operaciones
- **Control centralizado**: Permisos y políticas gestionados centralmente

#### Sistemas Distribuidos (Git, Mercurial)
- **Repositorios completos**: Cada desarrollador tiene una copia completa del historial
- **Operaciones locales**: La mayoría de operaciones funcionan sin conexión
- **Flexibilidad**: Múltiples flujos de trabajo posibles

## Git: El Sistema de Control de Versiones Dominante

Git es el sistema de control de versiones más utilizado en la industria actual. Fue creado por Linus Torvalds en 2005 para el desarrollo del kernel de Linux.

### Conceptos Fundamentales de Git

#### 1. Repositorio
Un repositorio es una colección de archivos y su historial de cambios. Puede ser local (en tu máquina) o remoto (en un servidor como GitHub, GitLab).

#### 2. Commit
Un commit es una instantánea del proyecto en un momento específico. Cada commit tiene:
- **Identificador único**: Hash SHA-1
- **Mensaje descriptivo**: Explicación de los cambios
- **Autor y fecha**: Quién hizo el cambio y cuándo
- **Padre(s)**: Commit(s) anterior(es)

#### 3. Ramas (Branches)
Las ramas permiten desarrollar características en paralelo sin afectar la línea principal de desarrollo.

```bash
# Crear y cambiar a una nueva rama
git checkout -b nueva-funcionalidad

# Listar ramas
git branch

# Cambiar entre ramas
git checkout main
```

#### 4. Fusión (Merge)
Combinar cambios de una rama a otra.

```bash
# Fusionar una rama en la actual
git merge nueva-funcionalidad
```

### Flujo de Trabajo Básico de Git

#### 1. Área de Trabajo (Working Directory)
Archivos actuales en tu sistema de archivos.

#### 2. Área de Preparación (Staging Area)
Archivos preparados para el próximo commit.

#### 3. Repositorio (Repository)
Historial de commits almacenado.

#### Flujo típico:
```bash
# 1. Modificar archivos
echo "Nuevo contenido" > archivo.txt

# 2. Preparar cambios
git add archivo.txt

# 3. Crear commit
git commit -m "Añadir nuevo contenido al archivo"

# 4. Compartir cambios
git push origin main
```

## Estrategias de Ramificación

### Git Flow
Modelo de ramificación que define roles específicos para ramas:

#### Ramas principales:
- **main/master**: Código en producción
- **develop**: Última versión de desarrollo

#### Ramas de soporte:
- **feature/*: Nuevas funcionalidades
- **release/*: Preparación para lanzamiento
- **hotfix/*: Correcciones urgentes en producción

```bash
# Crear rama de feature
git checkout -b feature/nueva-funcionalidad develop

# Fusionar feature en develop
git checkout develop
git merge --no-ff feature/nueva-funcionalidad
git branch -d feature/nueva-funcionalidad
```

### GitHub Flow
Modelo más simple, ideal para despliegues continuos:

#### Principios:
- **main** siempre desplegable
- **Ramas de feature** para todo desarrollo
- **Pull Requests** para revisión de código
- **Despliegue automático** al fusionar en main

### Trunk Based Development
Todos los desarrolladores trabajan en una rama principal:

#### Características:
- **Ramas de corta vida**: Menos de un día
- **Integración frecuente**: Múltiples veces al día
- **Feature flags**: Control de características en tiempo de ejecución

## Commits Efectivos

### Características de Buenos Commits

#### 1. Atómicos
Cada commit debe representar un cambio lógico único:

```bash
# Bien - cambio específico
git commit -m "Añadir validación de email en formulario de registro"

# Mal - cambios múltiples sin relación
git commit -m "Cambios varios: validar email, actualizar README, arreglar CSS"
```

#### 2. Mensajes Descriptivos
Los mensajes deben explicar qué cambió y por qué:

##### Estructura recomendada:
```
<tipo>(<ámbito>): <descripción corta>

<cuerpo opcional>

<footer opcional>
```

##### Tipos comunes:
- **feat**: Nueva funcionalidad
- **fix**: Corrección de bug
- **docs**: Cambios en documentación
- **style**: Formato, punto y coma faltantes, etc.
- **refactor**: Refactorización de código
- **test**: Adición o corrección de pruebas
- **chore**: Cambios en herramientas, configuración

##### Ejemplos:
```bash
# Bien
feat(auth): añadir autenticación por OAuth2
fix(api): corregir error en endpoint de usuarios cuando id es null
docs(readme): actualizar instrucciones de instalación

# Mal
git commit -m "arreglos"  # Demasiado vago
git commit -m "cambios en el código"  # No descriptivo
```

### Convencional Commits
Especificación para mensajes de commit consistentes:

```bash
# Ejemplo con breaking change
feat(api)!: eliminar endpoint v1 de usuarios

# Ejemplo con scope
fix(auth): resolver problema de sesión expirada en mobile
```

## Pull Requests y Revisión de Código

### Beneficios de Pull Requests:
- **Revisión de calidad**: Múltiples ojos en el código
- **Discusión de cambios**: Conversación sobre decisiones técnicas
- **Documentación**: Historial de decisiones de diseño
- **Control de acceso**: Aprobación requerida antes de integrar

### Buenas Práticas para Pull Requests:

#### 1. Tamaño Adecuado
- **Ideal**: 200-400 líneas de código cambiadas
- **Máximo recomendado**: 1000 líneas
- **Múltiples PRs**: Dividir cambios grandes en partes manejables

#### 2. Descripción Clara
```markdown
## ¿Qué hace este PR?
Implementa la funcionalidad de búsqueda de usuarios en el panel de administración.

## ¿Por qué es necesario?
Los administradores necesitan encontrar usuarios rápidamente para gestionar sus cuentas.

## ¿Cómo lo prueba?
1. Navega a /admin/usuarios
2. Usa el campo de búsqueda
3. Verifica que los resultados se filtren correctamente

## Screenshots (si aplica)
![Vista de búsqueda](url-a-imagen)
```

#### 3. Checklist de Revisión
- [ ] Código sigue estándares del proyecto
- [ ] Pruebas unitarias añadidas/actualizadas
- [ ] Documentación actualizada
- [ ] No hay código comentado
- [ ] Variables y funciones tienen nombres claros

## Gestión de Conflictos

### Identificar Conflictos
```bash
# Al hacer pull o merge
git pull origin main
# Auto-merging archivo.js
# CONFLICT (content): Merge conflict in archivo.js
```

### Resolver Conflictos
```javascript
// En el archivo con conflicto:
<<<<<<< HEAD
funcionOriginal();
=======
funcionModificada();
>>>>>>> rama-feature
```

#### Pasos para resolver:
1. Editar el archivo y elegir el código correcto
2. Eliminar los marcadores de conflicto (`<<<<<<<`, `=======`, `>>>>>>>`)
3. Añadir el archivo resuelto: `git add archivo.js`
4. Completar el merge: `git commit`

### Prevenir Conflictos
- **Pull frecuente**: Mantenerse actualizado con la rama principal
- **Commits pequeños**: Cambios más pequeños generan menos conflictos
- **Comunicación**: Coordinar con el equipo sobre áreas de trabajo

## Etiquetado y Versionado

### Etiquetas (Tags)
Marcadores para releases específicos:

```bash
# Crear etiqueta ligera
git tag v1.0.0

# Crear etiqueta anotada
git tag -a v1.0.0 -m "Versión 1.0.0 - Lanzamiento inicial"

# Compartir etiquetas
git push origin v1.0.0
```

### Versionado Semántico (SemVer)
Formato: `MAJOR.MINOR.PATCH`

#### Reglas:
- **MAJOR**: Cambios incompatibles en API
- **MINOR**: Funcionalidades nuevas compatibles
- **PATCH**: Correcciones de bugs compatibles

#### Ejemplos:
- `1.0.0`: Versión inicial
- `1.0.1`: Corrección de bug
- `1.1.0`: Nueva funcionalidad
- `2.0.0`: Cambio incompatible

## Herramientas y Plataformas

### Plataformas de Git
- **GitHub**: La más popular, integración con CI/CD
- **GitLab**: Solución completa con CI/CD integrado
- **Bitbucket**: Integración con herramientas Atlassian
- **Azure DevOps**: Solución empresarial de Microsoft

### Herramientas de Cliente
- **Git CLI**: Interfaz de línea de comandos estándar
- **GitHub Desktop**: Cliente gráfico para principiantes
- **SourceTree**: Cliente gráfico avanzado
- **VS Code**: Integración nativa con Git

### Extensiones Útiles
- **Git hooks**: Scripts que se ejecutan en eventos de Git
- **Pre-commit**: Framework para hooks de pre-commit
- **Commitlint**: Herramienta para validar mensajes de commit

## Métricas y Análisis

### Métricas Importantes
- **Frecuencia de commits**: Actividad del equipo
- **Tamaño de commits**: Granularidad de cambios
- **Tiempo de merge**: Velocidad de revisión
- **Tasa de conflictos**: Calidad de la colaboración

### Herramientas de Análisis
- **GitStats**: Estadísticas detalladas del repositorio
- **GitInsight**: Visualización de métricas de Git
- **CodeScene**: Análisis de complejidad y hotspots

## Buenas Prácticas Avanzadas

### 1. Rebase Interactivo
Limpiar el historial antes de fusionar:

```bash
# Rebase interactivo de los últimos 3 commits
git rebase -i HEAD~3
```

### 2. Cherry-Pick Selectivo
Aplicar commits específicos de otras ramas:

```bash
# Aplicar un commit específico
git cherry-pick abc1234
```

### 3. Bisect para Debugging
Encontrar el commit que introdujo un bug:

```bash
git bisect start
git bisect bad                 # Commit actual tiene el bug
git bisect good v1.0.0         # Último commit bueno conocido
# Git checkout commits intermedios para probar
git bisect good                # Marcar commit actual como bueno
git bisect bad                 # Marcar commit actual como malo
```

### 4. Worktrees
Trabajar en múltiples ramas simultáneamente:

```bash
# Crear worktree para una rama
git worktree add ../proyecto-feature feature/nueva-funcionalidad
```

## Integración con CI/CD

### Hooks de Git
Scripts que se ejecutan en eventos específicos:

#### Hooks del lado cliente:
- **pre-commit**: Validar cambios antes de commit
- **commit-msg**: Validar formato de mensajes
- **pre-push**: Validaciones antes de push

#### Hooks del lado servidor:
- **pre-receive**: Validaciones antes de aceptar cambios
- **post-receive**: Notificaciones después de recibir cambios

### Configuración Ejemplo
```bash
# .git/hooks/pre-commit
#!/bin/sh
# Ejecutar linter antes de cada commit
npm run lint
if [ $? -ne 0 ]; then
  echo "Linting failed. Commit aborted."
  exit 1
fi
```

## Recursos Adicionales

- Libro: "Pro Git" por Scott Chacon (gratis en git-scm.com)
- Libro: "Git for Teams" por Emma Hogbin Westby
- Curso: "Git Complete" en Udemy
- Sitio web: learn.github.com
- Herramienta: git-school.github.io/visualizing-git

---

*"El control de versiones no es solo una herramienta técnica, es una forma de comunicación entre desarrolladores. Cada commit cuenta una historia sobre cómo y por qué cambió el código. Escribe esa historia con claridad."*