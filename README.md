# Solución para "Codify" - Hack The Box

Este repositorio contiene una detallada guía paso a paso sobre cómo resolví la máquina "Codify" en Hack The Box. Mi objetivo es proporcionar tanto a los entusiastas de la ciberseguridad como a los profesionales, una referencia útil y educativa que puedan seguir para entender y replicar el proceso de resolución.

## Contenido

- **Análisis Inicial**: Una descripción completa del análisis inicial que realicé para identificar los vectores de ataque posibles en "Codify".
- **Enumeración**: Detalles sobre las herramientas y técnicas que utilicé para la enumeración de servicios, puertos y vulnerabilidades.
- **Explotación**: Un paso a paso de cómo exploté las vulnerabilidades encontradas para ganar acceso inicial al sistema.
- **Escalada de Privilegios**: Explicación de cómo escalé privilegios para obtener un acceso más profundo al sistema, incluyendo cualquier técnica y herramienta utilizada.
- **Post-Explotación**: Una visión general de las acciones realizadas después de obtener el acceso deseado, como la recolección de banderas y la extracción de datos sensibles.
- **Conclusión y Aprendizaje**: Reflexiones sobre el desafío, qué aprendí durante el proceso y consejos para quienes intenten resolver "Codify".
- **Recursos y Herramientas**: Una lista de todas las herramientas, scripts y recursos externos que me fueron útiles durante la resolución de la máquina.

## Objetivo Educativo

El propósito principal de este repositorio es educativo. Busco compartir mi enfoque y las lecciones aprendidas con la comunidad para que otros puedan aprender de la experiencia y, potencialmente, aplicar estos conocimientos en sus propios desafíos de pentesting y ciberseguridad.

## Disclaimer

Este trabajo se realiza puramente con fines educativos. No fomento ni apruebo el acceso no autorizado a sistemas informáticos. Es crucial tener permiso explícito antes de intentar cualquier prueba de penetración o ataque a sistemas.

## Proceso de Resolución

### Análisis Inicial y Enumeración de Puertos

- Inicio de la máquina en Hack The Box.
- Ejecución de un escaneo `nmap` revelando 3 puertos abiertos: 22 (SSH), 8080 y 3000.
- El puerto 8080 no está disponible debido a una redirección.
- El puerto 3000 muestra una página web que permite la ejecución de código Node.js en un entorno sandbox.

### Explotación

- Navegación por la página web del puerto 3000 revela varias secciones: 'About us', 'Editor', 'Limitations', y una página de bienvenida.
- La sección 'Limitations' indica que los módulos `fs` y `child_process` están restringidos.
- En 'About us', se menciona la librería utilizada para el sandbox, la cual tiene vulnerabilidades conocidas según su repositorio de GitHub.
- Utilización de una vulnerabilidad específica de escape de sandbox ([Referencia de Gist](https://gist.github.com/arkark/e9f5cf5782dec8321095be3e52acf5ac)) para ejecutar código fuera del sandbox.

### Obtención de Shell Inverso

- Intentos de obtener un shell inverso mediante `netcat`, logrando finalmente acceso al shell de la máquina.

### Inicio de Escalada de Privilegios

- Búsqueda en los directorios de la aplicación web lleva al descubrimiento de una posible contraseña en forma de hash bcrypt.

## Herramientas y Técnicas Utilizadas

- `nmap` para la enumeración de puertos.
- Análisis manual de la aplicación web y sus funcionalidades.
- Explotación de vulnerabilidades conocidas en la librería de sandbox utilizada.
- `netcat` para obtener un shell inverso.
