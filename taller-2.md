# Taller 2 - Segundo Corte: React

* **Estudiante:** Juan Francisco De Avila Alfaro
* **Materia:** Desarrollo Frontend
* **Modalidad:** Individual
* **Fecha de entrega:** 16 de octubre de 2026

---

## Punto 1 · ¿Qué es React?

### ¿Qué es React y para qué sirve dentro del desarrollo web?

React es una librería de JavaScript de código abierto que se usa para armar la parte visual (la interfaz) de las páginas web. Básicamente, sirve para hacer páginas interactivas donde las cosas cambian en la pantalla sin necesidad de que la página se tenga que recargar entera a cada rato (lo que conocemos como SPA). La idea principal de React es que armas tu web dividiéndola en pedacitos o piezas sueltas (componentes) como botones, barras de navegación o tarjetas, y luego los juntas todos.

![React en el desarrollo web](img/puntos/react-logo.svg)

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

Por eso es una librería: no te resuelve la vida entera del proyecto, solo se enfoca en hacer la interfaz de usuario. Hoy existen frameworks construidos encima de React (como Next.js) que sí traen esas decisiones ya resueltas, pero React por sí solo sigue siendo una librería.

### ¿Qué significa que React sea declarativo?

Significa que tú solamente le dices a React **qué quieres que se vea** según los datos que tengas en ese momento, y React se encarga por detrás de hacer todo el trabajo sucio en el navegador.

* **Modo imperativo (JS normal):** Tienes que decirle paso a paso: "busca el botón con id tal, cámbiale el color a rojo, crea un párrafo, cárgale este texto y mételo al final del div".
* **Modo declarativo (React):** Tú simplemente dices: "si la variable `sesionIniciada` es verdadera, muestra el saludo; si es falsa, muestra el botón de login". Tú solo piensas en el resultado final.

**Fuentes de este punto:** React Team (equipo e historia), Wikipedia (historia de React) y la documentación oficial de React. Los enlaces están en la sección de referencias.

---

## Punto 2 · ¿Qué problema resuelve React?

### ¿Cuál era la dificultad principal de construir interfaces con JavaScript "a mano" (manipulando el DOM)?

El problema de usar JavaScript puro (`document.getElementById`, `innerHTML`, `appendChild`) en páginas grandes era que se volvía un dolor de cabeza inmanejable:

1. **El código se volvía un espagueti:** Si un dato cambiaba (por ejemplo, los productos del carrito de compras), te tocaba acordarte de cambiar el número en el ícono del carrito, actualizar el total a pagar y modificar la lista de productos manualmente. Si se te pasaba uno, la pantalla quedaba mostrando datos equivocados.
2. **Era fácil equivocarse y también podía salir pesado:** Cada vez que tocas el DOM a mano, el navegador tiene que recalcular el diseño y redibujar la pantalla. Si haces muchos cambios seguidos y sin cuidado, la página puede sentirse lenta. Aun así, el problema más grande no era la velocidad sino mantener todo consistente: a medida que la página crecía, era cada vez más difícil asegurarse de que lo que se veía coincidiera con los datos.

![Esquema Imperativo vs Declarativo](img/esquemas/imperativo-vs-declarativo.svg)

### Explica la diferencia entre el enfoque imperativo y el enfoque declarativo

* **Imperativo (El CÓMO):** Como cuando le das indicaciones de manejo a alguien: "avanza 2 cuadras, cruza a la derecha, frena, sube la ventana". Le dices cada pasito que tiene que hacer el navegador.
* **Declarativo (El QUÉ):** Como pedir un taxi por aplicación: "llévame a la universidad". No le dices al conductor por qué calles ir ni cuándo girar; tú solo pides el resultado y la aplicación se encarga de la ruta. En React pasa lo mismo: describes cómo debe verse la pantalla para cada situación y React se encarga de los pasos.

### ¿Cómo ayuda React a mantener la interfaz sincronizada con los datos (el estado)?

La idea central es que **la pantalla es el resultado de los datos (el estado)**. Tú no actualizas la pantalla pieza por pieza: cambias el dato, y React vuelve a calcular cómo debe verse la interfaz con ese dato nuevo. Así no te toca acordarte de actualizar el ícono, el total y la lista por separado, porque todos salen del mismo estado.

Para hacer eso de forma eficiente, React usa una técnica conocida como **Virtual DOM**:

