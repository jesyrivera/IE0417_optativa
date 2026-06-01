# Parte 8: Cobertura de código

## ¿Qué es la cobertura de código?

La cobertura de código es una métrica que permite ver qué partes del programa fueron ejecutadas durante las pruebas. Esto ayuda a identificar funciones o líneas que no han sido probadas.


## Qué se hizo?

Primero se limpiaba la carpeta de compilación y volví a generar el proyecto con cobertura habilitada.

### Comandos utilizados

```bash
rm -rf build
mkdir build
cd build

cmake -DENABLE_COVERAGE=ON ..
make

./run_tests
```


## Resultado obtenido

Las pruebas se ejecutaron correctamente.

```bash
[==========] Running 41 tests from 3 test suites.
[  PASSED  ] 41 tests.
```

Se ejecutaron 41 pruebas y todas pasaron.

## Problema encontrado

Al intentar generar el reporte de cobertura con LCOV apareció un error relacionado con archivos de prueba:

```bash
lcov: ERROR: (inconsistent) mismatched end line ...
```

Por esta razón no se pudo generar el archivo `coverage.info`.


## Cómo lo corregí?

Ejecuté nuevamente LCOV ignorando las inconsistencias:

```bash
lcov --capture \
     --directory . \
     --output-file coverage.info \
     --ignore-errors inconsistent
```

Después filtré los archivos del sistema, Google Test y las pruebas:

```bash
lcov --remove coverage.info '/usr/*' '*/_deps/*' '*/tests/*' \
     --output-file coverage_filtered.info
```

Finalmente generé el reporte HTML:

```bash
genhtml coverage_filtered.info \
        --output-directory coverage_report
```

## Cobertura obtenida

El reporte mostró:

```text
Lines: 100.0% (54 de 54)
Functions: 100.0% (11 de 11)
```

## Archivos con mayor cobertura

* src/calculator.cpp
* src/string_utils.cpp
* src/grade_utils.cpp

Todos alcanzaron 100% de cobertura.


## Archivos con menor cobertura

No hubo archivos con cobertura menor al 100%.


## Líneas o ramas no cubiertas

No se encontraron líneas sin ejecutar en los archivos fuente del proyecto.


## Evidencia

El reporte HTML generado por LCOV mostró:

```text
Coverage: 100.0%
Lines: 54 / 54
Functions: 11 / 11
```

## Pruebas adicionales que podrían agregarse

### Prueba 1

Verificar cadenas con símbolos y números:

```cpp
EXPECT_EQ(toUpper("hola123!"), "HOLA123!");
```

### Prueba 2

Verificar promedio con valores extremos:

```cpp
std::vector<double> grades = {0, 100};
EXPECT_DOUBLE_EQ(calculateAverage(grades), 50);
```

# Preguntas de reflexión

## 1. ¿Qué significa tener 100% de cobertura?

Significa que todas las líneas y funciones del programa fueron ejecutadas al menos una vez durante las pruebas.

## 2. ¿Tener 100% de cobertura garantiza que el programa no tiene errores?

No, la cobertura solo indica que el código fue ejecutado pero no garantiza que todo funcione perfectamente.

## 3. ¿Qué diferencia hay entre cobertura de líneas y cobertura de ramas?

La cobertura de líneas mide qué líneas fueron ejecutadas. La cobertura de ramas verifica que todas las posibles decisiones del programa fueron probadas.

## 4. ¿Por qué una línea ejecutada no necesariamente significa que fue bien probada?

Porque una línea puede ejecutarse sin verificar si el resultado obtenido es correcto.

## 5. ¿Cómo puede ayudar la cobertura a mejorar las pruebas?

Ayuda a encontrar partes del código que no han sido probadas y permite crear nuevas pruebas para cubrirlas.
