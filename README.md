<!DOCTYPE html>
<html lang="es-CO">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>OVA: Estadística y Probabilidad</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        :root {
            --bg: #0B0D11;
            --surface: #151A21;
            --card: #1E2630;
            --accent: #F5A623;
            --text-primary: #F0F2F5;
            --text-secondary: #A8B2C0;
            --border: #2D3748;
        }
        body { font-family: 'Segoe UI', Arial, sans-serif; background: var(--bg); color: var(--text-primary); padding-bottom: 2rem; }
        nav {
            background: var(--surface);
            padding: 0.75rem 1.5rem;
            position: sticky;
            top: 0;
            display: flex;
            gap: 6px;
            overflow-x: auto;
            z-index: 1000;
            border-bottom: 2px solid var(--accent);
        }
        nav button {
            background: transparent;
            border: none;
            color: var(--text-secondary);
            padding: 0.6rem 1.2rem;
            cursor: pointer;
            border-radius: 40px;
            font-weight: 600;
            font-size: 0.9rem;
            white-space: nowrap;
        }
        nav button:hover { background: var(--card); color: var(--text-primary); }
        nav button.active-tab { background: var(--accent); color: var(--bg); }
        .section { display: none; padding: 2rem 1.5rem; max-width: 1000px; margin: auto; }
        .section.active { display: block; }
        .card { background: var(--card); padding: 1.8rem; border-radius: 16px; margin: 1rem 0; border: 1px solid var(--border); }
        .card h3 { color: var(--accent); margin-bottom: 0.75rem; }
        .card ul { list-style: none; padding-left: 0; }
        .card ul li { padding: 0.5rem 0 0.5rem 1.8rem; background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="%23F5A623" stroke-width="2"><polyline points="20 6 9 17 4 12"/></svg>') left center no-repeat; background-size: 1.2rem; }
        table { width: 100%; border-collapse: collapse; margin-top: 1.2rem; }
        th, td { padding: 1rem 1.2rem; text-align: left; border-bottom: 1px solid var(--border); background: var(--card); }
        th { background: var(--surface); color: var(--accent); }
        .interactive-btn {
            display: inline-block;
            background: var(--card);
            border: 1px solid var(--border);
            color: var(--text-primary);
            padding: 0.8rem 1.8rem;
            border-radius: 40px;
            font-weight: 600;
            cursor: pointer;
            margin: 0.4rem 0.4rem 0.4rem 0;
        }
        .interactive-btn:hover { background: var(--accent); color: var(--bg); }
        .interactive-btn.primary { background: var(--accent); color: var(--bg); }
        input[type="number"] {
            background: var(--surface);
            border: 1px solid var(--border);
            color: var(--text-primary);
            padding: 0.8rem 1.2rem;
            border-radius: 40px;
            font-size: 1rem;
            width: 220px;
            outline: none;
        }
        .result-box { background: var(--surface); padding: 1.2rem 1.8rem; border-radius: 16px; margin-top: 1rem; border-left: 6px solid var(--accent); }
        .grid-2 { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 1.2rem; margin-top: 0.5rem; }
        .badge { display: inline-block; background: var(--accent); color: var(--bg); font-size: 0.7rem; font-weight: 700; padding: 0.2rem 0.8rem; border-radius: 40px; }
        @media (max-width: 640px) { nav button { font-size: 0.75rem; padding: 0.4rem 0.8rem; } .section { padding: 1rem; } }
        
        /* Chat */
        #chatMessages { max-height: 350px; overflow-y: auto; }
        @keyframes dots { 0%, 20% { opacity: 0.2; } 50% { opacity: 1; } 100% { opacity: 0.2; } }
        #typingIndicator span { animation: dots 1.4s infinite; display: inline-block; }
        #typingIndicator span:nth-child(2) { animation-delay: 0.2s; }
        #typingIndicator span:nth-child(3) { animation-delay: 0.4s; }
    </style>
</head>
<body>

<nav>
    <button class="active-tab" onclick="show('inicio')">Inicio</button>
    <button onclick="show('plan')">Plan Clase</button>
    <button onclick="show('referentes')">Referentes</button>
    <button onclick="show('eval')">Evaluación</button>
    <button onclick="show('actividad')">Actividad</button>
    <button onclick="show('caso')">Caso Práctico</button>
    <button onclick="show('socratic')" style="background:var(--accent);color:var(--bg);font-weight:bold;">🤖 Tutor IA</button>
</nav>

<!-- INICIO -->
<div id="inicio" class="section active">
    <h1>📊 Estadística y Probabilidad</h1>
    <p style="font-size:1.2rem;color:var(--text-secondary);">IB <span class="badge">Apps NM</span></p>
    <div class="card">
        <h3>🎯 Competencias (MEN / IB)</h3>
        <ul>
            <li>Interpretación crítica de datos estadísticos para la toma de decisiones.</li>
            <li>Cálculo y análisis de medidas de tendencia central y dispersión.</li>
            <li>Modelación de situaciones mediante distribuciones de probabilidad.</li>
        </ul>
    </div>
</div>

<!-- PLAN -->
<div id="plan" class="section">
    <h2>📅 Plan de Clases (6 Sesiones)</h2>
    <table>
        <tr><th>Sesión</th><th>Objetivo</th></tr>
        <tr><td>1. Estadística Descriptiva</td><td>Organización y representación de datos.</td></tr>
        <tr><td>2. Medidas de Tendencia Central</td><td>Media, mediana y moda.</td></tr>
        <tr><td>3. Dispersión y Variabilidad</td><td>Rango, varianza y desviación estándar.</td></tr>
        <tr><td>4. Probabilidad Básica</td><td>Eventos y regla de Laplace.</td></tr>
        <tr><td>5. Distribución Binomial</td><td>Modelación de ensayos de Bernoulli.</td></tr>
        <tr><td>6. Distribución Normal</td><td>Curva de campana y aplicaciones.</td></tr>
    </table>
</div>

<!-- REFERENTES -->
<div id="referentes" class="section">
    <h2>🔍 Referentes Clave</h2>
    <div class="grid-2">
        <div class="card" onclick="alert('Thomas Bayes: Padre de la inferencia estadística moderna.')">
            <h3>Thomas Bayes</h3>
            <p>Teorema que actualiza probabilidades con nueva información.</p>
        </div>
        <div class="card" onclick="alert('Carl Friedrich Gauss: Desarrolló la distribución normal.')">
            <h3>Carl Friedrich Gauss</h3>
            <p>Distribución normal y método de mínimos cuadrados.</p>
        </div>
        <div class="card" onclick="alert('Karl Pearson: Pionero de la estadística aplicada.')">
            <h3>Karl Pearson</h3>
            <p>Coeficiente de correlación y prueba chi-cuadrado.</p>
        </div>
        <div class="card" onclick="alert('Florence Nightingale: Revolucionó la estadística sanitaria.')">
            <h3>Florence Nightingale</h3>
            <p>Pionera en visualización de datos y salud pública.</p>
        </div>
    </div>
</div>

<!-- EVALUACIÓN -->
<div id="eval" class="section">
    <h2>📝 Simulador de Evaluación</h2>
    <div class="card">
        <p><strong>❓ ¿Qué mide la desviación estándar?</strong></p>
        <button class="interactive-btn" onclick="alert('✅ Correcto! Mide la dispersión de los datos respecto a la media.')">📊 Dispersión</button>
        <button class="interactive-btn" onclick="alert('❌ Incorrecto.')">📈 Promedio</button>
    </div>
    <div class="card">
        <p><strong>❓ ¿Qué porcentaje de datos está a ±1σ en una distribución normal?</strong></p>
        <button class="interactive-btn" onclick="alert('❌ No.')">50%</button>
        <button class="interactive-btn" onclick="alert('✅ Correcto! El 68% de los datos está a ±1σ.')">68%</button>
        <button class="interactive-btn" onclick="alert('❌ No.')">95%</button>
    </div>
</div>

<!-- ACTIVIDAD -->
<div id="actividad" class="section">
    <h2>🧮 Calculadora de Probabilidad</h2>
    <div class="card">
        <input type="number" id="probInput" placeholder="Ej: 0.7" min="0" max="1" step="0.01">
        <button class="interactive-btn primary" onclick="calcularComplemento()">Calcular Complementario</button>
        <div id="resultadoProb" class="result-box" style="display:none;"><span id="resultadoTexto"></span></div>
    </div>
</div>

<!-- CASO -->
<div id="caso" class="section">
    <h2>🏢 Caso: Gestión de Riesgo en Seguros</h2>
    <div class="card">
        <h3>📌 Modelo para accidentes</h3>
        <button class="interactive-btn" onclick="alert('✅ Poisson es ideal para eventos raros.')">Distribución de Poisson</button>
        <button class="interactive-btn" onclick="alert('⚠️ La normal es continua.')">Distribución Normal</button>
        <button class="interactive-btn" onclick="alert('⚠️ Binomial requiere ensayos fijos.')">Distribución Binomial</button>
    </div>
</div>

<!-- TUTOR SOCRÁTICO -->
<div id="socratic" class="section">
    <h2>🤖 Tutor Socrático</h2>
    <div class="card">
        <p style="color:var(--text-secondary);">No doy respuestas directas. Te guío con preguntas para que descubras por ti mismo.</p>
        <div style="background:var(--surface);border-radius:12px;padding:15px;max-height:350px;overflow-y:auto;" id="chatContainer">
            <div id="chatMessages">
                <div style="display:flex;gap:10px;margin-bottom:10px;">
                    <div style="background:var(--accent);color:var(--bg);border-radius:50%;width:32px;height:32px;display:flex;align-items:center;justify-content:center;flex-shrink:0;">🤖</div>
                    <div style="background:var(--card);padding:10px 14px;border-radius:12px;max-width:85%;">
                        ¡Hola! ¿Sobre qué tema te gustaría reflexionar?<br>
                        <span style="font-size:0.8rem;color:var(--text-secondary);">(áreas, media, probabilidad, ecuaciones, funciones)</span>
                    </div>
                </div>
            </div>
        </div>
        <div style="display:flex;gap:10px;margin-top:10px;">
            <input type="text" id="userQuestion" placeholder="Escribe tu pregunta..." style="flex:1;padding:12px 16px;border-radius:8px;border:1px solid var(--border);background:var(--surface);color:var(--text-primary);font-size:1rem;">
            <button onclick="sendQuestion()" class="interactive-btn primary">Enviar ➤</button>
        </div>
        <div style="margin-top:8px;">
            <button onclick="addExampleQuestion()" style="background:transparent;border:none;color:var(--text-secondary);font-size:0.8rem;cursor:pointer;text-decoration:underline;">📝 Ejemplo</button>
            <button onclick="clearChat()" style="background:transparent;border:none;color:var(--text-secondary);font-size:0.8rem;cursor:pointer;text-decoration:underline;margin-left:15px;">🗑️ Limpiar</button>
        </div>
    </div>
</div>

<script>
// ---- Navegación ----
function show(id) {
    document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    document.querySelectorAll('nav button').forEach(b => b.classList.remove('active-tab'));
}

// ---- Calculadora ----
function calcularComplemento() {
    let val = parseFloat(document.getElementById('probInput').value);
    let div = document.getElementById('resultadoProb');
    let txt = document.getElementById('resultadoTexto');
    if (isNaN(val) || val < 0 || val > 1) {
        div.style.display = 'block';
        txt.innerHTML = '⚠️ Ingresa un valor entre 0 y 1.';
        return;
    }
    div.style.display = 'block';
    txt.innerHTML = `Complementario: ${(1 - val).toFixed(3)} (${((1 - val) * 100).toFixed(1)}%)`;
}

// ---- TUTOR SOCRÁTICO (NUNCA DA RESPUESTAS DIRECTAS) ----
const preguntasSocraticas = {
    'area': [
        "¿Qué figura geométrica estás analizando?",
        "¿Qué caracteriza a esa figura? ¿Cómo son sus lados?",
        "Si tuvieras que calcular su superficie, ¿qué pasos seguirías?",
        "¿Qué relación encuentras entre las medidas de la figura?",
        "¿Cómo podrías comprobar tu resultado?"
    ],
    'rectangulo': [
        "¿Qué es un rectángulo? ¿Cómo son sus lados?",
        "Si dibujas un rectángulo, ¿qué medidas necesitas?",
        "¿Cómo podrías calcular cuánto mide su superficie?",
        "¿Qué crees que pasa si multiplicas la base por la altura?"
    ],
    'media': [
        "¿Qué significa 'promedio' en tu vida diaria?",
        "Si tienes varios números, ¿cómo harías para encontrar un valor que los represente?",
        "¿Qué pasos seguirías para calcular un promedio?"
    ],
    'probabilidad': [
        "¿Qué significa que algo sea 'probable'?",
        "Si lanzas una moneda, ¿qué posibilidades hay?",
        "¿Cómo podrías medir la probabilidad de un evento?"
    ],
    'ecuacion': [
        "¿Qué significa que dos cosas sean iguales?",
        "Si tienes una balanza equilibrada, ¿qué pasa si agregas peso a un lado?",
        "¿Cómo podrías encontrar el valor de x?"
    ]
};

const preguntasGenerales = [
    "¿Qué sabes ya sobre este tema?",
    "¿Qué información tienes y qué necesitas encontrar?",
    "¿Has enfrentado un problema similar antes?",
    "¿Qué pasos crees que deberías seguir?"
];

let estadoChat = { tema: null, indice: 0 };

function detectarTema(pregunta) {
    let q = pregunta.toLowerCase();
    if (q.includes('rectángulo') || q.includes('rectangular')) return 'rectangulo';
    if (q.includes('área') || q.includes('superficie') || q.includes('perímetro')) return 'area';
    if (q.includes('media') || q.includes('promedio')) return 'media';
    if (q.includes('probabilidad') || q.includes('azar') || q.includes('posibilidad')) return 'probabilidad';
    if (q.includes('ecuación') || q.includes('despejar') || q.includes('incógnita')) return 'ecuacion';
    return null;
}

function sendQuestion() {
    let input = document.getElementById('userQuestion');
    let pregunta = input.value.trim();
    if (!pregunta) return;

    agregarMensaje('user', pregunta);
    input.value = '';

    let tema = detectarTema(pregunta);
    let respuesta = generarRespuesta(tema);

    let typingId = mostrarEscritura();
    setTimeout(() => {
        eliminarEscritura(typingId);
        agregarMensaje('bot', respuesta);
    }, 700);
}

function generarRespuesta(tema) {
    if (tema && tema !== estadoChat.tema) {
        estadoChat.tema = tema;
        estadoChat.indice = 0;
    }

    if (estadoChat.tema && preguntasSocraticas[estadoChat.tema]) {
        let preguntas = preguntasSocraticas[estadoChat.tema];
        if (estadoChat.indice < preguntas.length) {
            let p = preguntas[estadoChat.indice];
            estadoChat.indice++;
            let prefijos = ["🤔", "🧠", "💭", "🔍", "📐"];
            return `${prefijos[estadoChat.indice % prefijos.length]} ${p}`;
        } else {
            return `🌟 ¡Vas muy bien! ¿Podrías explicar con tus propias palabras lo que has entendido?`;
        }
    }

    let p = preguntasGenerales[Math.floor(Math.random() * preguntasGenerales.length)];
    return `🤔 ${p}`;
}

function agregarMensaje(sender, texto) {
    let container = document.getElementById('chatMessages');
    let div = document.createElement('div');
    if (sender === 'user') {
        div.innerHTML = `<div style="display:flex;gap:10px;margin-bottom:10px;justify-content:flex-end;">
            <div style="background:var(--accent);color:var(--bg);padding:10px 14px;border-radius:12px;max-width:85%;">${texto}</div>
            <div style="background:var(--card);border-radius:50%;width:32px;height:32px;display:flex;align-items:center;justify-content:center;flex-shrink:0;">🧑‍🎓</div>
        </div>`;
    } else {
        div.innerHTML = `<div style="display:flex;gap:10px;margin-bottom:10px;">
            <div style="background:var(--accent);color:var(--bg);border-radius:50%;width:32px;height:32px;display:flex;align-items:center;justify-content:center;flex-shrink:0;">🤖</div>
            <div style="background:var(--card);padding:10px 14px;border-radius:12px;max-width:85%;">${texto}</div>
        </div>`;
    }
    container.appendChild(div);
    document.getElementById('chatContainer').scrollTop = container.scrollHeight;
}

function mostrarEscritura() {
    let container = document.getElementById('chatMessages');
    let div = document.createElement('div');
    div.id = 'typingIndicator';
    div.innerHTML = `<div style="display:flex;gap:10px;margin-bottom:10px;">
        <div style="background:var(--accent);color:var(--bg);border-radius:50%;width:32px;height:32px;display:flex;align-items:center;justify-content:center;flex-shrink:0;">🤖</div>
        <div style="background:var(--card);padding:10px 14px;border-radius:12px;display:flex;gap:4px;align-items:center;">
            <span>●</span><span>●</span><span>●</span>
        </div>
    </div>`;
    container.appendChild(div);
    document.getElementById('chatContainer').scrollTop = container.scrollHeight;
    return 'typingIndicator';
}

function eliminarEscritura(id) {
    let el = document.getElementById(id);
    if (el) el.remove();
}

function clearChat() {
    if (!confirm('¿Limpiar chat?')) return;
    document.getElementById('chatMessages').innerHTML = `
        <div style="display:flex;gap:10px;margin-bottom:10px;">
            <div style="background:var(--accent);color:var(--bg);border-radius:50%;width:32px;height:32px;display:flex;align-items:center;justify-content:center;flex-shrink:0;">🤖</div>
            <div style="background:var(--card);padding:10px 14px;border-radius:12px;max-width:85%;">
                ¡Hola! ¿Sobre qué tema te gustaría reflexionar?<br>
                <span style="font-size:0.8rem;color:var(--text-secondary);">(áreas, media, probabilidad, ecuaciones, funciones)</span>
            </div>
        </div>
    `;
    estadoChat = { tema: null, indice: 0 };
}

function addExampleQuestion() {
    const ejemplos = [
        "¿Cómo puedo hallar el área de un rectángulo?",
        "No entiendo cómo calcular la media",
        "¿Cómo se calcula la probabilidad?",
        "¿Cómo se resuelve una ecuación?"
    ];
    document.getElementById('userQuestion').value = ejemplos[Math.floor(Math.random() * ejemplos.length)];
    sendQuestion();
}

// Enter para enviar
document.addEventListener('DOMContentLoaded', function() {
    document.getElementById('userQuestion').addEventListener('keypress', function(e) {
        if (e.key === 'Enter') sendQuestion();
    });
});
</script>
</body>
</html>