1. React guarda en memoria una representación ligera de cómo debería verse la página.
2. Cuando algún dato cambia, React genera una nueva representación con ese cambio.
3. Compara la anterior con la nueva (un proceso que llaman *diffing*).
4. Se da cuenta de cuál fue la única cosita que cambió (por ejemplo, solo cambió un numerito) y va al navegador real a modificar únicamente eso, sin tocar el resto de la página.

![Esquema del Virtual DOM y reconciliación](img/esquemas/virtual-dom.svg)

### ¿Qué rol juegan los componentes reutilizables en la solución de ese problema?

Permiten no tener que repetir código una y otra vez. En vez de copiar y pegar el mismo bloque HTML de una tarjeta de producto 20 veces, creas un solo componente `<Tarjeta />` y lo usas las veces que quieras pasándole los datos de cada producto. Si mañana quieres cambiarle el color al botón de la tarjeta, lo cambias en un solo archivo y se arregla en toda la web automáticamente. Además, cada componente se encarga de dibujarse según sus propios datos, lo que mantiene el código ordenado aunque la aplicación crezca.

**Fuentes de este punto:** documentación oficial de React (*Reacting to Input with State* y *Render and Commit*). Los enlaces están en la sección de referencias.

---

## Punto 3 · Principales componentes de React

![Estructura general de componentes y Props](img/puntos/componentes.svg)

### 1. Componentes

* **Definición:** Son como piezas de Lego de código. Básicamente son funciones normales de JavaScript que devuelven lo que se va a ver en la pantalla.
* **Características:**
  * El nombre de la función siempre tiene que empezar con **mayúscula** (ejemplo: `MiBoton()`) para que React no lo confunda con una etiqueta HTML normal.
  * Son independientes: lo que pasa dentro de un componente no daña a los otros.
  * Se pueden anidar (meter componentes dentro de otros).
* **Ejemplo de código:**

```jsx
// 1. Declaración del componente Aviso
function Aviso() {
  return (
    <div className="alerta">
      <h4>Atención requerida</h4>
      <p>Asegúrese de guardar las modificaciones antes de cerrar.</p>
    </div>
  );
}

// 2. Componente principal que integra a Aviso
export default function App() {
  return (
    <main>
      <h1>Panel de Configuración</h1>
      {/* Invocación del componente Aviso */}
      <Aviso />
    </main>
  );
}
```

**¿Qué hace este código?** `Aviso` es un componente: una función que devuelve un bloque con un título y un mensaje. `App` es el componente principal y usa a `Aviso` escribiendo `<Aviso />` como si fuera una etiqueta HTML. Si necesito el mismo aviso en otra pantalla, solo vuelvo a escribir `<Aviso />` sin copiar el contenido.

### 2. JSX

* **Definición:** Es una forma de escribir código que mezcla HTML dentro de JavaScript. Hace que armar las pantallas sea mucho más cómodo y visual.
* **Características:**
  * Aunque parece HTML, no lo es. Por debajo se transforma en código JavaScript normal.
  * Todo lo que devuelvas tiene que estar envuelto en una sola etiqueta padre (o usar etiquetas vacías `<> </>`).
  * En vez de `class` se escribe `className` (porque `class` ya es una palabra reservada de JS).
  * Todas las etiquetas deben cerrarse, incluso las que en HTML no se cierran (por ejemplo `<img />` o `<input />`).
  * Si quieres meter variables o lógica de JavaScript dentro del diseño, solo las pones entre llaves `{}`.
* **Ejemplo de código:**

```jsx
export default function TarjetaUsuario() {
  const usuario = "Carlos";
  const puntos = 150;

  return (
    <div className="tarjeta-puntos">
      <h2>Bienvenido, {usuario}</h2>
      <p>Puntos bonificados acumulados: {puntos * 2}</p>
    </div>
  );
}
```

**¿Qué hace este código?** Crea dos variables normales de JavaScript (`usuario` y `puntos`) y las muestra dentro del JSX usando llaves. Dentro de las llaves también se pueden hacer operaciones, así que el párrafo muestra `puntos * 2`, es decir, 300. El `div` es la única etiqueta padre que envuelve todo lo que devuelve el componente, y `className` se usa en lugar de `class`.

### 3. Props

* **Definición:** Son datos o información que le mandas a un componente desde afuera (de un componente padre a uno hijo), muy parecido a cuando le pasas argumentos a una función.
* **Características:**
  * Van en una sola dirección: siempre viajan de padre a hijo.
  * Son de solo lectura: el componente que las recibe no las puede modificar por su cuenta.
  * Puedes pasar de todo: textos, números, objetos o funciones.
