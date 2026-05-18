# Laboratorio de programación concurrente y paralela en C++
## Estudiante
Nombre: Jesy Pricilla Rivera Duarte
Carné: C06512

## Descripción

Este laboratorio explora conceptos básicos de programación concurrente y paralela usando C++. Durante las distintas partes del laboratorio se implementaron ejercicios de:

- Creación y manejo de hilos
- Condiciones de carrera
- Uso de mutex
- Comparación entre ejecución secuencial y paralela
- Relación entre cantidad de hilos y rendimiento
- Deadlocks y su prevención

---

## Requisitos

- g++
- C++17 o superior
- MSYS2 UCRT64 (Windows)
- Visual Studio Code
- Sistema operativo Linux, macOS o Windows con soporte para compilación C++

---

# Compilación y ejecución

## Parte 1 — Creación de hilos

### Compilación

```bash
g++ -std=c++17 -Wall -Wextra -pthread src/parte1_threads.cpp -o parte1
```

### Ejecución

```bash
./parte1.exe
```

---

## Parte 2 — Race condition

### Compilación

```bash
g++ -std=c++17 -Wall -Wextra -pthread src/parte2_race_condition.cpp -o parte2
```

### Ejecución

```bash
./parte2.exe
```

---

## Parte 3 — Uso de mutex

### Compilación

```bash
g++ -std=c++17 -Wall -Wextra -pthread src/parte3_mutex.cpp -o parte3
```

### Ejecución

```bash
./parte3.exe
```

---

## Parte 4 — Benchmark secuencial vs paralelo

### Compilación

```bash
g++ -std=c++17 -O2 -Wall -Wextra -pthread src/parte4_benchmark.cpp -o parte4
```

### Ejecución

```bash
./parte4.exe
```

---

## Parte 5 — Hilos vs rendimiento

### Compilación

```bash
g++ -std=c++17 -O2 -Wall -Wextra -pthread src/parte5_hilos_vs_rendimiento.cpp -o parte5
```

### Ejecución

```bash
./parte5.exe
```

### Ver cantidad de núcleos

```bash
nproc
```

---

## Parte 6 — Deadlock

### Compilación

```bash
g++ -std=c++17 -Wall -Wextra -pthread src/parte6_deadlock.cpp -o parte6
```

### Ejecución

```bash
./parte6.exe
```

---

## Parte 6 corregida — Prevención de deadlock

### Compilación

```bash
g++ -std=c++17 -Wall -Wextra -pthread src/parte6_deadlock_corregido.cpp -o parte6_corregido
```

### Ejecución

```bash
./parte6_corregido.exe
```

---

# Resultados

Los resultados y respuestas de análisis del laboratorio se encuentran en:

```text
resultados/analisis.md
```

---

# Conclusiones

En este laboratorio se aprendió cómo funciona la programación concurrente y paralela en C++ utilizando hilos. A lo largo de las diferentes partes se pudo observar cómo varios hilos pueden ejecutar tareas al mismo tiempo y cómo esto puede mejorar el rendimiento de algunos programas.

También se comprendió el concepto de condición de carrera y cómo puede provocar resultados incorrectos cuando varios hilos modifican una misma variable compartida. Por medio del uso de mutex se logró solucionar este problema y asegurar resultados correctos en cada ejecución.

En las pruebas realizadas se observó que la versión paralela generalmente fue más rápida que la secuencial, especialmente cuando el trabajo se dividió adecuadamente entre varios hilos. También, se notó que aumentar demasiado la cantidad de hilos no siempre mejora el rendimiento causado por el costo adicional de administrar los hilos y realizar cambios de contexto.

Además, se logró entender el problema del deadlock, donde dos hilos quedan esperando recursos mutuamente y el programa deja de avanzar. La versión corregida permitió entender como `std::scoped_lock` ayuda a prevenir este tipo de bloqueos.

En general, el laboratorio permitió entender mejor los beneficios y desafíos de la programación concurrente y paralela, también la importancia de sincronizar correctamente el acceso a recursos compartidos.