# Parte 12: Mini reto de testing

## Función implementada

Se agregó la función:

```cpp
bool is_valid_grade(int grade) {
    return grade >= 0 && grade <= 100;
}
```

Su propósito es verificar si una nota se encuentra dentro del rango válido de 0 a 100.

---

## Casos de prueba diseñados

### Caso normal válido

```cpp
TEST(GradeUtilsTest, ValidGradeNormalValue) {
    EXPECT_TRUE(is_valid_grade(85));
}
```

### Caso normal inválido

```cpp
TEST(GradeUtilsTest, InvalidGradeNormalValue) {
    EXPECT_FALSE(is_valid_grade(150));
}
```

### Borde inferior válido

```cpp
TEST(GradeUtilsTest, LowerBoundaryValid) {
    EXPECT_TRUE(is_valid_grade(0));
}
```

### Borde superior válido

```cpp
TEST(GradeUtilsTest, UpperBoundaryValid) {
    EXPECT_TRUE(is_valid_grade(100));
}
```

### Valor justo debajo del borde inferior

```cpp
TEST(GradeUtilsTest, BelowLowerBoundary) {
    EXPECT_FALSE(is_valid_grade(-1));
}
```

### Valor justo encima del borde superior

```cpp
TEST(GradeUtilsTest, AboveUpperBoundary) {
    EXPECT_FALSE(is_valid_grade(101));
}
```

---

## ¿Por qué se escogieron estos casos?

Los casos fueron seleccionados para cubrir:

* Valores válidos comunes.
* Valores inválidos comunes.
* Límites exactos aceptados por la función.
* Valores inmediatamente fuera del rango permitido.

De esta manera se verifica que la función se comporte correctamente tanto en situaciones normales como en casos borde.

---

## Resultado de las pruebas

Salida obtenida:

```bash
[==========] 47 tests from 3 test suites ran.
[  PASSED  ] 47 tests.
```

Todas las pruebas fueron ejecutadas exitosamente sin errores.

---

## GitHub

Los cambios fueron agregados al repositorio utilizando Git y posteriormente enviados a GitHub.

---

## GitHub Actions

Después de subir los cambios, GitHub Actions ejecutó automáticamente el workflow configurado en el laboratorio.

El workflow compiló el proyecto y ejecutó todas las pruebas satisfactoriamente.

---

# Respuestas Parte 12.6

## 1. ¿Cuál fue el caso más obvio de probar?

El caso más obvio fue verificar una nota válida común, por ejemplo 85, ya que se encuentra claramente dentro del rango permitido.

## 2. ¿Cuál fue el caso borde más importante?

Los valores 0 y 100, porque representan los límites exactos aceptados por la función.

## 3. ¿Qué error podría aparecer si no se prueban los valores 0 y 100?

La función podría rechazar incorrectamente alguno de los límites válidos debido a errores en los operadores de comparación.

## 4. ¿Qué diferencia hay entre probar un valor como 50 y probar valores como -1, 0, 100 y 101?

El valor 50 representa un caso normal dentro del rango permitido. Los valores -1, 0, 100 y 101 permiten verificar el comportamiento de la función en los límites y fuera de ellos.

## 5. ¿Qué aprendió sobre diseñar pruebas?

Aprendí que una buena estrategia de pruebas debe incluir casos normales, casos borde y casos inválidos para aumentar la confianza en el funcionamiento correcto del software.







# Reflexión final

## 1. ¿Qué es software testing?

Es el proceso de verificar y validar que un programa funciona correctamente y cumple los requisitos establecidos.

## 2. ¿Por qué el testing mejora la calidad del software?

Porque permite detectar errores tempranamente, verificar funcionalidades y prevenir regresiones.

## 3. ¿Cuál es la diferencia entre verificación y validación?

La verificación comprueba si el software fue construido correctamente. La validación verifica si el software satisface las necesidades del usuario.

## 4. ¿Qué es una prueba unitaria?

Es una prueba que evalúa una unidad pequeña de código, generalmente una función o método, de manera aislada.

## 5. ¿Qué es una prueba funcional?

Es una prueba que verifica que el sistema cumpla un requisito o comportamiento esperado desde la perspectiva del usuario.

## 6. ¿Qué diferencia hay entre EXPECT_ y ASSERT_?

EXPECT_ registra el error y continúa ejecutando la prueba. ASSERT_ detiene inmediatamente la ejecución de la prueba cuando falla.

## 7. ¿Por qué las pruebas deben ser deterministas?

Porque deben producir siempre el mismo resultado bajo las mismas condiciones para facilitar la detección y reproducción de errores.

## 8. ¿Por qué puede ser útil una semilla en pruebas con valores aleatorios?

Porque permite reproducir exactamente la misma secuencia de datos aleatorios en diferentes ejecuciones.

## 9. ¿Qué es cobertura de código?

Es una métrica que indica qué partes del código fueron ejecutadas por las pruebas.

## 10. ¿Por qué una cobertura alta no garantiza ausencia de errores?

Porque una línea puede ejecutarse sin que se validen correctamente todos sus comportamientos o resultados.

## 11. ¿Qué ventaja tiene ejecutar pruebas en GitHub Actions?

Permite verificar automáticamente que el proyecto sigue funcionando correctamente cada vez que se realizan cambios.

## 12. ¿Qué parte del laboratorio le pareció más útil?

La implementación de pruebas unitarias y la integración continua con GitHub Actions, ya que muestran prácticas utilizadas en proyectos reales.

## 13. ¿Qué parte le pareció más difícil?

La configuración inicial de CMake y GitHub Actions debido a la cantidad de archivos y configuraciones involucradas.

## 14. ¿Cómo aplicaría pruebas automatizadas en un proyecto futuro?

Implementaría pruebas unitarias desde las primeras etapas del desarrollo, configuraría integración continua y utilizaría cobertura de código para identificar áreas que necesitan más pruebas.

