markdown
# 🧩 Generador Abstracto de Agentes (Humo Desenmascarado)

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)](#)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)](#)
[![Sin Dependencias](https://img.shields.io/badge/Dependencias-0%20(vanilla)-green)](#)

**Demuestra que los "agentes IA" modernos son, en esencia, un conjunto de reglas configurables + una plantilla de texto. Sin magia, sin backend, sin humo.**

Crea tu propio agente (recomendador de recetas, generador de excusas, asesor de viajes...) en segundos respondiendo a 7 preguntas abstractas.

---

## 📖 Filosofía

> *"Un agente es un prompt bien ejecutado, que venden que es la leche pero no dejan de ser loops y eso se puede hacer con prompts bien ejecutados, que son humo."*

Este proyecto nace de una conversación sobre la verdadera naturaleza de los "Agentes IA" que inundan el marketing tecnológico. Queríamos demostrar que con un simple formulario de configuración, un `filter()` de JavaScript y una plantilla de texto, se puede replicar el 80% de la funcionalidad de muchos agentes comerciales.

**No es magia, es abstracción.**

---

## ✨ Características

- **100% configurable**: Todas las preguntas, opciones y la plantilla de respuesta son editables en tiempo real.
- **Sin backend**: Funciona completamente en el navegador con HTML, CSS y JavaScript vainilla.
- **Tres demos incluidas**: Recetas, excusas laborales y películas para jugar.
- **Modo "Búsqueda en Google"**: Sustituye una API costosa por una simple búsqueda web basada en las selecciones del usuario.
- **Vista previa en vivo**: El agente generado se actualiza al instante al modificar la configuración.
- **Persistencia local**: La configuración se guarda en `localStorage` para no perder tu trabajo.
- **Diseño responsive**: Funciona en móvil y escritorio.

---

## 🧠 ¿Cómo funciona?

El generador sigue una arquitectura **data-driven**:

1. **Creador**: Rellenas un formulario con las **7 dimensiones abstractas**:
   - Objetivo, Perfil, Restricciones, Recurso limitante, Contexto, Estilo de comunicación, Memoria/Acciones.
2. **Motor genérico**: Traduce esa configuración en:
   - Un formulario dinámico para el usuario final.
   - Reglas de filtrado sobre un dataset de ejemplo (o una consulta a Google).
   - Una plantilla de respuesta que se rellena con los datos seleccionados.
3. **Usuario final**: Interactúa con el agente generado, obtiene una recomendación personalizada y, si se configuró, un enlace para ampliar información.

El "agente" resultante es simplemente un **motor de reglas + un prompt con esteroides**.

---

## 🚀 Cómo usarlo

### Opción 1: Probar online (GitHub Pages)
*Próximamente: enlace a la demo desplegada.*

### Opción 2: Ejecutar en local
1. Clona este repositorio:
   ```bash
   git clone https://github.com/tu-usuario/generador-abstracto-agentes.git
Abre el archivo index.html en tu navegador favorito.

¡A crear agentes!

Modo Creador (parte superior)
Modifica el nombre, propósito y fuente de datos.

Cambia las preguntas y opciones de cada dimensión a tu gusto.

Pulsa "Aplicar configuración" para ver los cambios en la vista previa.

Modo Usuario (parte inferior)
Rellena el formulario generado con tus preferencias.

Pulsa "Ejecutar Agente".

Observa el resultado y, si está activado, el enlace externo.

Ejemplos rápidos
Recetas: Objetivo "Perder peso", restricción "Sin lactosa", tiempo 15 min.

Excusas: Objetivo "Salud", perfil "Quemado", recurso 5 min.

Búsqueda Google: Configura cualquier dimensión y el agente abrirá una pestaña con los resultados de búsqueda.

📁 Estructura del proyecto
text
.
├── index.html          # Único archivo necesario. Contiene HTML, CSS y JS.
├── LICENSE             # Texto completo de la GPLv3.
└── README.md           # Este archivo.
No hay dependencias externas. Todo el código está autocontenido.

🛠️ Tecnologías
HTML5 semántico.

CSS3 con Flexbox y diseño responsive.

JavaScript (ES6) puro, usando principios de programación funcional e inmutabilidad.

localStorage para persistencia.

⚖️ Licencia GPLv3
Este proyecto está licenciado bajo la GNU General Public License v3.0 (GPLv3).

¿Qué significa esto?
La GPLv3 es una licencia de software libre con copyleft fuerte. Sus principios fundamentales son:

Libertad de uso: Puedes ejecutar el programa para cualquier propósito.

Libertad de estudio y modificación: Puedes examinar cómo funciona el código y adaptarlo a tus necesidades. El acceso al código fuente es una condición necesaria.

Libertad de distribución: Puedes redistribuir copias del programa original o de tus versiones modificadas.

Libertad de contribuir a la comunidad: Si distribuyes versiones modificadas, debes hacerlo bajo la misma licencia GPLv3 y proporcionar el código fuente completo.

Obligaciones principales
Preservar los avisos de copyright y la licencia.

Mantener el código fuente disponible cuando distribuyas el software (incluso si es una versión modificada o integrada en otro proyecto).

No imponer restricciones adicionales que limiten los derechos otorgados por la licencia.

Si el software se utiliza para prestar un servicio a través de una red (SaaS), no estás obligado a liberar el código fuente. Sin embargo, la GPLv3 incluye cláusulas para proteger a los usuarios en esos casos (anti-tivoización).

¿Por qué GPLv3 para este proyecto?
Porque creemos que el conocimiento y las herramientas para desenmascarar el "humo tecnológico" deben permanecer libres y accesibles para todos. Queremos que cualquier mejora o derivado de este generador también sea compartido en las mismas condiciones, fomentando un ecosistema abierto.

El texto completo de la licencia está disponible en el archivo LICENSE y en https://www.gnu.org/licenses/gpl-3.0.html.

🔮 Posibles mejoras (Roadmap)
Si quieres expandir el proyecto, recuerda que cualquier modificación que distribuyas debe mantener la licencia GPLv3. Ideas:

Exportar/importar configuración como archivo JSON.

Permitir subir un CSV propio como fuente de datos.

Añadir más tipos de controles (select múltiple, radio, etc.).

Implementar memoria real (evitar repetir últimas N recomendaciones).

Convertir en PWA para funcionar offline como app.

Soporte para APIs externas (clima, calendario, etc.) mediante configuración de URL.

🙌 Créditos y agradecimientos
Idea original y desarrollo fruto de una conversación entre [tu nombre o alias] y DeepSeek, desenmascarando el hype de los agentes IA.

Si te gusta el proyecto, ¡dale una estrella ⭐ y compártelo!

"La libertad no es nada más que una oportunidad para ser mejor" – Albert Camus

text

### 📄 Archivo `LICENSE` que debes incluir

Junto al `README.md`, añade un archivo llamado `LICENSE` con el texto completo de la GPLv3. Puedes copiarlo de [https://www.gnu.org/licenses/gpl-3.0.txt](https://www.gnu.org/licenses/gpl-3.0.txt) o usar este bloque resumido (aunque es recomendable el texto íntegro):
GNU GENERAL PUBLIC LICENSE
Version 3, 29 June 2007

Copyright (C) 2007 Free Software Foundation, Inc. https://fsf.org/
Everyone is permitted to copy and distribute verbatim copies
of this license document, but changing it is not allowed.

Preamble

The GNU General Public License is a free, copyleft license for
software and other kinds of works.

(El texto completo continúa...)

text

### ⚠️ Nota importante sobre GPLv3

Si decides usar GPLv3, ten en cuenta que **cualquier persona que modifique el código y distribuya el resultado (incluso en una web pública)** está legalmente obligada a proporcionar el código fuente bajo la misma licencia. Esto garantiza que el proyecto y sus derivados permanezcan siempre libres. Si en el futuro quieres permitir usos propietarios, podrías considerar una licencia dual (GPL + comercial) o simplemente cambiar a MIT/Apache, pero eso requiere el consentimiento de todos los contribuyentes. 

¡Listo para GitHub con licencia GPLv3!