* **Ejemplo de código:**

```jsx
// Componente hijo que recibe las propiedades 'texto' y 'color'
function BotonAccion({ texto, color }) {
  return (
    <button style={{ backgroundColor: color, color: 'white', padding: '10px' }}>
      {texto}
    </button>
  );
}

// Componente padre que utiliza BotonAccion con diferentes configuraciones
export default function BarraHerramientas() {
  return (
    <div>
      <BotonAccion texto="Guardar cambios" color="green" />
      <BotonAccion texto="Eliminar registro" color="red" />
    </div>
  );
}
```

**¿Qué hace este código?** `BotonAccion` es un solo componente que recibe dos props, `texto` y `color`, y con ellas arma el botón. `BarraHerramientas` (el padre) lo usa dos veces con valores distintos: el resultado es un botón verde que dice "Guardar cambios" y otro rojo que dice "Eliminar registro". El hijo solo lee esos valores, no los cambia.

### 4. Estado (useState)

* **Definición:** Es la memoria propia que tiene un componente para acordarse de cosas que pueden cambiar mientras el usuario usa la página (como un texto escrito, un contador o si un menú está abierto o cerrado).
* **Características:**
  * Se usa la función `useState()`.
  * Te devuelve dos cosas en una lista: el valor de la variable y una función especial para cambiar ese valor.
  * Cada vez que usas esa función para cambiar el dato, React se da cuenta y vuelve a pintar el componente con el nuevo valor.
* **Ejemplo de código:**

```jsx
import { useState } from 'react';

export default function ContadorMeGusta() {
  // Declaración del estado: likes (valor actual) y setLikes (función actualizadora)
  const [likes, setLikes] = useState(0);

  function darLike() {
    setLikes(likes + 1);
  }

  return (
    <div>
      <p>Total de reacciones: {likes}</p>
      <button onClick={darLike}>Reaccionar 👍</button>
    </div>
  );
}
```

**¿Qué hace este código?** El estado `likes` empieza en 0. Cuando el usuario hace clic en el botón se ejecuta `darLike`, que llama a `setLikes(likes + 1)`. Al ver que el estado cambió, React vuelve a ejecutar el componente y el párrafo muestra el número nuevo. Si en lugar de `useState` usara una variable normal, el valor podría cambiar, pero la pantalla no se actualizaría, porque React no se enteraría del cambio.

![Cómo funciona useState](img/puntos/usestate.svg)

### 5. Eventos (onClick, onChange)

* **Definición:** Es la manera en que React se entera de las cosas que hace el usuario (hacer clics, teclear, enviar un formulario) y ejecuta una función de respuesta.
* **Características:**
  * Se escriben con mayúscula intermedia (camelCase): `onClick`, `onChange`, `onSubmit`.
  * Tienes que pasarle la función sin ejecutar (sin poner los paréntesis `()`), para que solo se dispare cuando el usuario haga la acción. Por ejemplo, `onClick={darLike}` es correcto; `onClick={darLike()}` ejecutaría la función apenas se dibuja el componente, no al hacer clic.
  * `onClick` responde a los clics y `onChange` responde cuando cambia el valor de un campo, por ejemplo cada vez que el usuario escribe en un input.
* **Ejemplo de código:**

```jsx
import { useState } from 'react';

export default function EntradaTexto() {
  const [mensaje, setMensaje] = useState('');

  // Función manejadora que extrae el texto ingresado
  function alEscribir(e) {
    setMensaje(e.target.value);
  }

  return (
    <div>
      <input
        type="text"
        placeholder="Escriba un texto..."
        value={mensaje}
        onChange={alEscribir}
      />
      <p>Contenido procesado: {mensaje}</p>
    </div>
  );
}
```

**¿Qué hace este código?** El valor del `input` viene del estado `mensaje`. Cada vez que el usuario teclea, se dispara `onChange` y se ejecuta `alEscribir`, que guarda en el estado el texto actual (`e.target.value`). Como el estado cambió, React vuelve a dibujar el componente y el párrafo de abajo muestra lo que se va escribiendo en tiempo real.

