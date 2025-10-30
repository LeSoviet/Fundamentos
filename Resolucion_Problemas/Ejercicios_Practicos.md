# Ejercicios Prácticos de Resolución de Problemas

La mejor manera de mejorar tus habilidades de resolución de problemas es practicando con ejercicios variados. Esta colección presenta problemas progresivamente más desafiantes junto con estrategias para abordarlos.

## Nivel Básico

### 1. Suma de Números Pares
**Problema**: Dado un arreglo de números enteros, encuentra la suma de todos los números pares.

**Estrategia**:
1. Iterar por cada número en el arreglo
2. Verificar si es par usando el operador módulo (%)
3. Si es par, agregarlo a una suma acumulativa

**Solución en pseudocódigo**:
```
funcion sumaPares(arreglo):
    suma = 0
    para cada numero en arreglo:
        si numero % 2 == 0:
            suma = suma + numero
    retornar suma
```

### 2. Invertir Cadena
**Problema**: Dada una cadena, devuelve la misma cadena pero invertida.

**Estrategia**:
1. Convertir cadena a arreglo de caracteres
2. Invertir el arreglo
3. Convertir arreglo de vuelta a cadena

**Alternativa**:
1. Usar dos punteros (inicio y fin)
2. Intercambiar caracteres y mover punteros hacia el centro

### 3. Encontrar Máximo
**Problema**: Dado un arreglo de números, encuentra el valor máximo.

**Estrategia**:
1. Asumir primer elemento como máximo
2. Comparar con cada elemento restante
3. Actualizar máximo si se encuentra uno mayor

## Nivel Intermedio

### 1. Palabras Únicas
**Problema**: Dada una lista de palabras, devuelve una lista con solo las palabras que aparecen una vez.

**Estrategia**:
1. Contar frecuencia de cada palabra usando un diccionario/hash map
2. Filtrar palabras con frecuencia igual a 1

**Complejidad**: O(n) tiempo, O(n) espacio

### 2. Rotación de Arreglo
**Problema**: Dado un arreglo y un número k, rota el arreglo k posiciones a la derecha.

**Estrategia**:
1. Normalizar k (k % longitud del arreglo)
2. Dividir arreglo en dos partes: últimos k elementos y resto
3. Concatenar segunda parte + primera parte

**Optimización**: Rotación in-place usando reversas:
1. Reversar todo el arreglo
2. Reversar primeros k elementos
3. Reversar elementos restantes

### 3. Comprimir Cadena
**Problema**: Implementa compresión básica de cadenas. Por ejemplo: "aaabbc" → "a3b2c1"

**Estrategia**:
1. Iterar por la cadena contando caracteres consecutivos
2. Construir resultado con carácter + conteo
3. Retornar cadena original si comprimida es más larga

## Nivel Avanzado

### 1. Subarreglo de Suma Máxima (Kadane's Algorithm)
**Problema**: Dado un arreglo de números (positivos y negativos), encuentra el subarreglo contiguo con la suma máxima.

**Estrategia**:
1. Mantener dos variables: suma máxima hasta ahora y suma máxima terminando en posición actual
2. Para cada elemento, decidir si agregarlo a subarreglo existente o comenzar nuevo
3. Actualizar máximo global

**Complejidad**: O(n) tiempo, O(1) espacio

### 2. Producto de Arreglo Excepto Self
**Problema**: Dado un arreglo de números, retorna un arreglo donde cada elemento es el producto de todos los demás elementos.

**Estrategia**:
1. Solución ingenua: Dos bucles anidados (O(n²))
2. Solución óptima: Dos pasadas
   - Primera pasada: calcular productos izquierdos
   - Segunda pasada: multiplicar por productos derechos

### 3. Coin Change Problem
**Problema**: Dados un conjunto de denominaciones de monedas y una cantidad, encuentra el mínimo número de monedas necesarias.

**Estrategia**:
1. Programación dinámica
2. dp[i] = mínimo número de monedas para hacer cantidad i
3. Para cada cantidad, probar todas las monedas posibles

## Problemas de Lógica

### 1. Torres de Hanoi
**Problema**: Mover n discos de una torre a otra siguiendo reglas específicas.

**Estrategia**:
1. Recursión natural
2. Mover n-1 discos a torre auxiliar
3. Mover disco más grande a destino
4. Mover n-1 discos de auxiliar a destino

### 2. N-Reinas
**Problema**: Colocar N reinas en un tablero N×N sin que se ataquen.

**Estrategia**:
1. Backtracking
2. Colocar reina fila por fila
3. Verificar conflictos con reinas ya colocadas
4. Si hay conflicto, retroceder y probar otra posición

## Ejercicios de Análisis

### 1. Complejidad Algorítmica
Dado un fragmento de código, determina su complejidad temporal y espacial.

### 2. Optimización
Dada una solución funcional, encuentra formas de mejorar su eficiencia.

### 3. Casos Extremos
Identifica y maneja casos límite en soluciones existentes.

## Consejos para Resolver Ejercicios

### Antes de Codificar
1. **Entiende completamente el problema**
   - Pide ejemplos si no los dan
   - Clarifica suposiciones
   - Identifica inputs/outputs

2. **Piensa en fuerza bruta primero**
   - Asegúrate de tener solución viable
   - Usa esto como base para optimizar

3. **Considera estructuras de datos**
   - ¿Necesitas búsqueda rápida? Hash table
   - ¿Necesitas orden? Heap
   - ¿Necesitas conexiones? Graph

### Durante la Implementación
1. **Escribe código limpio**
   - Nombres descriptivos
   - Funciones pequeñas
   - Comentarios útiles

2. **Prueba mientras programas**
   - Verifica partes individuales
   - Imprime valores intermedios si ayuda

3. **Maneja errores**
   - Inputs vacíos
   - Valores extremos
   - Tipos incorrectos

### Después de Codificar
1. **Prueba exhaustivamente**
   - Casos normales
   - Casos extremos
   - Inputs inválidos

2. **Analiza eficiencia**
   - Tiempo y espacio
   - Posibles mejoras
   - Trade-offs aceptables

3. **Refactoriza si necesario**
   - Mejora legibilidad
   - Elimina duplicados
   - Optimiza cuellos de botella

## Recursos Adicionales

- Plataforma: LeetCode.com
- Plataforma: HackerRank.com
- Plataforma: CodeWars.com
- Libro: "Cracking the Coding Interview"
- Sitio: ProjectEuler.net (problemas matemáticos)

---

*"La práctica constante con problemas variados es la llave para desarrollar una intuición sólida de resolución de problemas."*