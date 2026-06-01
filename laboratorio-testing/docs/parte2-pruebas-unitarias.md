# Parte 2: Implementación inicial del código

## Módulos creados

Se crearon tres módulos:

### calculator

Contiene funciones matemáticas básicas:

* add()
* subtract()
* multiply()
* divide()
* is_even()

### string_utils

Contiene funciones para trabajar con cadenas de texto:

* to_uppercase()
* is_palindrome()
* count_vowels()

### grade_utils

Contiene funciones relacionadas con notas:

* average()
* is_passing()
* letter_grade()

## Función de los archivos .h

Los archivos de encabezado (.h) contienen las declaraciones de las funciones que se utilizarán en otras partes del programa. Entonces:

* calculator.h: declara las operaciones matemáticas
* string_utils.h: declara funciones para manipular texto.
* grade_utils.h: declara funciones para trabajar con notas.

## Función de los archivos .cpp

Estos archivos contienen la implementación de las funciones declaradas en los archivos .h, de la siguiente manera:

* calculator.cpp: implementa las operaciones matemáticas
* string_utils.cpp: implementa las funciones de cadenas
* grade_utils.cpp: implementa las funciones relacionadas con notas

## Funciones que parecen tener casos normales, borde e inválidos

### Casos normales

* add(2,3)
* multiply(3,4)
* average({80,90,100})
* letter_grade(85)

### Casos borde

* is_passing(70)
* is_passing(69)
* letter_grade(90)
* letter_grade(80)

### Casos inválidos

* divide(10,0)
* average({})
* letter_grade(120)

## Archivos creados y modificados

```text
include/calculator.h
src/calculator.cpp

include/string_utils.h
src/string_utils.cpp

include/grade_utils.h
src/grade_utils.cpp
```

## Resultado obtenido

Se implementaron correctamente los tres módulos solicitados. Todas las funciones compilaron sin errores y quedaron listas para ser probadas mediante Google Test.

## ¿Qué aprendí?

Aprendí la diferencia entre archivos .h y .cpp, cómo organizar mejor el código y cómo identificar posibles casos de prueba antes de ejecutar el programa.






# Parte 3: Primeras pruebas unitarias con Google Test

En esta tercera parte se crearon pruebas unitarias para las funciones de los módulos calculator, string_utils y grade_utils utilizando Google Test.

## Archivos creados y modificados

```text
tests/test_calculator.cpp
tests/test_string_utils.cpp
tests/test_grade_utils.cpp
```

## Comandos ejecutados

### Configuración del proyecto

```bash
cmake ..
```

### Compilación

```bash
make
```

### Ejecución de pruebas

```bash
./run_tests
```

### Ejecución con CTest

```bash
ctest --output-on-failure
```

## Resultado obtenido

Al principio apareció el siguiente error:

```bash
make: *** No targets specified and no makefile found. Stop.
```

Esto ocurrió porque el directorio build ya existía, pero todavía no se había ejecutado CMake.

La solución fue ejecutar:

```bash
cmake ..
```

Después de eso, el comando make funcionó correctamente y el proyecto compiló sin problemas.

## Resultado de ./run_tests

```text
[==========] Running 25 tests from 3 test suites.
[==========] 25 tests from 3 test suites ran.
[  PASSED  ] 25 tests.
```

## Resultado de ctest --output-on-failure

```text
100% tests passed, 0 tests failed out of 25
```

## Cantidad de pruebas ejecutadas

* Total de pruebas: 25
* Pruebas exitosas: 25
* Pruebas fallidas: 0

## Explicación de algunas pruebas

### AddPositiveNumbers

```cpp
EXPECT_EQ(add(2,3),5);
```

Esta prueba verifica que la función de suma retorne el resultado correcto.

### DivideByZeroThrowsException

```cpp
EXPECT_THROW(divide(10,0), std::invalid_argument);
```

Verifica que se lance una excepción cuando se intenta dividir entre cero.

### DetectPalindromeWithSpaces

```cpp
EXPECT_TRUE(is_palindrome("anita lava la tina"));
```

Comprueba que la función detecte correctamente un palíndromo con espacios.

### AverageEmptyVectorThrowsException

```cpp
EXPECT_THROW(average(grades), std::invalid_argument);
```

Esta prueba lo que hace es verificar que no se pueda calcular el promedio de un vector vacío.

### InvalidGradeThrowsException

```cpp
EXPECT_THROW(letter_grade(120), std::invalid_argument);
```

Verifica que una nota fuera del rango permitido genere una excepción.

## ¿Qué aprendí?

Aprendí a utilizar Google Test para crear pruebas unitarias, verificar resultados esperados y comprobar que las funciones respondan correctamente tanto en casos normales como en situaciones de error.

# Preguntas de reflexión

## 1. ¿Qué significa que una prueba pase?

Significa que el resultado obtenido fue el esperado.

## 2. ¿Qué significa que una prueba falle?

Significa que el resultado obtenido fue diferente al esperado y puede indicar un error en el código.

## 3. ¿Qué diferencia hay entre probar una función manualmente y probarla con Google Test?

Con Google Test la verificación es automática y mucho más rápida. Manualmente habría que revisar cada resultado uno por uno.

## 4. ¿Por qué las pruebas unitarias deben ser rápidas?

Porque se ejecutan muchas veces durante el desarrollo y no deben retrasar el trabajo.

## 5. ¿Por qué las pruebas unitarias deben ser deterministas?