**Fuentes de este punto:** documentación oficial de React (*Describing the UI* y *State: A Component's Memory*). Los enlaces están en la sección de referencias.

---

## Punto 4 · Importancia de React en la industria

### ¿Por qué tantas empresas eligen React para sus productos web?

A las empresas les gusta porque ahorra tiempo y plata. Al poder reutilizar componentes, los equipos de diseño y desarrollo crean "sistemas de diseño" que usan en varios productos a la vez. Además, como es tan conocido, cuando una empresa necesita contratar un desarrollador front-end es mucho más fácil encontrar a alguien que ya sepa React que buscar a alguien de tecnologías menos usadas. Esto se ve en los datos: en la encuesta de desarrolladores de Stack Overflow de 2025, React fue la tecnología más usada en la categoría de frameworks y tecnologías web, con cerca del 45 % de los encuestados.

### ¿Qué aporta React al ecosistema de desarrollo?

React cambió totalmente la forma de programar en la web y creó un ecosistema gigante alrededor:

* Creó la base para frameworks más grandes como Next.js o Remix, que sirven para hacer páginas completas con buen posicionamiento en Google (SEO).
* Con **React Native**, un programador web puede usar prácticamente lo mismo que aprendió en React para hacer aplicaciones móviles para Android y iPhone.
* Hay miles de librerías hechas por la comunidad en `npm` listas para usar: cosas para formularios, tablas, animaciones o manejo de datos.

### ¿Qué papel juegan su comunidad y su mantenimiento?

Es clave porque React no es un proyecto abandonado. Durante años lo mantuvo principalmente Meta, pero eso cambió: el **24 de febrero de 2026** se lanzó oficialmente la **React Foundation**, una fundación independiente alojada en la Linux Foundation. Desde entonces, React, React Native y proyectos relacionados como JSX ya no pertenecen a Meta, sino a esa fundación. Sus ocho miembros fundadores de nivel platino son Amazon, Callstack, Expo, Huawei, Meta, Microsoft, Software Mansion y Vercel.

Según el anuncio oficial, la dirección técnica de React se mantiene independiente de la junta de la fundación y sigue en manos de las personas que contribuyen y mantienen el proyecto. Esto le da más estabilidad a largo plazo, porque React ya no depende de una sola empresa.

Además, la comunidad es inmensa: si tienes un error o duda rara, lo buscas en Google o foros y es casi seguro que a otra persona ya le pasó y está resuelto.

### ¿Por qué es una habilidad relevante para un desarrollador front-end hoy en día?

Porque es muy común que las ofertas de empleo de front-end en portales de trabajo (LinkedIn, Get on Board, etc.) pidan saber React como requisito principal o deseable, y los datos de uso de la encuesta de Stack Overflow muestran que sigue siendo la opción más extendida. Además, aprender React te enseña a pensar la web en componentes y manejar datos de forma ordenada, lo que te hace mejor programador en general.

**Fuentes de este punto:** anuncio oficial de la React Foundation en react.dev, React Team, y la encuesta de desarrolladores de Stack Overflow 2025. Los enlaces están en la sección de referencias.

---

## Punto 5 · Grandes empresas que utilizan React

### 1. Netflix

**¿En qué producto o sección lo usan?**

Netflix ha documentado el uso de React en el desarrollo de la interfaz de usuario de su aplicación para televisores inteligentes (*Smart TVs*) y otros dispositivos de reproducción multimedia.

![Interfaz de Netflix en TV](img/puntos/netflix-ui.svg)

**¿Por qué es un caso relevante?**

Los televisores inteligentes pueden tener menos capacidad de procesamiento y memoria que un computador convencional. Por esta razón, desarrollar interfaces rápidas y fluidas representa un desafío para los equipos de ingeniería.

En un artículo técnico publicado en enero de 2017, Netflix explicó cómo desarrolló una solución llamada **React-Gibbon**. Esta implementación adaptaba React a Gibbon, un motor gráfico utilizado por Netflix para representar su interfaz en dispositivos de televisión, en lugar de depender del DOM tradicional del navegador.

Gracias a esta arquitectura, los desarrolladores podían construir interfaces mediante componentes declarativos de React y aplicar optimizaciones para mejorar el rendimiento en dispositivos con recursos limitados.

Este caso demuestra que React puede adaptarse a diferentes entornos de ejecución y que la optimización del código es importante para ofrecer una buena experiencia de usuario.

* **Fuente:**
  * Netflix Technology Blog. [Crafting a high-performance TV user interface using React](https://medium.com/netflix-techblog/crafting-a-high-performance-tv-user-interface-using-react-3350e5a6ad3b).

### 2. Airbnb

**¿En qué producto o sección lo usan?**

Airbnb usa React en su sitio web. En su blog de ingeniería cuenta que, desde principios de 2015, adoptó React como su librería principal para construir las vistas del front-end, y que más adelante migró a React la página de búsqueda de alojamientos, que antes estaba hecha con otra herramienta. En otro artículo, explica cómo reestructuró el front-end del sitio: pasó de páginas armadas por completo en el servidor con Rails a un esquema que combina React, React Router y renderizado de React en el servidor con una herramienta propia llamada Hypernova.

![Interfaz de Airbnb](img/puntos/airbnb-ui.svg)

**¿Por qué es un caso relevante?**

Airbnb es una plataforma de alojamiento y viajes con muchas secciones que deben sentirse como una sola experiencia: la búsqueda de propiedades, las fichas de alojamientos y el proceso de reserva. Su caso es interesante porque no empezó con React desde cero: tenía código antiguo y lo fue migrando, lo que muestra que React también sirve para modernizar aplicaciones grandes que ya existen.

React permite dividir la interfaz en componentes independientes que se pueden reutilizar y mantener con más facilidad. Airbnb además compartió con la comunidad herramientas y convenciones de programación, entre ellas su guía de estilo de JavaScript y sus recomendaciones para React y JSX, lo que ayuda a entender cómo los componentes reutilizables y las buenas prácticas organizan aplicaciones web complejas.

* **Fuentes:**
  * Airbnb Tech Blog. [Moving Airbnb Search to React](https://medium.com/airbnb-engineering/b85b815e166c) (marzo de 2017).
  * Airbnb Engineering. [Rearchitecting Airbnb's Frontend (Archivo Web)](https://web.archive.org/web/20201208162910/https://medium.com/airbnb-engineering/rearchitecting-airbnbs-frontend-5e213efc24d2).
  * Airbnb. [React/JSX Style Guide](https://github.com/airbnb/javascript/tree/master/react).

---

## Referencias

**Documentación oficial de React**

* React. [Describing the UI](https://es.react.dev/learn/describing-the-ui). Consultada para estudiar los componentes, JSX y la organización de las interfaces.
* React. [State: A Component's Memory](https://es.react.dev/learn/state-a-components-memory). Consultada para comprender el estado de los componentes y el funcionamiento de `useState`.
* React. [Reacting to Input with State](https://es.react.dev/learn/reacting-to-input-with-state). Consultada para entender el enfoque declarativo y cómo la interfaz depende del estado.
* React. [Render and Commit](https://es.react.dev/learn/render-and-commit). Consultada para entender cómo React actualiza solo lo que cambió en el DOM.
* React. [React Team](https://es.react.dev/community/team). Consultada para conocer el equipo y la comunidad que participan en el desarrollo y mantenimiento de React.
* React. [The React Foundation: A New Home for React Hosted by the Linux Foundation](https://react.dev/blog/2026/02/24/the-react-foundation) (24 de febrero de 2026). Consultada para saber quién mantiene React hoy.

**Industria y empresas**

* Netflix Technology Blog. [Crafting a high-performance TV user interface using React](https://medium.com/netflix-techblog/crafting-a-high-performance-tv-user-interface-using-react-3350e5a6ad3b). Fuente técnica sobre React-Gibbon y la optimización de interfaces para dispositivos de televisión.
* Airbnb Tech Blog. [Moving Airbnb Search to React](https://medium.com/airbnb-engineering/b85b815e166c). Fuente sobre la adopción de React en Airbnb y la migración de su página de búsqueda.
* Airbnb Engineering. [Rearchitecting Airbnb's Frontend (Archivo Web)](https://web.archive.org/web/20201208162910/https://medium.com/airbnb-engineering/rearchitecting-airbnbs-frontend-5e213efc24d2). Fuente sobre la evolución de la arquitectura del front-end de Airbnb.
* Airbnb. [JavaScript Style Guide](https://github.com/airbnb/javascript). Recurso sobre convenciones y buenas prácticas para escribir código JavaScript.
* Airbnb. [React/JSX Style Guide](https://github.com/airbnb/javascript/tree/master/react). Recurso con recomendaciones de estilo para desarrollar componentes React y utilizar JSX.
* Stack Overflow. [Developer Survey 2025](https://survey.stackoverflow.co/2025/). Consultada para los datos de uso de React frente a otras tecnologías web.

**Complementaria**

* Wikipedia. [React](https://es.wikipedia.org/wiki/React). Fuente complementaria para contextualizar la historia y las características generales de React.
