# README.md

## Índice

1. [Parte 1: Verificación de instalación de Docker](parte1-verificacion.md)
2. [Parte 2: Primer contenedor](parte2-comandos-basicos.md)
3. [Parte 3: Imágenes y contenedor](parte3-imagenes-y-contenedores.md)
4. [Parte 4: administración básica de contenedores](parte3-imagenes-y-contenedores.md)
5. [Parte 5: crear una aplicación sencilla](parte4-dockerfile.md)
6. [Parte 6: construir una imagen con Dockerfile](parte4-dockerfile.md)
7. [Parte 7: publicación de puertos](parte5-puertos.md)
8. [Parte 8: logs e inspección de contenedores](parte5-puertos.md)
9. [Parte 9: variables de entorno](parte5-puertos.md)
10. [Parte 10: persistencia con volúmenes](parte6-volumenes.md)
11. [Parte 11: bind mounts](parte6-volumenes.md)
12. [Parte 12: redes de Docker](parte7-redes.md)
13. [Parte 13: ejemplo con aplicación y base de datos simulada](parte7-redes.md)
14. [Parte 14: limpieza del ambiente](parte8-limpieza.md)
15. Reflexión final 

---

## Reflexión final

1. **¿Qué es un contenedor?**  
Un contenedor es una forma de ejecutar una aplicación junto con todo lo que necesita para funcionar (librerías, dependencias y configuración) sin afectar el sistema operativo principal.

2. **¿Qué problema resuelve Docker?**  
Docker resuelve el problema de que una aplicación no siempre funciona igual en diferentes computadoras o sistemas. Muchas veces algo funciona en una máquina, pero falla en otra por diferencias de versiones, dependencias o configuración. Docker evita eso porque empaqueta la aplicación con todo lo que necesita para que se ejecute igual en cualquier lugar.

3. **¿Qué diferencia hay entre una imagen y un contenedor?**  
La imagen es como un molde o plantilla. El contenedor es cuando esa imagen ya está en ejecución y funcionando.

4. **¿Qué diferencia hay entre un contenedor y una máquina virtual?**  
Un contenedor comparte el sistema operativo del host y es más liviano. Una máquina virtual incluye su propio sistema operativo completo, por eso consume más recursos.

5. **¿Qué aprendió sobre puertos?**  
Los puertos sirven para comunicar el contenedor con el exterior. Por ejemplo, para acceder a una aplicación web desde el navegador.

6. **¿Qué aprendió sobre volúmenes?**  
Los volúmenes sirven para guardar información de forma permanente, aunque el contenedor se elimine.

7. **¿Qué aprendió sobre redes?**  
Las redes en Docker permiten que varios contenedores se comuniquen entre sí usando sus nombres, sin necesidad de usar direcciones IP.

8. **¿En qué casos usaría Docker en un proyecto de software?**  
Lo usaría cuando necesito que una aplicación funcione igual en diferentes computadoras o cuando un proyecto tiene varios servicios como base de datos, backend y frontend.

9. **¿Qué parte del laboratorio le pareció más útil?**  
La parte de redes y comunicación entre contenedores, porque permite ver cómo los servicios se conectan entre sí en un entorno real.

10. **¿Qué parte le pareció más confusa?**  
Al inicio, entender la diferencia entre imágenes, contenedores y redes puede ser un poco confuso, pero con la práctica se vuelve más claro.