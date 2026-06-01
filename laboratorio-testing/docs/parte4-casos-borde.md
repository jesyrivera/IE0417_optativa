# Parte 6: Diseño de casos borde

## 6.1 Objetivo

Diseñar pruebas que permitan verificar no solamente el comportamiento normal del programa, sino también situaciones límite, valores extremos y casos especiales que podrían revelar errores ocultos.

## ¿Qué es un caso borde?

Es una situación de prueba que utiliza valores cercanos a los límites permitidos por una función o sistema. Estos casos son importantes porque muchos errores ocurren precisamente en los extremos de los rangos válidos o en situaciones poco comunes.

Estos casos borde ayudan a verificar que el software se comporte correctamente en condiciones especiales y no solo en escenarios normales.

## Archivos modificados

```text
tests/test_calculator.cpp
tests/test_string_utils.cpp
tests/test_grade_utils.cpp
```

## Casos borde que se agregaron a los archivos

### En test_calculator.cpp

```cpp
TEST(CalculatorTest, DivideNegativeNumbers) {
    EXPECT_EQ(divide(-10, -2), 5);
}

TEST(CalculatorTest, DividePositiveByNegative) {
    EXPECT_EQ(divide(10, -2), -5);
}

TEST(CalculatorTest, ZeroIsEven) {
    EXPECT_TRUE(is_even(0));
}
```

### En test_string_utils.cpp

```cpp
TEST(StringUtilsTest, EmptyStringToUppercase) {
    EXPECT_EQ(to_uppercase(""), "");
}

TEST(StringUtilsTest, EmptyStringIsPalindrome) {
    EXPECT_TRUE(is_palindrome(""));
}

TEST(StringUtilsTest, SingleLetterIsPalindrome) {
    EXPECT_TRUE(is_palindrome("a"));
}
```

### En test_grade_utils.cpp

```cpp
TEST(GradeUtilsTest, MinimumValidGrade) {
    EXPECT_EQ(letter_grade(0), 'F');
}

TEST(GradeUtilsTest, MaximumValidGrade) {
    EXPECT_EQ(letter_grade(100), 'A');
}

TEST(GradeUtilsTest, NegativeGradeThrowsException) {
    EXPECT_THROW(letter_grade(-1), std::invalid_argument);
}

TEST(GradeUtilsTest, GradeBoundaryBetweenFAndD) {
    EXPECT_EQ(letter_grade(59), 'F');
    EXPECT_EQ(letter_grade(60), 'D');
}

TEST(GradeUtilsTest, GradeBoundaryBetweenDAndC) {
    EXPECT_EQ(letter_grade(69), 'D');
    EXPECT_EQ(letter_grade(70), 'C');
}

TEST(GradeUtilsTest, GradeBoundaryBetweenCAndB) {
    EXPECT_EQ(letter_grade(79), 'C');
    EXPECT_EQ(letter_grade(80), 'B');
}

TEST(GradeUtilsTest, GradeBoundaryBetweenBAndA) {
    EXPECT_EQ(letter_grade(89), 'B');
    EXPECT_EQ(letter_grade(90), 'A');
}
```

## ¿Por qué estos casos son importantes?

- Porque verifican el comportamiento con valores extremos como `0` y `100`.
- Comprueban que las divisiones con números negativos den resultados correctos.
- Validan que una cadena vacía sea manejada correctamente
- Se encargan de verificar que una única letra sea considerada un palíndromo.
- Comprueban que el sistema rechace valores inválidos como notas negativas.
- Validan los límites exactos donde cambia la calificación de una letra a otra.

Estos escenarios son propensos a errores de programación y suelen revelar problemas que no aparecen en pruebas con valores normales.

## Comandos ejecutados

```bash
cd build
make
./run_tests
```

## Resultado obtenido

El proyecto se compiló correctamente y todas las pruebas fueron ejecutadas sin errores.

```text
[==========] Running 40 tests from 3 test suites.
[==========] 40 tests from 3 test suites ran. (1 ms total)
[  PASSED  ] 40 tests.
```

### Resultados por módulo

#### CalculatorTest

```text
13 pruebas ejecutadas.
13 pruebas aprobadas.
```

#### StringUtilsTest

```text
10 pruebas ejecutadas.
10 pruebas aprobadas.
```

#### GradeUtilsTest

```text
17 pruebas ejecutadas.
17 pruebas aprobadas.
```

## ¿Alguna prueba falló?

Todas las pruebas pasaron correctamente en la primera ejecución. No fue necesario realizar correcciones adicionales en el código fuente.

## Aprendizaje obtenido

Se aprendió la importancia de diseñar pruebas que cubran situaciones límite y valores extremos. También se comprobó que una buena suite de pruebas no debe enfocarse únicamente en casos normales, sino incluir escenarios especiales que ayuden a detectar errores ocultos antes de que lleguen a producción.

## Preguntas de reflexión

### 1. ¿Por qué no basta con probar casos normales?

Porque muchos errores aparecen en situaciones especiales o límites que no suelen presentarse en los casos comunes. Probar únicamente escenarios normales puede dejar defectos importantes sin detectar.

### 2. ¿Qué es un caso borde?

