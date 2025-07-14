<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Daniel Garrido - Portfolio y Test</title>

  <!-- Font Awesome para iconos -->
  <script src="https://kit.fontawesome.com/a076d05399.js" crossorigin="anonymous"></script>

  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #e0c3fc, #8ec5fc);
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 30px;
      animation: fadeIn 2s ease;
      padding: 20px;
    }

    .container, .social-container, .test-container {
      background: white;
      border-radius: 15px;
      padding: 30px;
      max-width: 800px;
      width: 90%;
      box-shadow: 0 10px 20px rgba(0,0,0,0.2);
      text-align: center;
      animation: slideIn 1s ease;
    }

    .test-container {
      display: none; /* Oculto al inicio */
    }

    h1, h2 {
      color: #6200ee;
      margin-bottom: 20px;
    }

    p {
      margin-bottom: 30px;
      color: #555;
    }

    .buttons {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 10px;
    }

    button {
      padding: 12px 20px;
      border: none;
      border-radius: 8px;
      background-color: #6200ee;
      color: white;
      font-size: 1em;
      cursor: pointer;
      transition: transform 0.2s, background-color 0.3s;
    }

    button:hover {
      background-color: #3700b3;
      transform: scale(1.05);
    }

    button:disabled {
      background-color: #bbb;
      cursor: not-allowed;
    }

    .socials {
      display: flex;
      flex-direction: column;
      gap: 15px;
      align-items: center;
    }

    .social-link {
      display: flex;
      align-items: center;
      gap: 10px;
      text-decoration: none;
      color: #6200ee;
      font-size: 1.2em;
      transition: transform 0.2s, color 0.3s;
    }

    .social-link i {
      font-size: 1.5em;
    }

    .social-link:hover {
      color: #3700b3;
      transform: scale(1.05);
    }

    .question {
      font-size: 1.2em;
      margin-bottom: 20px;
      animation: fadeIn 1s ease;
    }

    .options {
      display: flex;
      flex-direction: column;
      gap: 10px;
      animation: fadeIn 1.5s ease;
    }

    .result {
      font-size: 1.2em;
      margin-top: 20px;
      animation: fadeIn 2s ease;
    }

    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }

    @keyframes slideIn {
      from { transform: translateY(-50px); opacity: 0; }
      to { transform: translateY(0); opacity: 1; }
    }
  </style>
</head>

