# Parte 11: Fallo intencional en CI

## Cambio realizado para provocar el fallo

Se modificó temporalmente la prueba `AddPositiveNumbers` en el archivo `tests/test_calculator.cpp`.

Código original:

```cpp
EXPECT_EQ(add(2, 3), 5);
```

Código modificado:

```cpp
EXPECT_EQ(add(2, 3), 999);
```

El objetivo fue provocar una falla intencional para observar cómo Google Test y GitHub Actions detectan errores durante la ejecución de las pruebas.

---

## Resultado local

Después de recompilar y ejecutar las pruebas:

```bash
cd build
make
./run_tests
```

Google Test reportó una prueba fallida.

Salida relevante:

```text
[ RUN      ] CalculatorTest.AddPositiveNumbers

Failure
Expected equality of these values:
  add(2, 3)
    Which is: 5
  999

[  FAILED  ] CalculatorTest.AddPositiveNumbers
```

Resumen final:

```text
[==========] 41 tests from 3 test suites ran.
[  PASSED  ] 40 tests.
[  FAILED  ] 1 test.
```

---

## Análisis del error

La función `add(2,3)` devuelve correctamente el valor `5`.

Sin embargo, la prueba esperaba el valor `999`, por lo que Google Test detectó la discrepancia y marcó la prueba como fallida.

Información mostrada por Google Test:

* Valor esperado: `999`
* Valor obtenido: `5`
* Nombre de la prueba: `CalculatorTest.AddPositiveNumbers`
* Archivo: `tests/test_calculator.cpp`

Esto permitió identificar inmediatamente el origen del problema.

---

## Resultado en GitHub Actions

Después de realizar el commit:

```bash
git commit -m "Introduce fallo intencional en prueba"
git push
```

GitHub Actions ejecutó automáticamente el workflow definido en `.github/workflows/testing.yml`.

Debido a que una prueba falló, el job `build-and-test` fue marcado como fallido.

El workflow detuvo la ejecución en el paso:

```text
Run tests
```

y mostró el error correspondiente generado por Google Test.

---

## Corrección realizada

Se restauró la prueba a su estado correcto.

Código corregido:

```cpp
EXPECT_EQ(add(2, 3), 5);
```

Posteriormente se realizaron los comandos:

```bash
git add .
git commit -m "Corrige prueba fallida"
git push
```

---

## Resultado final

Después de corregir la prueba:

```bash
make
./run_tests
```

Todas las pruebas finalizaron exitosamente.

Resultado esperado:

```text
[==========] 41 tests from 3 test suites ran.
[  PASSED  ] 41 tests.
```

GitHub Actions volvió a ejecutar el workflow automáticamente y el estado del job cambió a exitoso.

---

## Evidencia de commits realizados

Commit que introdujo el fallo:

```text
f7bfc58 - Introduce fallo intencional en prueba
```

Commit que corrigió el fallo:

```text
a7b027a - Corrige prueba fallida
```

Estos commits permiten observar claramente cómo la integración continua detecta errores y verifica que la corrección restablece el funcionamiento correcto del proyecto.


## Preguntas de reflexión

### 1. ¿Por qué es útil ver una prueba fallar al menos una vez?

Porque permite comprender cómo las herramientas de testing reportan errores y qué información proporcionan para localizar la causa del problema.

### 2. ¿Qué diferencia hay entre una prueba fallando localmente y una prueba fallando en CI?

Una falla local solo afecta al desarrollador que ejecuta las pruebas. Una falla en CI es visible para todo el equipo y evita integrar cambios defectuosos al repositorio principal.

### 3. ¿Por qué no se debería dejar código con pruebas fallidas en la rama principal?

Porque indica que existe un comportamiento incorrecto o inconsistente en el software, lo que puede afectar a otros desarrolladores y generar errores en futuras versiones.

### 4. ¿Qué aporta CI a la calidad del software?

La integración continua verifica automáticamente que el código compile y que todas las pruebas pasen después de cada cambio, reduciendo la probabilidad de introducir errores en el proyecto.
