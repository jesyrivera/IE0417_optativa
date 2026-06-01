# Parte 1: Preparación del proyecto

## ¿Qué es CMake?

CMake es una herramienta que ayuda a compilar proyectos de C++. Permite generar automáticamente los archivos necesarios para construir el programa sin tener que escribir manualmente todos los comandos de compilación.

## ¿Para qué sirve Google Test?

Google Test es una biblioteca que se utiliza para crear y ejecutar pruebas unitarias en C++. Permite verificar que las funciones del programa funcionen correctamente y facilita encontrar errores.

## ¿Qué significa automatizar pruebas?

Automatizar pruebas significa que las pruebas se ejecutan mediante un programa sin necesidad de revisar cada caso manualmente. Esto permite ahorrar tiempo y repetir las pruebas cuantas veces sea necesario.

## ¿Qué significa que las pruebas sean repetibles?

Significa que una prueba debe dar el mismo resultado cada vez que se ejecuta bajo las mismas condiciones. Esto ayuda a confiar en que los resultados son correctos.

## Archivos y carpetas creados

Se creó la estructura básica del proyecto:

```text
laboratorio-testing/
├── CMakeLists.txt
├── include/
├── src/
├── tests/
├── docs/
├── .github/workflows/
└── build/
```

## Resultado obtenido

Se logró crear correctamente la estructura del proyecto. También se configuró CMake para utilizar Google Test y preparar el entorno donde se desarrollarán las pruebas unitarias.

## ¿Qué aprendí?

Aprendí cómo organizar un proyecto de C++, cómo separar el código fuente de las pruebas y cómo utilizar CMake para facilitar la compilación del proyecto.

# Preguntas de reflexión

## 1. ¿Por qué conviene separar el código fuente de las pruebas?

Porque permite mantener el proyecto más ordenado y facilita el mantenimiento del código.

## 2. ¿Qué ventaja tiene usar CMake en un proyecto de C++?

Permite automatizar la compilación y manejar mejor proyectos con varios archivos.

## 3. ¿Por qué es útil que las pruebas se puedan ejecutar con un solo comando?

Porque ahorra tiempo y facilita verificar rápidamente si el programa sigue funcionando correctamente.

## 4. ¿Qué diferencia hay entre probar manualmente y probar automáticamente?

Las pruebas manuales requieren que una persona revise los resultados. Las pruebas automáticas verifican los resultados por sí mismas y muestran inmediatamente si existe algún error.








# Parte 9: Pruebas funcionales sencillas

## Casos funcionales

| ID | Requisito | Entrada | Resultado esperado | Tipo de caso |
|----|------------|----------|-------------------|--------------|
| TC-001 | Convertir nota excelente | 95 | A | Normal |
| TC-002 | Límite inferior de A | 90 | A | Borde |
| TC-003 | Límite superior de B | 89 | B | Borde |
| TC-004 | Nota inválida baja | -1 | Excepción | Inválido |
| TC-005 | Nota inválida alta | 101 | Excepción | Inválido |
| TC-006 | Nota aprobatoria mínima para C | 70 | C | Borde |
| TC-007 | Nota mínima válida | 0 | F | Borde |
| TC-008 | Nota máxima válida | 100 | A | Borde |

## Cobertura de los casos

Revisé el archivo `tests/test_grade_utils.cpp` y encontré que todos los casos anteriores ya estaban cubiertos por pruebas.

Pruebas relacionadas:

- `LetterGradeA` cubre TC-001.
- `GradeBoundaryBetweenBAndA` cubre TC-002 y TC-003.
- `NegativeGradeThrowsException` cubre TC-004.
- `InvalidGradeThrowsException` cubre TC-005.
- `GradeBoundaryBetweenDAndC` cubre TC-006.
- `MinimumValidGrade` cubre TC-007.
- `MaximumValidGrade` cubre TC-008.

No fue necesario agregar pruebas adicionales porque todos los casos funcionales definidos ya estaban contemplados.

## ¿Por qué estas pruebas son funcionales?

Estas pruebas son funcionales porque verifican que el sistema cumpla con los requisitos establecidos para la conversión de notas. En lugar de enfocarse en cómo está implementada la función internamente, se verifica que para una entrada determinada se obtenga el resultado esperado según las reglas del sistema.

## Reflexión

### 1. ¿Qué diferencia hay entre una prueba unitaria y una prueba funcional?

Una prueba unitaria verifica una función o componente específico de forma aislada. Una prueba funcional verifica que el sistema cumpla un requisito o comportamiento esperado.

### 2. ¿Por qué una prueba funcional se relaciona con requisitos?

Porque se diseña a partir de lo que el sistema debe hacer según las especificaciones y no a partir de la implementación interna.

### 3. ¿Qué significa pensar desde la perspectiva del usuario o del sistema?

Significa enfocarse en las entradas y resultados esperados, igual que lo haría una persona que utiliza el sistema, sin preocuparse por el código interno.

### 4. ¿Por qué la documentación de casos de prueba ayuda al equipo?

Porque permite entender qué se está verificando, facilita encontrar errores y ayuda a mantener las pruebas cuando el proyecto cambia.
