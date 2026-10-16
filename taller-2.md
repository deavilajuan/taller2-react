# Taller 2 - Segundo Corte: React
* **Estudiante:** Juan Francisco De Avila Alfaro
* **Materia:** Desarrollo Frontend
* **Modalidad:** Individual
* **Fecha de entrega:** 16 de octubre de 2026
---
## Punto 1 · ¿Qué es React?
### ¿Qué es React y para qué sirve dentro del desarrollo web?
React es una herramienta de JavaScript que se usa para armar la parte visual (la interfaz) de las páginas web. Básicamente, sirve para hacer páginas interactivas donde las cosas cambian en la pantalla sin necesidad de que la página se tenga que recargar entera a cada rato (lo que conocemos como SPA). La idea principal de React es que armas tu web dividiéndola en pedacitos o piezas sueltas (componentes) como botones, barras de navegación o tarjetas, y luego los juntas todos.
![React en el desarrollo web](img/puntos/react-logo.png)
### ¿Quién lo creó y en qué año apareció?
Lo creó **Jordan Walke**, que era un programador de **Facebook** (hoy Meta). 
* Primero lo crearon de forma interna en 2011 para solucionar problemas que tenían con el muro de noticias de Facebook.
* Luego lo usaron en Instagram en 2012.
* Finalmente lo abrieron al público (código abierto) en **mayo de 2013** en una conferencia de JavaScript (JSConf US).
### ¿Es una librería o un framework? Explica la diferencia y justifica tu respuesta
**React es una librería**, no un framework.
La diferencia principal está en quién manda a quién (lo que llaman inversión de control):
* **En un framework (como Angular):** El framework es como una casa prefabricada con reglas estrictas. Te dice exactamente cómo ordenar las carpetas, cómo hacer las rutas y cómo llamar a las APIs. El framework maneja tu código.
* **En una librería (como React):** React es más bien como una herramienta específica de tu caja de herramientas. Solo se encarga de pintar cosas en la pantalla (la vista). Tú decides qué estructura ponerle a tu proyecto, qué usar para cambiar de página (rutas) o cómo traer los datos de internet. 
Por eso es una librería: no te resuelve la vida entera del proyecto, solo se enfoca en hacer la interfaz de usuario.
### ¿Qué significa que React sea declarativo?
Significa que tú solamente le dices a React **qué quieres que se vea** según los datos que tengas en ese momento, y React se encarga por detrás de hacer todo el trabajo sucio en el navegador.
* **Modo imperativo (JS normal):** Tienes que decirle paso a paso: "busca el botón con id tal, cámbiale el color a rojo, crea un párrafo, cárgale este texto y mételo al final del div".
* **Modo declarativo (React):** Tú simplemente dices: "si la variable `sesionIniciada` es verdadera, muestra el saludo; si es falsa, muestra el botón de login". Tú solo piensas en el resultado final.
---
## Punto 2 · ¿Qué problema resuelve React?
### ¿Cuál era la dificultad principal de construir interfaces con JavaScript "a mano" (manipulando el DOM)?
El problema de usar JavaScript puro (`document.getElementById`, `innerHTML`, `appendChild`) en páginas grandes era que se volvía un dolor de cabeza inmanejable:
1. **El código se volvía un espagueti:** Si un dato cambiaba (por ejemplo, los productos del carrito de compras), te tocaba acordarte de cambiar el número en el ícono del carrito, actualizar el total a pagar y modificar la lista de productos manualmente. Si se te pasaba uno, la pantalla quedaba mostrando datos equivocados.
2. **Era lento:** Cada vez que tocas el DOM a mano, el navegador gasta recursos recalculando el diseño y redibujando la pantalla. Si hacías muchos cambios seguidos, la página se sentía pesada o lagueada.
![Esquema Imperativo vs Declarativo](img/esquemas/imperativo-vs-declarativo.png)
### Explica la diferencia entre el enfoque imperativo y el enfoque declarativo
* **Imperativo (El CÓMO):** Como cuando le das indicaciones de manejo a alguien: "avanza 2 cuadras, cruza a la derecha, frena, sube la ventana". Le dices cada pasito que tiene que hacer el navegador.
* **Declarativo (El QUÉ):** Como pedir un taxi por aplicación: "llévame a la universidad". No le dices al conductor cómo meter los cambios ni por qué calle exacta meterse; tú solo pides el resultado y React se encarga de la ruta.
### ¿Cómo ayuda React a mantener la interfaz sincronizada con los datos (el estado)?
React lo soluciona usando algo llamado **Virtual DOM**:
1. React tiene una copia ligera de la página guardada en la memoria RAM.
2. Cuando algún dato de tu página cambia, React dibuja una nueva copia en memoria con ese cambio.
3. Compara la copia vieja con la nueva (un proceso que llaman *Diffing*).
4. Se da cuenta de cuál fue la única cosita que cambió (por ejemplo, solo cambió un numerito) y va al navegador real a cambiar únicamente ese numerito, sin tener que recargar ni tocar el resto de la página.
![Esquema del Virtual DOM y reconciliación](img/esquemas/virtual-dom.png)
### ¿Qué rol juegan los componentes reutilizables en la solución de ese problema?
Permiten no tener que repetir código una y otra vez. En vez de copiar y pegar el mismo bloque HTML de una tarjeta de producto 20 veces, creas un solo componente `<Tarjeta />` y lo usas las veces que quieras pasándole los datos de cada producto. Si mañana quieres cambiarle el color al botón de la tarjeta, lo cambias en un solo archivo y se arregla en toda la web automáticamente.
---
## Punto 3 · Principales componentes de React
![Estructura general de componentes y Props](img/puntos/componentes.png)
### 1. Componentes
* **Definición:** Son como piezas de Lego de código. Básicamente son funciones normales de JavaScript que devuelven lo que se va a ver en la pantalla.
* **Características:**
  * El nombre de la función siempre tiene que empezar con **mayúscula** (ejemplo: `MiBoton()`) para que React no lo confunda con una etiqueta HTML normal.
  * Son independientes: lo que pasa dentro de un componente no daña a los otros.
  * Se pueden anidar (meter componentes dentro de otros).
* **Ejemplo de código:**
```jsx

function Aviso() {
  return (
    <div className="alerta">
      <h4>¡Cuidado!</h4>
      <p>No olvides guardar tus cambios antes de salir.</p>
    </div>
  );
}
export default function App() {
  return (
    <div>
      <h1>Panel de usuario</h1>
      <Aviso />
    </div>
  );
}
