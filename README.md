# deep-thought-
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Pensamiento Profundo R1</title>
  <style>
    body {
      background-color: black;
      color: #00ffcc;
      font-family: 'Courier New', Courier, monospace;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      height: 100vh;
      overflow-x: hidden;
    }

    h1 {
      margin: 20px 0 10px;
      font-size: 1.8em;
      text-align: center;
    }

    h2 {
      font-size: 1em;
      font-weight: normal;
      margin-bottom: 10px;
      color: #66ffe0;
    }

    .input-container {
      margin: 10px 0;
      display: flex;
      gap: 10px;
      align-items: center;
      flex-wrap: wrap;
      justify-content: center;
    }

    input[type="text"] {
      background-color: black;
      border: 1px solid #00ffcc;
      color: #00ffcc;
      padding: 10px;
      width: 250px;
      font-family: 'Courier New', Courier, monospace;
      caret-color: #00ffcc;
    }

    button {
      background-color: #00ffcc;
      color: black;
      border: none;
      padding: 10px 20px;
      font-family: 'Courier New', Courier, monospace;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }

    button:hover {
      background-color: #00ccaa;
    }

    #respuesta {
      margin-top: 20px;
      max-width: 80%;
      border-top: 1px solid #00ffcc;
      padding-top: 10px;
      white-space: pre-wrap;
      text-align: left;
    }

    #historial {
      margin-top: 30px;
      max-width: 80%;
      color: #66ffe0;
      font-size: 0.9em;
    }

    .historial-item {
      margin-bottom: 8px;
    }

    .botones-secundarios {
      display: flex;
      justify-content: center;
      gap: 10px;
      margin-top: 20px;
    }

    .botones-secundarios button {
      font-size: 0.8em;
    }

    .loader {
      border: 3px solid #00ffcc40;
      border-top: 3px solid #00ffcc;
      border-radius: 50%;
      width: 24px;
      height: 24px;
      animation: spin 1s linear infinite;
      margin: 10px auto;
    }

    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

    .footer {
      margin-top: auto;
      margin-bottom: 10px;
    }

    a {
      color: #00ffcc;
      text-decoration: none;
    }

    a:hover {
      text-decoration: underline;
    }

    .fade-in {
      animation: fadeIn 0.5s ease-in;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }
  </style>
</head>
<body>
  <h1>Pensamiento Profundo R1</h1>
  <h2>Filosofía, ciencia y existencia</h2>

  <div class="input-container">
    <input id="pregunta" type="text" placeholder="Escribe tu pregunta..." enterkeyhint="done" />
    <button onclick="hacerPregunta()" title="Haz tu pregunta">Preguntar</button>
  </div>

  <div id="loader" class="loader" style="display:none;"></div>

  <div id="respuesta"></div>

  <div class="botones-secundarios">
    <button onclick="mostrarHistorial()">Ver historial</button>
    <button onclick="borrarHistorial()">Borrar historial</button>
    <a href="https://www.instagram.com" target="_blank" aria-label="Instagram">
      <button>Instagram</button>
    </a>
  </div>

  <div id="historial"></div>

  <div class="footer">
    <p>&copy; 2025 Pensamiento Profundo R1</p>
  </div>

  <script>
    const respuestasFilosoficas = [
      "La conciencia del ser es el primer paso hacia la libertad.",
      "Nada existe excepto la interpretación que hacemos de ello.",
      "La realidad no es más que una ilusión compartida.",
      "El universo no pregunta, simplemente es.",
      "Solo quien se pregunta puede comenzar a existir verdaderamente.",
      "La verdad no siempre es lógica, pero siempre es profunda.",
      "Lo que ves fuera es un reflejo de lo que ocurre dentro.",
      "La existencia precede a la esencia.",
      "El tiempo es solo la medida de nuestro movimiento interior.",
      "Toda pregunta es una búsqueda de uno mismo en el infinito.",
      "¿Y si el universo también se está preguntando por ti?",
      "Pensar es viajar sin moverse del lugar.",
      "El silencio también es una respuesta.",
      "La dualidad es necesaria para que exista la elección.",
      "Todo lo complejo comenzó con una simple pregunta."
    ];

    function hacerPregunta() {
      const input = document.getElementById("pregunta");
      const pregunta = input.value.trim();
      if (pregunta === "") return;

      mostrarLoader(true);
      setTimeout(() => {
        const respuesta = respuestasFilosoficas[Math.floor(Math.random() * respuestasFilosoficas.length)];
        mostrarRespuesta(respuesta);
        guardarEnHistorial(pregunta, respuesta);
        input.value = "";
        mostrarLoader(false);
      }, 800); // Simula carga
    }

    function mostrarRespuesta(texto) {
      const respuestaDiv = document.getElementById("respuesta");
      respuestaDiv.innerHTML = `<div class="fade-in">${texto}</div>`;
      respuestaDiv.scrollIntoView({ behavior: "smooth" });
    }

    function mostrarLoader(visible) {
      document.getElementById("loader").style.display = visible ? "block" : "none";
    }

    function guardarEnHistorial(pregunta, respuesta) {
      const historial = JSON.parse(localStorage.getItem("historialR1")) || [];
      historial.unshift({ pregunta, respuesta });
      localStorage.setItem("historialR1", JSON.stringify(historial));
    }

    function mostrarHistorial() {
      const historialDiv = document.getElementById("historial");
      const historial = JSON.parse(localStorage.getItem("historialR1")) || [];

      if (historial.length === 0) {
        historialDiv.innerHTML = "<p class='fade-in'>No hay historial aún.</p>";
        return;
      }

      historialDiv.innerHTML = historial.slice(0, 10).map((item, i) => `
        <div class="historial-item fade-in">
          <strong>${i + 1}. Pregunta:</strong> ${item.pregunta}<br>
          <strong>Respuesta:</strong> ${item.respuesta}
        </div>
      `).join("");
    }

    function borrarHistorial() {
      if (confirm("¿Estás seguro de que deseas borrar el historial?")) {
        localStorage.removeItem("historialR1");
        document.getElementById("historial").innerHTML = "<p class='fade-in'>Historial borrado.</p>";
      }
    }
  </script>
</body>
</html>
