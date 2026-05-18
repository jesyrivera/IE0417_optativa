# Parte 1 — Creación de hilos

## Resultados observados

### Ejecución 1

```text
Hola desde el hilo Hola desde el hilo 1
0
Hola desde el hilo Hola desde el hilo 42
Hola desde el hilo 3

Todos los hilos finalizaron.
```

### Ejecución 2

```text
Hola desde el hilo Hola desde el hilo 3Hola desde el hilo 1
Hola desde el hilo 2
Hola desde el hilo 40

Todos los hilos finalizaron.
```

### Ejecución 3

```text
Hola desde el hilo Hola desde el hilo 0Hola desde el hilo
Hola desde el hilo Hola desde el hilo 124
3

Todos los hilos finalizaron.
```

### Ejecución 4

```text
Hola desde el hilo Hola desde el hilo Hola desde el hilo Hola desde el hilo 12

Hola desde el hilo 30

4
Todos los hilos finalizaron.
```

### Ejecución 5

```text
Hola desde el hilo 0
Hola desde el hilo Hola desde el hilo Hola desde el hilo 42
Hola desde el hilo 1
3

Todos los hilos finalizaron.
```

## 1. ¿Los mensajes aparecen siempre en el mismo orden?

No, el orden cambia entre ejecuciones.

## 2. ¿Por qué podría cambiar el orden de impresión?

Porque los hilos se ejecutan concurrentemente y el sistema operativo decide cuándo ejecutarlos.

## 3. ¿Qué función cumple join()?

Hace que el hilo principal espere a que los otros hilos terminen.

## 4. ¿Qué podría pasar si no se llama a join()?

El programa podría terminar antes de que los hilos finalicen.

---

# Parte 2: condición de carrera

## Resultados obtenidos

| Ejecución | Valor esperado | Valor obtenido |
|---|---|---|
| 1 | 4000000 | 1715234 |
| 2 | 4000000 | 4000000 |
| 3 | 4000000 | 1547730 |
| 4 | 4000000 | 1107000 |
| 5 | 4000000 | 1881682 |


## 1. ¿El valor obtenido siempre coincide con el valor esperado?

No, en la mayoría de ejecuciones el valor fue incorrecto, de las 5 veces, solo uno fue correcto.

## 2. ¿Por qué se pierden incrementos?

Porque varios hilos modifican la variable compartida al mismo tiempo.

## 3. ¿La operación contador++ es realmente una sola operación a nivel de CPU?

No, internamente implica leer, modificar y escribir el valor.

## 4. ¿Qué problema de concurrencia se está observando?

Una condición de carrera.

---

# Parte 3: corrección usando mutex

## Resultados obtenidos

| Ejecución | Valor esperado | Valor obtenido |
|---|---|---|
| 1 | 4000000 | 4000000 |
| 2 | 4000000 | 4000000 |
| 3 | 4000000 | 4000000 |
| 4 | 4000000 | 4000000 |
| 5 | 4000000 | 4000000 |


## 1. ¿Qué cambió con respecto al programa anterior?

Ahora se usa un mutex para proteger la variable compartida.

## 2. ¿Qué hace std::mutex?

Permite que solo un hilo acceda a la sección crítica al mismo tiempo.

## 3. ¿Qué hace std::lock_guard?

Bloquea automáticamente el mutex al iniciar y lo libera al salir del bloque.

## 4. ¿Por qué ahora el resultado sí debería ser correcto?

Porque los hilos ya no modifican la variable simultáneamente.

## 5. ¿Qué desventaja podría tener proteger cada incremento individual con un mutex?

Puede reducir el rendimiento debido al costo de bloquear y desbloquear constantemente.

---

# Parte 4 - Benchmark de rendimiento

## Resultados obtenidos

| Ejecución | Tiempo secuencial | Tiempo paralelo | ¿Cuál fue más rápido? |
|---|---|---|---|
| 1 | 76 ms | 24 ms | Paralelo |
| 2 | 41 ms | 20 ms | Paralelo |
| 3 | 44 ms | 19 ms | Paralelo |
| 4 | 43 ms | 18 ms | Paralelo |
| 5 | 39 ms | 17 ms | Paralelo |

---

## 1. ¿El resultado secuencial y el paralelo son iguales?

Si, en todas las ejecuciones ambos resultados fueron 100000000.

## 2. ¿La versión paralela siempre fue más rápida?

Si, en todas las pruebas el tiempo paralelo fue menor que el secuencial.

## 3. ¿Por qué dividir el vector en bloques permite paralelizar el trabajo?

Porque cada hilo puede trabajar sobre una parte diferente del vector al mismo tiempo, aprovechando varios núcleos del procesador.

## 4. ¿Qué costos adicionales tiene la versión paralela?

La creación y administración de hilos, sincronización y comunicación entre ellos.

## 5. ¿Qué podría pasar si el vector fuera muy pequeño?

El costo de crear los hilos podría ser mayor que la mejora obtenida, haciendo que la versión paralela no sea conveniente.

---

# Parte 5 - Hilos vs Rendimiento

## Cantidad de núcleos detectados

Comando utilizado:

```bash
nproc
```

Resultado:

```bash
12
```

La computadora tiene 12 procesadores lógicos disponibles.

---

## Resultados obtenidos

| Cantidad de hilos | Tiempo obtenido |
|---|---|
| 1 | 56 ms |
| 2 | 37 ms |
| 4 | 25 ms |
| 8 | 16 ms |
| 16 | 18 ms |