Es una prueba que utiliza valores cercanos a los límites permitidos por una función o sistema para verificar que el comportamiento siga siendo correcto en esas condiciones.

### 3. ¿Qué es un caso inválido?

Es una prueba que utiliza datos fuera de los rangos permitidos o condiciones incorrectas para verificar que el sistema maneje adecuadamente los errores y excepciones.

### 4. ¿Qué diferencia hay entre probar 85 y probar exactamente 80, 90 o 70?

El valor 85 se encuentra dentro de un rango ya establecido y normalmente no genera problemas. Los valores 80, 90 y 70 representan límites donde cambia la calificación asignada, por lo que son mucho más importantes para detectar errores en las condiciones de decisión.

### 5. ¿Cómo puede un caso borde revelar errores ocultos?

Porque obliga al programa a manejar situaciones extremas o límites exactos donde suelen ocurrir errores de comparación, validación o lógica. Estos errores muchas veces no son visibles cuando se prueban únicamente valores intermedios.







# Parte 7:  Semillas en pruebas

## Objetivo

Comprender cómo el uso de semillas permite controlar la generación de valores aleatorios para que las pruebas sean reproducibles y consistentes.

### Código agregado

Se agregó la biblioteca para generación de números aleatorios:

```cpp
#include <random>
```

Y se implementó la siguiente prueba:

```cpp
TEST(CalculatorTest, RandomAdditionsWithFixedSeed) {
    std::mt19937 generator(12345);
    std::uniform_int_distribution<int> distribution(-100, 100);

    for (int i = 0; i < 10; i++) {
        int a = distribution(generator);
        int b = distribution(generator);

        EXPECT_EQ(add(a, b), a + b);
    }
}
```

### ¿Qué hace la semilla?

La semilla es un valor inicial utilizado por el generador de números aleatorios para producir una secuencia de números aparentemente aleatoria.

En esta prueba se utilizó:

```cpp
std::mt19937 generator(12345);
```

La semilla `12345` garantiza que la misma secuencia de números se genere cada vez que la prueba se ejecuta.

### ¿Por qué se usa una semilla fija?

Se utiliza una semilla fija para asegurar que las pruebas sean deterministas y reproducibles.

Esto hace que:

- Los mismos datos se generan en cada ejecución.
- Los resultados de la prueba son consistentes.
- Los errores pueden reproducirse fácilment.
- El comportamiento es idéntico en diferentes computadoras y momentos de ejecución.

### Comandos ejecutados

```bash
cd build
make
./run_tests
```

### Resultado con la semilla 12345

La nueva prueba fue ejecutada correctamente.

```text
[ RUN      ] CalculatorTest.RandomAdditionsWithFixedSeed
[       OK ] CalculatorTest.RandomAdditionsWithFixedSeed (0 ms)
```

y

```text
[==========] 41 tests from 3 test suites ran.
[  PASSED  ] 41 tests.
```

### Cambio temporal de semilla

Se modificó temporalmente la semilla a:

```cpp
std::mt19937 generator(54321);
```

Luego, se recompiló el proyecto y se ejecutaron nuevamente las pruebas.

Resultado:

```text
[==========] 41 tests from 3 test suites ran.
[  PASSED  ] 41 tests.
```

### ¿Qué pasó al cambiar la semilla?

Al utilizar la semilla `54321`, el generador produjo una secuencia diferente de números aleatorios.

Sin embargo, todas las pruebas continuaron pasando porque la función `add()` implementa correctamente la suma de enteros para cualquier combinación de valores generados.

La diferencia principal fue que los números utilizados internamente por la prueba cambiaron, aunque el resultado final siguió siendo correcto.

### ¿Por qué esto ayuda en debugging?

Si una prueba falla usando una semilla específica, se puede registrar dicha semilla y volver a ejecutarla luego.

Entonces:

- Se reproducen exactamente los mismos datos de entrada.
- El error puede investigarse paso a paso.
- Se facilita la depuración.
- Otros desarrolladores pueden reproducir el problema en sus equipos.

### Aprendizaje

Se aprendió que las pruebas que utilizan números aleatorios deben ser controladas mediante semillas fijas para garantizar resultados reproducibles. También se observó que cambiar la semilla modifica los datos generados, pero mantiene la capacidad de repetir exactamente la misma secuencia cuando se utiliza nuevamente la misma semilla.

## Preguntas de reflexión

### 1. ¿Por qué las pruebas con datos aleatorios pueden ser peligrosas si no se controlan?

Porque podrían producir resultados diferentes en cada ejecución. Esto dificulta reproducir errores y puede generar comportamientos inconsistentes durante el proceso de validación.

### 2. ¿Qué ventaja tiene usar una semilla fija?

Permite generar siempre la misma secuencia de datos aleatorios, haciendo que las pruebas sean deterministas y reproducibles.

### 3. ¿Cómo ayuda la semilla a reproducir errores?

Si una prueba falla con una semilla determinada, basta con reutilizar esa misma semilla para generar exactamente los mismos datos y reproducir el problema.

### 4. ¿Por qué es importante documentar la semilla usada?

Porque permite que otros desarrolladores puedan ejecutar la prueba bajo las mismas condiciones y obtener exactamente los mismos resultados, facilitando la depuración y el mantenimiento del software.