<body>

  <!-- Página principal -->
  <div class="container" id="mainContainer">
    <h1>Daniel Garrido</h1>
    <p>Bienvenido a mi página personal</p>

    <div class="buttons">
      <button onclick="showTest()">Tipo Test</button>
      <button disabled>Próximamente</button>
      <button disabled>Próximamente</button>
      <button disabled>Próximamente</button>
    </div>
  </div>

  <!-- Redes sociales -->
  <div class="social-container" id="socialContainer">
    <h2>Redes Sociales</h2>
    <div class="socials">
      <a class="social-link" href="https://www.tiktok.com/@gb_danx" target="_blank">
        <i class="fab fa-tiktok"></i> TikTok
      </a>
      <a class="social-link" href="https://www.instagram.com/daniel.garkuz0" target="_blank">
        <i class="fab fa-instagram"></i> Instagram
      </a>
    </div>
  </div>

  <!-- Cuestionario Psicológico -->
  <div class="test-container" id="testContainer">
    <h1>🧠 Cuestionario Psicológico 🧠</h1>
    <div id="questionContainer"></div>

    <div class="result" id="result" style="display:none;">
      <h2>🎉 Resultado final: Eres gay 🎉</h2>
      <p>ATTE: Daniel Garrido</p>
      <button onclick="showRealResult()">Ver resultado real</button>
    </div>

    <div class="result" id="realResult" style="display:none;"></div>

    <button onclick="returnToMain()" style="margin-top: 30px;">Volver a la página principal</button>
  </div>

  <script>
    const mainContainer = document.getElementById("mainContainer");
    const socialContainer = document.getElementById("socialContainer");
    const testContainer = document.getElementById("testContainer");

    function showTest() {
      mainContainer.style.display = "none";
      socialContainer.style.display = "none";
      testContainer.style.display = "block";
      showQuestion(currentQuestion);
    }

    function returnToMain() {
      mainContainer.style.display = "block";
      socialContainer.style.display = "block";
      testContainer.style.display = "none";
      resetTest();
    }

    const questions = [
      { text: "🌳 Estás caminando por un bosque tranquilo. ¿Qué animal ves?", options: ["🐦 Pájaro", "🦊 Zorro", "🐺 Lobo"] },
      { text: "🦊 El animal se te acerca. ¿Qué haces?", options: ["💬 Hablo con él", "⬅️ Retrocedo", "🙈 Lo ignoro"] },
      { text: "🏚️ Encuentras una casa abandonada. ¿Qué haces?", options: ["🏃‍♂️ Entro a explorar", "🔄 La rodeo", "👀 La observo desde lejos"] },
      { text: "📚 Dentro hay una mesa con tres objetos. ¿Cuál tomas?", options: ["📖 Un libro", "🗝️ Una llave", "🕯️ Una vela"] },
      { text: "🏠 Subes las escaleras de la casa y oyes un ruido. ¿Cómo reaccionas?", options: ["🔎 Investigo", "🙈 Me escondo", "🏃‍♀️ Salgo corriendo"] },
      { text: "🚪 Una puerta se abre sola. ¿Qué haces?", options: ["🚶‍♂️ Entro", "🚪 La cierro", "👀 Observo desde lejos"] },
      { text: "🪞 Ves un espejo antiguo. ¿Qué haces?", options: ["👤 Me miro", "🙈 Lo ignoro", "🧣 Lo cubro"] },
      { text: "👤 Aparece una figura misteriosa. ¿Qué sientes?", options: ["🤔 Curiosidad", "😨 Miedo", "😕 Confusión"] },
      { text: "📦 La figura te entrega una caja. ¿La abres?", options: ["✅ Sí", "❌ No", "❓ Pregunto por su contenido"] },
      { text: "📜 La caja contiene una carta. ¿Qué haces?", options: ["📖 La leo", "📥 La guardo", "🗑️ La rompo"] }
      // Puedes añadir las demás preguntas largas aquí si deseas
    ];

    let currentQuestion = 0;
    const answers = [];
    const questionContainer = document.getElementById("questionContainer");
    const resultContainer = document.getElementById("result");
    const realResult = document.getElementById("realResult");

    function showQuestion(index) {
      const q = questions[index];
      questionContainer.innerHTML = `
        <div class="question">${q.text}</div>
        <div class="options">
          ${q.options.map(opt => `<button onclick="answerQuestion('${opt}')">${opt}</button>`).join('')}
        </div>
      `;
    }

    function answerQuestion(answer) {
      answers.push(answer);
      currentQuestion++;
      if (currentQuestion < questions.length) {
        showQuestion(currentQuestion);
      } else {
        questionContainer.style.display = "none";
        resultContainer.style.display = "block";
      }
    }

    function showRealResult() {
      let personality;
      const keywords = answers.join(" ");

      if (keywords.includes("Pájaro") || keywords.includes("Libro")) {
        personality = "🧠 Eres una persona introspectiva, con gran imaginación y amor por la libertad.";
      } else if (keywords.includes("Zorro") || keywords.includes("Llave")) {
        personality = "🦊 Tienes una personalidad curiosa, astuta y te gusta descubrir secretos.";
      } else if (keywords.includes("Lobo") || keywords.includes("Vela")) {
        personality = "🐺 Tu carácter es fuerte, protector y estás en búsqueda de una verdad más profunda.";
      } else {
        personality = "✨ Eres una mezcla única, compleja e interesante de emociones y pensamientos.";
      }

      realResult.innerHTML = `<h2>${personality}</h2>`;
      realResult.style.display = "block";
    }

    function resetTest() {
      currentQuestion = 0;
      answers.length = 0;
      questionContainer.style.display = "block";
      resultContainer.style.display = "none";
      realResult.style.display = "none";
    }
  </script>

</body>
</html>