| Cantidad de hilos | Tiempo obtenido |
|---|---|
| 1 | 44 ms |
| 2 | 22 ms |
| 4 | 18 ms |
| 8 | 15 ms |
| 16 | 14 ms |

| Cantidad de hilos | Tiempo obtenido |
|---|---|
| 1 | 40 ms |
| 2 | 25 ms |
| 4 | 19 ms |
| 8 | 13 ms |
| 16 | 12 ms |

| Cantidad de hilos | Tiempo obtenido |
|---|---|
| 1 | 48 ms |
| 2 | 24 ms |
| 4 | 22 ms |
| 8 | 13 ms |
| 16 | 13 ms |

| Cantidad de hilos | Tiempo obtenido |
|---|---|
| 1 | 47 ms |
| 2 | 25 ms |
| 4 | 19 ms |
| 8 | 13 ms |
| 16 | 13 ms |

---

## Conclusión

El rendimiento mejoró al aumentar la cantidad de hilos hasta cierto punto. La mejor mejora ocurrió entre 1 y 8 hilos, apartir de 16 hilos la diferencia fue pequeña, esto se debe a la sobrecarga de administrar demasiados hilos.

---

## Preguntas de análisis

### 1. ¿Cuál cantidad de hilos produjo el mejor tiempo?

Entre 8 y 16 hilos se obtuvieron los mejores tiempos, aproximadamente entre 12 y 13 ms.

### 2. ¿El tiempo mejoró siempre al aumentar los hilos?

No, después de cierto punto la mejora fue mínima.

### 3. ¿Cuántos núcleos tiene la computadora donde se ejecutó el programa?

El sistema reportó 12 procesadores lógicos.

### 4. ¿Qué ocurre cuando se usan más hilos que núcleos disponibles?

Los hilos deben turnarse para usar el procesador, aumentando la sobrecarga.

### 5. ¿Qué relación tiene esto con el context switching?

El sistema operativo debe cambiar constantemente entre hilos, lo cual consume tiempo adicional.

### 6. ¿Por qué la versión con 16 hilos podría no ser la mejor?

Porque administrar demasiados hilos puede generar más costos que beneficios.

---

# Parte 6 - Deadlock

## Ejecución del programa con deadlock

Salida obtenida:

```text
Hilo A intentando tomar recurso 1...
Hilo B intentando tomar recurso 2...

Hilo B intentando tomar recurso 1...
Hilo A intentando tomar recurso 2...
```

---

## Preguntas de análisis

### 1. ¿El programa termina normalmente?

No, el programa queda bloqueado indefinidamente.

### 2. ¿Qué recurso tomó primero el hilo A?

El recurso 1.

### 3. ¿Qué recurso tomó primero el hilo B?

El recurso 2.

### 4. ¿Por qué ninguno de los dos hilos puede continuar?

Porque cada hilo espera un recurso que está siendo utilizado por el otro hilo.

### 5. ¿Qué significa espera circular?

Que dos o más hilos esperan recursos entre sí formando un ciclo de espera.

### 6. ¿Cómo se podría evitar este problema?

Usando un orden consistente de bloqueo o utilizando mecanismos seguros como `std::scoped_lock`.

---

# Parte 6 corregida - Uso de std::scoped_lock

Salida obtenida:

```text
Hilo A obtuvo ambos recursos de forma segura.
Hilo B obtuvo ambos recursos de forma segura.
```

---

## Pregunta final

### Explique por qué `std::scoped_lock` ayuda a evitar este deadlock.

`std::scoped_lock` bloquea múltiples mutex de forma segura y evita la espera circular entre hilos. Además, libera automáticamente los recursos al salir del bloque de código.

---

# Parte 7 - Reflexión final

### 1. ¿Cuál fue la diferencia más clara que observó entre ejecución secuencial y ejecución con hilos?

La ejecución con hilos fue considerablemente más rápida al aprovechar varios núcleos del procesador.

### 2. ¿Qué es una condición de carrera?

Es un problema donde varios hilos modifican una misma variable al mismo tiempo sin sincronización.

### 3. ¿Por qué `contador++` puede fallar cuando muchos hilos lo ejecutan al mismo tiempo?

Porque la operación no es atómica y varios hilos pueden sobrescribir cambios entre sí.

### 4. ¿Qué problema resuelve un mutex?

Evita que varios hilos accedan simultáneamente a una sección crítica.

### 5. ¿Qué ventaja tiene `std::lock_guard` sobre llamar manualmente a `lock()` y `unlock()`?

Libera automáticamente el mutex y reduce errores de programación.

### 6. ¿Por qué más hilos no siempre significan mejor rendimiento?

Porque demasiados hilos generan sobrecarga y cambios constantes de contexto.

### 7. ¿Qué es un deadlock?

Es un bloqueo mutuo donde varios hilos esperan recursos entre sí indefinidamente.

### 8. ¿Qué buenas prácticas aplicaría al programar con hilos?

Usar mutex correctamente, evitar compartir datos innecesariamente y controlar el acceso a recursos compartidos.

### 9. ¿En qué tipo de programas reales podría ser útil la programación concurrente?

Servidores web, aplicaciones multitarea, videojuegos y sistemas operativos.

### 10. ¿En qué tipo de programas reales podría ser útil la programación paralela?

Procesamiento de imágenes, simulaciones científicas, inteligencia artificial y análisis de grandes volúmenes de datos.