Porque deben producir siempre el mismo resultado cuando se ejecutan bajo las mismas condiciones.







# Parte 4: EXPECT vs ASSERT

## 4.1 Objetivo

Comprender la diferencia entre las verificaciones `EXPECT_` y `ASSERT_` en Google Test.

`EXPECT_` permite que la prueba continúe ejecutándose aunque una verificación falle, mientras que `ASSERT_` detiene inmediatamente la ejecución de la prueba cuando la condición evaluada no se cumple. Esto es especialmente útil cuando una falla inicial invalida el resto de las comprobaciones.

## Código agregado

### Prueba utilizando EXPECT

```cpp
TEST(CalculatorTest, MultipleExpectChecks) {
    EXPECT_EQ(add(1, 1), 2);
    EXPECT_EQ(add(2, 2), 4);
    EXPECT_EQ(add(3, 3), 6);
}
```

### Prueba utilizando ASSERT

```cpp
TEST(CalculatorTest, AssertBeforeDivision) {
    int divisor = 2;

    ASSERT_NE(divisor, 0);

    EXPECT_EQ(divide(10, divisor), 5);
}
```

## Comandos ejecutados

```bash
cd build
make
./run_tests
```

## Resultados obtenidos

### Caso 1: divisor = 2

Al ejecutar las pruebas con `divisor = 2`, la condición `ASSERT_NE(divisor, 0)` se cumplió correctamente porque el divisor era diferente de cero. La prueba continuó ejecutándose y verificó que `divide(10, divisor)` retornara `5`.

Resultado:

```text
[ RUN      ] CalculatorTest.AssertBeforeDivision
[       OK ] CalculatorTest.AssertBeforeDivision (0 ms)
```

Además, todas las pruebas del proyecto fueron exitosas:

```text
[==========] 27 tests from 3 test suites ran.
[  PASSED  ] 27 tests.
```

### Caso 2: divisor = 0

Se modificó temporalmente la prueba:

```cpp
TEST(CalculatorTest, AssertBeforeDivision) {
    int divisor = 0;

    ASSERT_NE(divisor, 0);

    EXPECT_EQ(divide(10, divisor), 5);
}
```

Al ejecutar de nuevo las pruebas luego de modificar, la condición `ASSERT_NE(divisor, 0)` falló porque el divisor era igual a cero.

Resultado:

```text
[ RUN      ] CalculatorTest.AssertBeforeDivision
Failure
Expected: (divisor) != (0), actual: 0 vs 0
[  FAILED  ] CalculatorTest.AssertBeforeDivision
```

Resumen final:

```text
[==========] 27 tests from 3 test suites ran.
[  PASSED  ] 26 tests.
[  FAILED  ] 1 test.

[  FAILED  ] CalculatorTest.AssertBeforeDivision
```

## Documentación

### ¿Qué pasó cuando divisor era 2?

La condición `ASSERT_NE(divisor, 0)` fue verdadera, entonces la prueba continuó ejecutándose normalmente. Luego se verificó correctamente que el resultado de la división fuera igual a 5 y la prueba paso.

### ¿Qué pasó cuando divisor era 0?

La condición `ASSERT_NE(divisor, 0)` falló porque el divisor era igual a cero. Google Test marcó inmediatamente la prueba como fallida y detuvo su ejecución antes de llegar a la instrucción de división.

### ¿Por qué ASSERT_NE detuvo la prueba?

Porque `ASSERT_` genera fallos fatales. Cuando una condición evaluada mediante `ASSERT_` falla, Google Test interrumpe inmediatamente la ejecución de esa prueba para evitar ejecutar código que puede depender de una condición inválida.

### Diferencia entre EXPECT_ y ASSERT_

La principal diferencia es que `EXPECT_` permite que la prueba continúe aunque una verificación falle, mientras que `ASSERT_` detiene la ejecución de la prueba en el momento en que ocurre el fallo. De esta manera,

`EXPECT_` se utiliza cuando se quiere comprobar varias condiciones y seguir evaluando las demás aunque una falle.

`ASSERT_` se utiliza cuando una condición es indispensable para continuar con la prueba de forma segura.



## Aprendizaje obtenido

Se comprendió la diferencia entre fallos fatales y no fatales en Google Test. También se observó cómo `ASSERT_` protege la ejecución de una prueba evitando que continúe cuando una condición esencial no se cumple.

## Preguntas de reflexión

### 1. ¿Cuándo conviene usar EXPECT_?

Cuando se desea verificar varias condiciones independientes dentro de una misma prueba y se quiere obtener información sobre todos los errores encontrados en una sola ejecución.

### 2. ¿Cuándo conviene usar ASSERT_?

Cuando una condición es indispensable para continuar la prueba, por ejemplo, validar que un puntero no sea nulo, que un archivo se haya abierto correctamente o que un divisor sea diferente de cero.

### 3. ¿Qué podría pasar si se usa EXPECT_ cuando en realidad se necesitaba detener la prueba?

La prueba podría continuar ejecutándose con datos inválidos, provocando errores adicionales, resultados incorrectos o incluso fallos inesperados durante la ejecución.

### 4. ¿Qué podría pasar si se usa ASSERT_ en exceso?

Las pruebas podrían detenerse demasiado pronto, impidiendo detectar otros errores presentes en la misma ejecución y reduciendo la cantidad de información útil obtenida durante el proceso de depuración.
