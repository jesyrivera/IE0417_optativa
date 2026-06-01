# Parte 5: Pruebas fallidas y corrección de errores

## 5.1 Objetivo

Observar cómo una prueba automatizada ayuda a encontrar errores en el código mediante la detección inmediata de comportamientos incorrectos después de realizar modificaciones.

## Cambio realizado en el archivo

Se modificó la función `is_even` en el archivo `src/calculator.cpp`:

```cpp
bool is_even(int number) {
    return number % 2 == 1;
}
```

Antes era un 0 en luegar del 1. Esta modificación es incorrecta porque devuelve `true` para números impares y `false` para números pares.

## Archivo modificado

```text
src/calculator.cpp
```

## Comandos ejecutados

```bash
cd build
make
./run_tests
```

## Resultado obtenido

Al ejecutar las pruebas, Google Test detectó errores en las pruebas relacionadas con la función `is_even`.

### Pruebas que fallaron

```text
CalculatorTest.DetectEvenNumber
CalculatorTest.DetectOddNumber
```

### Mensajes de error mostrados por Google Test


```text
[ RUN      ] CalculatorTest.DetectEvenNumber
Failure
Value of: is_even(8)
  Actual: false
Expected: true
[  FAILED  ] CalculatorTest.DetectEvenNumber
```

y 

```text
[ RUN      ] CalculatorTest.DetectOddNumber
Failure
Value of: is_even(7)
  Actual: true
Expected: false
[  FAILED  ] CalculatorTest.DetectOddNumber
```

### ¿Qué esperaba la prueba?

Para el caso del número 8:

```cpp
EXPECT_TRUE(is_even(8));
```

La prueba esperaba que la función retornara:

```cpp
true
```

porque 8 es un número par.

Para el caso del número 7:

```cpp
EXPECT_FALSE(is_even(7));
```

La prueba esperaba que la función retornara:

```cpp
false
```

porque 7 es un número impar.

### ¿Qué obtuvo realmente?

La función modificada devolvió:

```cpp
is_even(8) -> false
is_even(7) -> true
```

Esto ocurrió porque la condición:

```cpp
number % 2 == 1
```

identifica números impares en lugar de números pares.

## Corrección realizada

Se restauró la implementación correcta de la función:

```cpp
bool is_even(int number) {
    return number % 2 == 0;
}
```

Esta condición devuelve `true` cuando el residuo de dividir entre 2 es cero, lo que corresponde a un número par.

## Resultado final

Después de corregir la función, se recompiló el proyecto y se ejecutaron nuevamente las pruebas.

Resultado esperado:

```text
[==========] 27 tests from 3 test suites ran.
[  PASSED  ] 27 tests.
```

Todas las pruebas volvieron a ejecutarse correctamente sin errores.

## Aprendizaje obtenido

Se comprobó que las pruebas automatizadas permiten detectar rápidamente errores introducidos en el código. También se observó cómo Google Test proporciona información detallada sobre qué prueba falló, qué valor se esperaba y cuál fue el valor obtenido, facilitando la localización y corrección del problema.

## Preguntas de reflexión

### 1. ¿Cómo ayudó Google Test a identificar el error?

Google Test señaló exactamente cuáles pruebas fallaron y mostró los valores esperados y obtenidos. Esto permitió identificar rápidamente que el problema estaba en la función `is_even`.

### 2. ¿Qué información útil muestra una prueba fallida?

Muestra el nombre de la prueba que falló, la ubicación del error, la condición evaluada, el valor esperado y el valor realmente obtenido durante la ejecución.

### 3. ¿Por qué es importante ejecutar pruebas después de modificar código?

Porque cualquier cambio puede introducir errores inesperados. Ejecutar las pruebas permite verificar que las funcionalidades existentes continúan funcionando correctamente.

### 4. ¿Qué riesgo existe si se cambia código y no se ejecutan las pruebas?

Podrían introducirse errores en el sistema sin ser detectados, afectando funcionalidades que anteriormente funcionaban correctamente y generando fallos en etapas posteriores del desarrollo o producción.
