<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Rexo — El Dinosaurio que Soñaba Ser Dragón (25 páginas)</title>
<style>
/* --- Evitar selección / menú copiar --- */
* {
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  user-select: none;
}

/* --- Estilos generales (mantener diseño exacto) --- */
body {
  margin: 0;
  padding: 0;
  background: #000; /* fondo negro estilo manga */
  font-family: Arial, sans-serif;
  height: 100vh;
  overflow: hidden;
  touch-action: manipulation;
}

/* Página a pantalla completa */
.page {
  width: 100vw;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  display: none;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

/* página visible */
.page.visible {
  display: flex;
}

/* Grid 2x2 para las 4 viñetas */
.grid {
  width: 90%;
  height: 75%;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  gap: 12px;
  box-sizing: border-box;
}

/* Panel / viñeta (tamaño y estilo conservados) */
.panel {
  background: #fff;
  padding: 12px;
  font-size: 16px;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  border-width: 6px;
  border-style: solid;
  border-radius: 8px;
  box-sizing: border-box;
  line-height: 1.3;
  color: #000;
}

/* Borde-color según posición (1..4) */
.panel:nth-child(1) { border-color: var(--rojo, #ff3b30); }
.panel:nth-child(2) { border-color: var(--morado, #9b59b6); }
.panel:nth-child(3) { border-color: var(--azul, #007aff); }
.panel:nth-child(4) { border-color: var(--amarillo, #f1c40f); color: #000; }

/* Botones (centrados cuando hay uno, separación cuando hay dos) */
.buttons {
  position: absolute;
  bottom: 20px;
  width: 90%;
  display: flex;
  justify-content: center; /* centra cuando hay 1; gap separa cuando 2 */
  gap: 12px;
  box-sizing: border-box;
}

/* Botón */
button.nav {
  width: 48%;
  padding: 12px;
  font-size: 14px; /* 25% más pequeño que antes */
  font-weight: bold;
  background: #5A2A9C; /* morado */
  color: #fff;
  border: none;
  border-radius: 8px;
  box-shadow: none;
}

/* Estado deshabilitado */
button.nav:disabled {
  background: #444;
  color: #aaa;
}
</style>
</head>
<body>

<!-- Contenedor de páginas generado por JS -->
<div id="container"></div>

<script>
/* ============================
   Historia: 25 páginas × 4 paneles
   Rexo: dinosaurio que soñaba con ser dragón
   ============================ */

const pages = [
  // página 1
  [
    "Rexo nació en una llanura de gigantes antiguas.",
    "Desde pequeño miraba al cielo con curiosidad.",
    "Mientras otros jugaban a cazar, él miraba las nubes.",
    "Tenía un sueño silencioso: convertirse en dragón."
  ],

  // página 2
  [
    "Los demás dinos se reían: 'Los dragones son leyendas'.",
    "Rexo no se rendía; practicaba rugidos frente al lago.",
    "Intentaba batir sus patas como si fueran alas.",
    "Al anochecer, miraba la luna y susurraba: 'Un día...'"
  ],

  // página 3
  [
    "Una tarde, el viento trajo historias de un anciano dragón.",
    "Decían que vivía en las montañas de fuego lejanas.",
    "Rexo sintió que su corazón latía con fuerza.",
    "Tomó la decisión: partiría a encontrar a ese dragón."
  ],

  // página 4
  [
    "Caminó por praderas que parecían mares verdes.",
    "Atravesó ríos y durmió bajo millones de estrellas.",
    "Cada paso lo acercaba a su sueño, pero también lo cansaba.",
    "Aún así, su decisión se volvió más firme."
  ],

  // página 5
  [
    "En un risco vio una silueta inmensa recostada: el dragón.",
    "El anciano dragón abrió un ojo, calmo y profundo.",
    "Rexo avanzó con respeto y un nudo en la garganta.",
    "—¿Por qué buscas ser dragón? —preguntó la voz grave."
  ],

  // página 6
  [
    "Rexo explicó su sueño, tímido y lleno de esperanza.",
    "Habló de alas, fuego y de volar sobre el mundo.",
    "El dragón anciano rió, pero no con burla: con ternura.",
    "—Para ser dragón debes entender qué significa serlo."
  ],

  // página 7
  [
    "El dragón le enseñó que ser dragón es proteger, no solo volar.",
    "Que la fuerza viene del coraje, la sabiduría y el corazón.",
    "Rexo escuchó atentamente, sintiendo cada palabra.",
    "El anciano propuso una prueba: demostrar valor verdadero."
  ],

  // página 8
  [
    "Rexo aceptó sin dudar; su pulso era fuego en la boca.",
    "Antes de irse, el dragón le dio un pequeño cristal azul.",
    "—Cuando estés perdido, mira esta luz —dijo el anciano.",
    "Rexo guardó el cristal como quien guarda una promesa."
  ],

  // página 9
  [
    "De regreso al valle, el cielo se nubló de repente.",
    "Una gran grieta apareció en la colina cercana.",
    "Los moradores comenzaron a correr, el pánico creció.",
    "Rexo sintió un miedo nuevo: algo más peligroso venía."
  ],

  // página 10
  [
    "Un derrumbe atrapó a varios pequeños dinosaurios en la zanja.",
    "Entre ellos, un bebé llamado Pico lloraba asustado.",
    "Los adultos, pesados y lentos, no podían mover grandes rocas.",
    "Rexo vio la oportunidad de probar su coraje."
  ],

  // página 11
  [
    "Se acercó a la grieta: las piedras eran inmensas.",
    "Intentó empujar, pero se deslizó y cayó varios pasos atrás.",
    "La desesperación lo golpeó; no sabía si sería suficiente.",
    "Recordó la voz del dragón: 'El coraje es persistencia'."
  ],

  // página 12
  [
    "Respiró hondo y usó su cuerpo como palanca con ingenio.",
    "Apiló ramas, palos y formó una cuña para mover piedras.",
    "No fue fuerza pura; fue pensar y persistir con valor.",
    "Poco a poco, una roca cedió y Pico asomó temblando."
  ],

  // página 13
  [
    "Rexo tiró de Pico hacia afuera con todas sus fuerzas.",
    "Los demás aplaudieron, la madre lloró de alivio.",
    "En los ojos de Rexo hubo miedo, pero también orgullo.",
    "Había salvado una vida; por primera vez se sintió distinto."
  ],

  // página 14
  [
    "La noticia del rescate corrió por todo el valle.",
    "Los que se burlaban antes ahora miraban con respeto.",
    "Rexo no se jactó; su corazón solo latía más tranquilo.",
    "Esa noche, bajo la luna, sostuvo el cristal y sonrió."
  ],

  // página 15
  [
    "Pero el valle no estaba libre de peligros aún.",
    "Un enorme depredador de bloques acechaba en la sombra.",
    "Su llegada amenazaba a todos: cosechas, refugios y vidas.",
    "Los ancianos se reunieron: había que preparar defensa."
  ],

  // página 16
  [
    "Rexo ofreció ayudar; su voz no era perfecta, pero firme.",
    "Organizó a los jóvenes: barreras, alarmas y rutas de escape.",
    "No tenía fuerza para pelear solo, pero sí para liderar.",
    "Su plan calmó a muchos; por primera vez lo siguieron."
  ],

  // página 17
  [
    "La bestia atacó al anochecer, un rugido que hizo temblar la tierra.",
    "Los mayores luchaban, algunos caían, la situación era dura.",
    "Rexo y los jóvenes guiaron a los más pequeños a seguridad.",
    "Su liderazgo salvó a muchos; su valor crecía como llama."
  ],

  // página 18
  [
    "En un momento crítico, la bestia atrapó a un guardián veterano.",
    "Rexo corrió sin pensar y distrajo a la criatura con astucia.",
    "Usó espejos de agua y luces para confundirla.",
    "La bestia quedó mareada y retrocedió por un instante."
  ],

  // página 19
  [
    "Esa ventana permitió a los adultos acabar con la amenaza.",
    "La bestia huyó, dejando marcas pero sin destruir el valle.",
    "Gritos de victoria, abrazos y lágrimas de todos por doquier.",
    "Rexo, exhausto, cayó de rodillas; su pecho ardía de emoción."
  ],

  // página 20
  [
    "El anciano dragón apareció al borde de la colina, observando.",
    "No había intervenido antes; había querido ver la prueba.",
    "Rexo levantó la vista y vio orgullo en los ojos del dragón.",
    "El valle celebró a su nuevo protector, el DinoDragón en alma."
  ],

  // página 21
  [
    "El dragón descendió y habló con voz que llenó el aire.",
    "—Has demostrado lo que realmente hace a uno dragón—",
    "—coraje, sacrificio y la voluntad de proteger a otros—",
    "Rexo escuchó y sintió una paz profunda en su interior."
  ],

  // página 22
  [
    "El anciano puso su garra sobre el cristal azul de Rexo.",
    "La piedra brilló y una cálida energía recorrió su cuerpo.",
    "No aparecieron alas, ni fuego visible… solo una calma feroz.",
    "Rexo comprendió que su poder venía del interior."
  ],

  // página 23
  [
    "Con el tiempo, Rexo ya no soñaba con ser otro ser.",
    "Su sueño cambió: quería que todos pudieran sentirse protegidos.",
    "Entrenó a los jóvenes en valor, en ingenio y en empatía.",
    "El valle se volvió más fuerte y unido que nunca."
  ],

  // página 24
  [
    "Años después, los cuentos decían: 'Rexo el DinoDragón, guardián'.",
    "Los niños imitaban su rugido y sus gestos de ayuda.",
    "El anciano dragón, ya viejo, dormía en paz sabiendo el mundo mejor.",
    "Rexo miraba al horizonte: su sueño se había convertido en legado."
  ],

  // página 25 (cierre)
  [
    "Una tarde, Rexo llevó a Pico —ya crecido— al risco del antiguo dragón.",
    "Le contó la historia de cómo un pequeño decidió no rendirse.",
    "Pico miró las nubes y dijo: 'Quiero ser valiente como tú'.",
    "Rexo sonrió: el dragón no fue el final, fue el comienzo."
  ]
];

/* ==== Crear páginas en DOM ==== */
const container = document.getElementById('container');

pages.forEach((panels, index) => {
  const pageDiv = document.createElement('div');
  pageDiv.className = 'page';
  pageDiv.id = 'page' + (index + 1);

  // grid
  const grid = document.createElement('div');
  grid.className = 'grid';

  // panels (4)
  panels.forEach(text => {
    const p = document.createElement('div');
    p.className = 'panel';
    p.textContent = text;
    grid.appendChild(p);
  });

  pageDiv.appendChild(grid);

  // botones
  const buttons = document.createElement('div');
  buttons.className = 'buttons';

  // anterior
  const prev = document.createElement('button');
  prev.className = 'nav';
  prev.textContent = '← Página anterior';
  prev.onclick = () => showPage(current - 1);
  if (index === 0) prev.disabled = true;

  // siguiente
  const next = document.createElement('button');
  next.className = 'nav';
  next.textContent = 'Página siguiente →';
  next.onclick = () => showPage(current + 1);
  if (index === pages.length - 1) next.disabled = true;

  // Append smart: si disabled no lo retiramos (mantener consistencia visual),
  // pero como pediste antes: cuando solo hay uno que aparezca centrado.
  // Con justify-content:center y gap, si uno está disabled se ve atenuado en su lugar.
  buttons.appendChild(prev);
  buttons.appendChild(next);

  pageDiv.appendChild(buttons);
  container.appendChild(pageDiv);
});

/* ==== Navegación ==== */
let current = 1;
const total = pages.length;

function showPage(n) {
  if (n < 1 || n > total) return;
  // ocultar todas
  document.querySelectorAll('.page').forEach(p => p.classList.remove('visible'));
  // mostrar la solicitada
  document.getElementById('page' + n).classList.add('visible');
  current = n;

  // Actualizar estado botones (enable/disable)
  document.querySelectorAll('.page').forEach((pg, idx) => {
    const prevBtn = pg.querySelector('button.nav:nth-child(1)');
    const nextBtn = pg.querySelector('button.nav:nth-child(2)');
    // prevBtn y nextBtn existen, pero debemos habilitar/inhabilitar segun current
    if (idx + 1 === current) {
      // prev
      if (current === 1) prevBtn.disabled = true; else prevBtn.disabled = false;
      // next
      if (current === total) nextBtn.disabled = true; else nextBtn.disabled = false;
    }
  });
}

// Mostrar página 1 inicial
showPage(1);

/* ==== Prevenir zoom por doble-tap y pinch (iPhone) ==== */
/* doble-tap */
let lastTouch = 0;
document.addEventListener('touchend', function (e) {
  const now = new Date().getTime();
  if (now - lastTouch <= 300) {
    e.preventDefault(); // evita zoom por doble tap
  }
  lastTouch = now;
}, { passive: false });

/* pinch-to-zoom se controla con meta viewport (ya agregado) */

/* ==== Opcional: permitir cambio rápido con teclado (para probar en PC) ==== */
document.addEventListener('keydown', (e) => {
  if (e.key === 'ArrowRight') showPage(Math.min(total, current + 1));
  if (e.key === 'ArrowLeft') showPage(Math.max(1, current - 1));
});
</script>

</body>
</html>
