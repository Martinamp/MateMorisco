[ova_estadistica.html](https://github.com/user-attachments/files/31714701/ova_estadistica.html)
<!DOCTYPE html>
<html lang="es-CO">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>OVA: Estadística y Probabilidad | IB Apps NM</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,400;14..32,600;14..32,700&display=swap" rel="stylesheet">
<style>
/* --- Reset & Variables --- */
* {
margin: 0;
padding: 0;
box-sizing: border-box;
}

:root {
--bg: #0B0D11;
--surface: #151A21;
--card: #1E2630;
--card-hover: #2A3440;
--accent: #F5A623;
--accent-dim: #c4881c;
--text-primary: #F0F2F5;
--text-secondary: #A8B2C0;
--border: #2D3748;
--shadow: 0 8px 24px rgba(0, 0, 0, 0.5);
--radius: 16px;
}

body {
font-family: 'Inter', sans-serif;
background: var(--bg);
color: var(--text-primary);
min-height: 100vh;
line-height: 1.6;
padding-bottom: 2rem;
}

/* --- Scrollbar personalizada --- */
::-webkit-scrollbar {
width: 6px;
height: 6px;
}
::-webkit-scrollbar-track {
background: var(--bg);
}
::-webkit-scrollbar-thumb {
background: var(--accent);
border-radius: 8px;
}

/* --- Navegación --- */
<nav>
    <button onclick="show('inicio')">Inicio</button>
    <button onclick="show('plan')">Plan Clase</button>
    <button onclick="show('referentes')">Referentes</button>
    <button onclick="show('eval')">Evaluación</button>
    <button onclick="show('actividad')">Actividad</button>
    <button onclick="show('caso')">Caso Práctico</button>
    <button onclick="show('socratic')" style="background: var(--accent); color: var(--bg);">🤖 Tutor IA</button>
</nav>
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
backdrop-filter: blur(6px);
flex-wrap: nowrap;
align-items: center;
scrollbar-width: thin;
scrollbar-color: var(--accent) var(--bg);
}
<nav id="mainNav">
    <button class="active-tab" data-section="inicio">Inicio</button>
    <button data-section="plan">Plan Clase</button>
    <button data-section="referentes">Referentes</button>
    <button data-section="eval">Evaluación</button>
    <button data-section="actividad">Actividad</button>
    <button data-section="caso">Caso Práctico</button>
    <button onclick="show('socratic')" style="background: var(--accent); color: var(--bg);">🤖 Tutor IA</button>  <!-- NUEVO -->
</nav>
nav button {
background: transparent;
border: none;
color: var(--text-secondary);
padding: 0.6rem 1.2rem;
cursor: pointer;
border-radius: 40px;
font-weight: 600;
font-size: 0.9rem;
transition: all 0.2s ease;
white-space: nowrap;
letter-spacing: 0.3px;
border: 1px solid transparent;
}

nav button:hover {
background: var(--card);
color: var(--text-primary);
border-color: var(--accent);
}

nav button.active-tab {
background: var(--accent);
color: var(--bg);
border-color: var(--accent);
box-shadow: 0 0 20px rgba(245, 166, 35, 0.25);
}

/* --- Secciones --- */
.section {
display: none;
padding: 2rem 1.5rem;
max-width: 1000px;
margin: 0 auto;
animation: fadeUp 0.35s ease;
}

.section.active {
display: block;
}

@keyframes fadeUp {
0% { opacity: 0; transform: translateY(16px); }
100% { opacity: 1; transform: translateY(0); }
}

/* --- Tarjetas --- */
.card {
background: var(--card);
padding: 1.8rem;
border-radius: var(--radius);
margin: 1rem 0;
border: 1px solid var(--border);
transition: all 0.25s ease;
box-shadow: var(--shadow);
}

.card:hover {
background: var(--card-hover);
border-color: var(--accent);
transform: translateY(-2px);
}

.card h3 {
color: var(--accent);
margin-bottom: 0.75rem;
font-weight: 700;
font-size: 1.3rem;
}

.card ul {
list-style: none;
padding-left: 0;
}

.card ul li {
padding: 0.5rem 0 0.5rem 1.8rem;
background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="%23F5A623" stroke-width="2"><polyline points="20 6 9 17 4 12"/></svg>') left center no-repeat;
background-size: 1.2rem;
}

/* --- Tablas --- */
table {
width: 100%;
border-collapse: separate;
border-spacing: 0;
margin-top: 1.2rem;
border-radius: var(--radius);
overflow: hidden;
box-shadow: var(--shadow);
}

th, td {
padding: 1rem 1.2rem;
text-align: left;
border-bottom: 1px solid var(--border);
background: var(--card);
transition: background 0.2s;
}

th {
background: var(--surface);
color: var(--accent);
font-weight: 700;
text-transform: uppercase;
font-size: 0.8rem;
letter-spacing: 0.5px;
border-bottom: 2px solid var(--accent);
}

tr:last-child td {
border-bottom: none;
}

tr.expandable td {
cursor: pointer;
font-weight: 600;
}

tr.expandable td:hover {
background: var(--card-hover);
}

tr.detail-row td {
background: var(--surface);
padding: 1.2rem;
font-style: italic;
color: var(--text-secondary);
border-left: 4px solid var(--accent);
}

/* --- Botones interactivos --- */
.interactive-btn {
display: inline-block;
background: var(--card);
border: 1px solid var(--border);
color: var(--text-primary);
padding: 0.8rem 1.8rem;
border-radius: 40px;
font-weight: 600;
cursor: pointer;
transition: all 0.2s;
margin: 0.4rem 0.4rem 0.4rem 0;
font-size: 0.95rem;
}

.interactive-btn:hover {
background: var(--accent);
color: var(--bg);
border-color: var(--accent);
transform: scale(1.02);
box-shadow: 0 0 20px rgba(245, 166, 35, 0.25);
}

.interactive-btn.primary {
background: var(--accent);
color: var(--bg);
border-color: var(--accent);
}

.interactive-btn.primary:hover {
background: var(--accent-dim);
border-color: var(--accent-dim);
}

/* --- Inputs --- */
input[type="number"] {
background: var(--surface);
border: 1px solid var(--border);
color: var(--text-primary);
padding: 0.8rem 1.2rem;
border-radius: 40px;
font-size: 1rem;
width: 220px;
outline: none;
transition: border 0.2s;
font-family: 'Inter', sans-serif;
}

input[type="number"]:focus {
border-color: var(--accent);
box-shadow: 0 0 0 3px rgba(245, 166, 35, 0.2);
}

.result-box {
background: var(--surface);
padding: 1.2rem 1.8rem;
border-radius: var(--radius);
margin-top: 1rem;
border-left: 6px solid var(--accent);
font-weight: 600;
font-size: 1.1rem;
}

/* --- Referentes (cards clickeables) --- */
.referente-card {
cursor: pointer;
transition: all 0.25s;
position: relative;
overflow: hidden;
}

.referente-card::after {
content: "↗";
position: absolute;
top: 1rem;
right: 1.5rem;
font-size: 1.5rem;
color: var(--accent);
opacity: 0.5;
transition: opacity 0.2s;
}

.referente-card:hover::after {
opacity: 1;
}

/* --- Grid para referentes --- */
.grid-2 {
display: grid;
grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
gap: 1.2rem;
margin-top: 0.5rem;
}

/* --- Badge --- */
.badge {
display: inline-block;
background: var(--accent);
color: var(--bg);
font-size: 0.7rem;
font-weight: 700;
padding: 0.2rem 0.8rem;
border-radius: 40px;
text-transform: uppercase;
letter-spacing: 0.5px;
margin-left: 0.5rem;
}

/* --- Responsive --- */
@media (max-width: 640px) {
nav {
padding: 0.5rem 1rem;
gap: 4px;
}
nav button {
font-size: 0.75rem;
padding: 0.4rem 0.8rem;
}
.section {
padding: 1rem;
}
.card {
padding: 1.2rem;
}
th, td {
padding: 0.6rem 0.8rem;
font-size: 0.9rem;
}
input[type="number"] {
width: 100%;
max-width: 280px;
}
}
</style>
</head>
<body>

<!-- ==================== NAVEGACIÓN ==================== -->
<nav id="mainNav">
<button class="active-tab" data-section="inicio">Inicio</button>
<button data-section="plan">Plan Clase</button>
<button data-section="referentes">Referentes</button>
<button data-section="eval">Evaluación</button>
<button data-section="actividad">Actividad</button>
<button data-section="caso">Caso Práctico</button>
</nav>

<!-- ==================== SECCIONES ==================== -->

<!-- --- INICIO --- -->
<div id="inicio" class="section active">
<h1 style="font-size: 2.5rem; font-weight: 700; letter-spacing: -0.02em; margin-bottom: 0.25rem;">
📊 Estadística y Probabilidad
</h1>
<p style="font-size: 1.2rem; color: var(--text-secondary); margin-bottom: 1.5rem;">
IB <span class="badge">Apps NM</span> — Pensamiento estadístico aplicado al mundo real.
</p>
<div class="card">
<h3>🎯 Competencias (MEN / IB)</h3>
<ul>
<li>Interpretación crítica de datos estadísticos para la toma de decisiones.</li>
<li>Cálculo y análisis de medidas de tendencia central y dispersión.</li>
<li>Modelación de situaciones mediante distribuciones de probabilidad.</li>
<li>Uso de herramientas tecnológicas para el análisis de datos.</li>
</ul>
</div>
<div class="card" style="border-color: var(--accent); background: var(--surface);">
<p style="display: flex; align-items: center; gap: 0.8rem; flex-wrap: wrap;">
<span style="font-size: 2rem;">🧠</span>
<span><strong>Enfoque IB:</strong> Exploración, modelación y aplicación de la estadística en contextos locales y globales.</span>
</p>
</div>
</div>

<!-- --- PLAN DE CLASE --- -->
<div id="plan" class="section">
<h2>📅 Plan de Clases (6 Sesiones)</h2>
<p style="color: var(--text-secondary); margin-bottom: 1rem;">Haz clic en una fila para ver los detalles de la actividad.</p>
<table>
<thead>
<tr><th>Sesión</th><th>Objetivo</th></tr>
</thead>
<tbody>
<tr class="expandable" onclick="toggleDetail('c1')">
<td><strong>1. Estadística Descriptiva</strong></td>
<td>Organización y representación de datos.</td>
</tr>
<tr id="c1" class="detail-row" style="display:none;">
<td colspan="2">📌 <strong>Actividad:</strong> Análisis de datos masivos (encuestas reales). Uso de hojas de cálculo para construir tablas de frecuencia y gráficos.</td>
</tr>
<tr class="expandable" onclick="toggleDetail('c2')">
<td><strong>2. Medidas de Tendencia Central</strong></td>
<td>Media, mediana y moda en contextos diversos.</td>
</tr>
<tr id="c2" class="detail-row" style="display:none;">
<td colspan="2">📌 <strong>Actividad:</strong> Comparación de salarios en diferentes sectores. Debate sobre la representatividad de la media.</td>
</tr>
<tr class="expandable" onclick="toggleDetail('c3')">
<td><strong>3. Dispersión y Variabilidad</strong></td>
<td>Rango, varianza y desviación estándar.</td>
</tr>
<tr id="c3" class="detail-row" style="display:none;">
<td colspan="2">📌 <strong>Actividad:</strong> Análisis de rendimiento académico. Interpretación de la desviación estándar en calificaciones.</td>
</tr>
<tr class="expandable" onclick="toggleDetail('c4')">
<td><strong>4. Probabilidad Básica</strong></td>
<td>Eventos, espacio muestral y regla de Laplace.</td>
</tr>
<tr id="c4" class="detail-row" style="display:none;">
<td colspan="2">📌 <strong>Actividad:</strong> Simulación de lanzamiento de dados y monedas. Cálculo de probabilidades teóricas y experimentales.</td>
</tr>
<tr class="expandable" onclick="toggleDetail('c5')">
<td><strong>5. Distribución Binomial</strong></td>
<td>Modelación de ensayos de Bernoulli.</td>
</tr>
<tr id="c5" class="detail-row" style="display:none;">
<td colspan="2">📌 <strong>Actividad:</strong> Control de calidad en una fábrica. Cálculo de probabilidad de piezas defectuosas.</td>
</tr>
<tr class="expandable" onclick="toggleDetail('c6')">
<td><strong>6. Distribución Normal</strong></td>
<td>Curva de campana y aplicaciones.</td>
</tr>
<tr id="c6" class="detail-row" style="display:none;">
<td colspan="2">📌 <strong>Actividad:</strong> Estudio de estaturas en una población. Uso de la regla 68-95-99.7.</td>
</tr>
</tbody>
</table>
</div>

<!-- --- REFERENTES --- -->
<div id="referentes" class="section">
<h2>🔍 Referentes Clave</h2>
<p style="color: var(--text-secondary); margin-bottom: 1.2rem;">Haz clic en cada tarjeta para conocer más sobre su legado.</p>
<div class="grid-2">
<div class="card referente-card" onclick="mostrarReferente('bayes')">
<h3>Thomas Bayes <span style="font-size: 0.8rem; color: var(--text-secondary);">(1701–1761)</span></h3>
<p>Padre de la inferencia estadística moderna. Su teorema permite actualizar probabilidades con nueva información, pilar de la IA.</p>
</div>
<div class="card referente-card" onclick="mostrarReferente('gauss')">
<h3>Carl Friedrich Gauss <span style="font-size: 0.8rem; color: var(--text-secondary);">(1777–1855)</span></h3>
<p>Desarrolló la distribución normal y el método de mínimos cuadrados, fundamentales en estadística y ciencias.</p>
</div>
<div class="card referente-card" onclick="mostrarReferente('pearson')">
<h3>Karl Pearson <span style="font-size: 0.8rem; color: var(--text-secondary);">(1857–1936)</span></h3>
<p>Pionero de la estadística aplicada. Introdujo el coeficiente de correlación y la prueba chi-cuadrado.</p>
</div>
<div class="card referente-card" onclick="mostrarReferente('nightingale')">
<h3>Florence Nightingale <span style="font-size: 0.8rem; color: var(--text-secondary);">(1820–1910)</span></h3>
<p>Revolucionó la estadística sanitaria con el uso de gráficos para comunicar datos y salvar vidas.</p>
</div>
</div>
<div id="referenteInfo" class="card" style="border-left: 6px solid var(--accent); background: var(--surface); display: none;">
<p id="referenteTexto" style="font-size: 1.05rem;">👤 Información del referente aparecerá aquí.</p>
</div>
</div>

<!-- --- EVALUACIÓN --- -->
<div id="eval" class="section">
<h2>📝 Simulador de Evaluación</h2>
<p style="color: var(--text-secondary);">Pon a prueba tus conocimientos con estas preguntas estilo IB.</p>
<div class="card">
<div id="quizContainer">
<p style="font-weight: 600; font-size: 1.1rem;">❓ Pregunta 1: ¿Qué mide la desviación estándar?</p>
<div style="display: flex; flex-wrap: wrap; gap: 0.8rem; margin-top: 0.8rem;">
<button class="interactive-btn" onclick="responderQuiz(true, '¡Correcto! La desviación estándar mide la dispersión de los datos respecto a la media.')">📊 Dispersión</button>
<button class="interactive-btn" onclick="responderQuiz(false, 'Incorrecto. La desviación estándar no mide el promedio, sino la variabilidad.')">📈 Promedio</button>
<button class="interactive-btn" onclick="responderQuiz(false, 'Incorrecto. La desviación estándar mide dispersión, no el valor central.')">🎯 Mediana</button>
</div>
<div id="quizFeedback" style="margin-top: 1.2rem; padding: 0.8rem 1.2rem; border-radius: 12px; background: var(--surface); border-left: 6px solid var(--accent); display: none;"></div>
</div>
</div>
<div class="card">
<p style="font-weight: 600; font-size: 1.1rem;">❓ Pregunta 2: En una distribución normal, ¿qué porcentaje de datos se encuentra dentro de una desviación estándar de la media?</p>
<div style="display: flex; flex-wrap: wrap; gap: 0.8rem; margin-top: 0.8rem;">
<button class="interactive-btn" onclick="responderQuiz2(false, 'No, en una distribución normal el 68% está a ±1σ.')">50%</button>
<button class="interactive-btn" onclick="responderQuiz2(true, '¡Correcto! Aproximadamente el 68% de los datos está a una desviación estándar de la media (regla 68-95-99.7).')">68%</button>
<button class="interactive-btn" onclick="responderQuiz2(false, 'No, 95% corresponde a ±2σ.')">95%</button>
</div>
<div id="quizFeedback2" style="margin-top: 1.2rem; padding: 0.8rem 1.2rem; border-radius: 12px; background: var(--surface); border-left: 6px solid var(--accent); display: none;"></div>
</div>
</div>

<!-- --- ACTIVIDAD (Calculadora) --- -->
<div id="actividad" class="section">
<h2>🧮 Calculadora de Probabilidad</h2>
<p style="color: var(--text-secondary);">Ingresa la probabilidad de un evento (entre 0 y 1) y calcula su complementario.</p>
<div class="card">
<div style="display: flex; flex-wrap: wrap; gap: 1rem; align-items: center;">
<input type="number" id="probInput" placeholder="Ej: 0.7" min="0" max="1" step="0.01">
<button class="interactive-btn primary" onclick="calcularComplemento()">Calcular Complementario</button>
</div>
<div id="resultadoProb" class="result-box" style="display: none;">
<span id="resultadoTexto"></span>
</div>
<div style="margin-top: 1.2rem; display: flex; flex-wrap: wrap; gap: 0.8rem;">
<button class="interactive-btn" onclick="ejemploProb(0.3)">🎲 Ejemplo: P(éxito)=0.3</button>
<button class="interactive-btn" onclick="ejemploProb(0.85)">🏀 Ejemplo: P(anotar)=0.85</button>
</div>
</div>
</div>

<!-- --- CASO PRÁCTICO --- -->
<div id="caso" class="section">
<h2>🏢 Caso: Gestión de Riesgo en Seguros</h2>
<p style="color: var(--text-secondary);">Una aseguradora quiere predecir la frecuencia de accidentes para fijar primas justas.</p>
<div class="card">
<h3>📌 Paso 1: Selección del modelo</h3>
<p>¿Qué modelo estadístico usarías para modelar el número de accidentes por semana?</p>
<div style="display: flex; flex-wrap: wrap; gap: 0.8rem; margin-top: 0.8rem;">
<button class="interactive-btn" onclick="casoRespuesta('Distribución de Poisson', '✅ Excelente. La distribución de Poisson es ideal para contar eventos raros en un intervalo fijo.')">📊 Distribución de Poisson</button>
<button class="interactive-btn" onclick="casoRespuesta('Distribución Normal', '⚠️ La normal es continua y simétrica, pero para conteos de accidentes (discretos) es mejor Poisson o binomial.')">📈 Distribución Normal</button>
<button class="interactive-btn" onclick="casoRespuesta('Distribución Binomial', '🤔 Binomial requiere un número fijo de ensayos. Para accidentes en tiempo continuo, Poisson es más adecuado.')">🎯 Distribución Binomial</button>
</div>
<div id="casoFeedback" class="result-box" style="display: none; margin-top: 1.2rem;"></div>
</div>
<div class="card">
<h3>📌 Paso 2: Análisis de datos históricos</h3>
<p>La aseguradora tiene registros: promedio de 3 accidentes por semana. ¿Cuál es la probabilidad de que ocurran exactamente 2 accidentes en una semana?</p>
<button class="interactive-btn primary" onclick="casoPoisson()">Calcular con Poisson (λ=3, k=2)</button>
<div id="poissonResult" class="result-box" style="display: none; margin-top: 1rem;"></div>
</div>
</div>
**<!-- ==================== AGENTE SOCRÁTICO ==================== -->
<div id="socratic" class="section">
    <h2>🤖 Tutor Socrático de Matemáticas</h2>
    <div class="card">
        <p style="color: var(--text-secondary);">
            Este tutor no te dará respuestas directas. En su lugar, te guiará con preguntas 
            para que descubras las soluciones por ti mismo. ¡Así es como realmente se aprende!
        </p>
        
        <div style="margin: 15px 0;">
            <div style="background: var(--surface); border-radius: 12px; padding: 15px; max-height: 350px; overflow-y: auto;" id="chatContainer">
                <div id="chatMessages">
                    <div class="message bot" style="display: flex; gap: 10px; margin-bottom: 10px;">
                        <div style="background: var(--accent); color: var(--bg); border-radius: 50%; width: 32px; height: 32px; display: flex; align-items: center; justify-content: center; flex-shrink: 0;">🤖</div>
                        <div style="background: var(--card); padding: 10px 14px; border-radius: 12px; max-width: 85%;">
                            ¡Hola! Soy tu tutor socrático. No te daré respuestas directas, pero te haré preguntas para que tú mismo descubras las soluciones. 
                            <br><br>
                            <strong>¿Sobre qué tema te gustaría reflexionar hoy?</strong> 
                            <span style="display: block; font-size: 0.8rem; color: var(--text-secondary); margin-top: 4px;">(álgebra, geometría, funciones, trigonometría, estadística, probabilidad)</span>
                        </div>
                    </div>
                </div>
            </div>
            
            <div style="display: flex; gap: 10px; margin-top: 10px;">
                <input type="text" id="userQuestion" placeholder="Escribe tu pregunta o problema..." 
                       style="flex: 1; padding: 12px 16px; border-radius: 8px; border: 1px solid var(--border); background: var(--surface); color: var(--text); font-family: inherit; font-size: 1rem;">
                <button onclick="sendSocraticQuestion()" class="interactive-btn primary" style="white-space: nowrap;">Enviar ➤</button>
            </div>
            
            <div style="margin-top: 8px;">
                <button onclick="addExample()" style="background: transparent; border: none; color: var(--text-secondary); font-size: 0.8rem; cursor: pointer; text-decoration: underline;">
                    📝 Probar con un ejemplo
                </button>
                <button onclick="clearChat()" style="background: transparent; border: none; color: var(--text-secondary); font-size: 0.8rem; cursor: pointer; text-decoration: underline; margin-left: 15px;">
                    🗑️ Limpiar chat
                </button>
            </div>
        </div>
        
        <div style="background: var(--surface); border-radius: 8px; padding: 12px; border-left: 4px solid var(--accent);">
            <p style="font-size: 0.85rem; color: var(--text-secondary); margin: 0;">
                💡 <strong>Consejo:</strong> Este tutor sigue el método socrático. No te dará respuestas directas, 
                sino que te guiará con preguntas para que desarrolles tu propio razonamiento.
            </p>
        </div>
    </div>
</div>**
// ============================================================
// AGENTE SOCRÁTICO - Tutor de Matemáticas
// Basado en el prompt de identidad y rol
// ============================================================

// ---- Respuestas socráticas predefinidas (para versión sin API) ----
const socraticResponses = {
    // Respuestas para temas específicos
    'estadistica': {
        validation: "¡Excelente pregunta! La estadística puede parecer compleja al principio, pero es una herramienta muy poderosa.",
        hint: "Piensa en la estadística como una forma de resumir mucha información en números que nos cuentan una historia.",
        question: "¿Qué crees que representa la media aritmética de un conjunto de datos en la vida real?"
    },
    'probabilidad': {
        validation: "¡La probabilidad es fascinante! Es la forma que tenemos de medir la incertidumbre.",
        hint: "Imagina que lanzas una moneda al aire. ¿Qué posibilidades hay de que caiga cara?",
        question: "¿Por qué crees que la probabilidad siempre está entre 0 y 1?"
    },
    'geometria': {
        validation: "La geometría está en todas partes, desde un edificio hasta un videojuego.",
        hint: "Cuando veas una figura geométrica, pregúntate: ¿qué forma tiene? ¿Qué propiedades tiene?",
        question: "Si tienes un triángulo, ¿qué relación hay entre sus ángulos internos?"
    },
    'funciones': {
        validation: "Las funciones son como máquinas: reciben algo y devuelven algo transformado.",
        hint: "Piensa en una función como una receta de cocina: ingredientes (entrada) → proceso → plato (salida).",
        question: "¿Qué significa que una función sea 'lineal'? ¿Cómo se ve en una gráfica?"
    },
    'trigonometria': {
        validation: "La trigonometría puede parecer difícil, pero es solo la relación entre los lados y ángulos de un triángulo.",
        hint: "El seno, coseno y tangente son como 'recetas' para encontrar medidas que no vemos directamente.",
        question: "¿Qué relación crees que hay entre el seno y el coseno de un mismo ángulo?"
    },
    'algebra': {
        validation: "El álgebra es como un juego de misterio donde tienes que encontrar el valor de la incógnita.",
        hint: "Piensa en la ecuación como una balanza: lo que hagas de un lado, debes hacerlo del otro para mantener el equilibrio.",
        question: "¿Qué significa 'despejar' una variable en una ecuación?"
    }
};

// ---- Respuestas por defecto (cuando no reconoce el tema) ----
const defaultResponses = [
    {
        validation: "¡Me encanta tu curiosidad! Esa es la primera habilidad de un buen matemático.",
        hint: "A veces, el primer paso es entender qué nos están pidiendo realmente.",
        question: "¿Podrías explicarme con tus propias palabras qué crees que te pide el problema?"
    },
    {
        validation: "Es normal sentirse perdido al principio. Hasta los matemáticos más grandes empezaron desde cero.",
        hint: "Divide el problema en partes más pequeñas. Resuelve lo que puedas y ve paso a paso.",
        question: "¿Cuál crees que sería el primer paso para resolver este problema?"
    },
    {
        validation: "¡Bien! Ya estás pensando como un matemático. El error es parte del proceso.",
        hint: "Pregúntate: ¿qué información tengo y qué necesito encontrar?",
        question: "¿Qué herramientas o fórmulas crees que podrían ayudarte aquí?"
    }
];

// ---- Estado del chat ----
let currentTopic = null;
let messageCount = 0;
let waitingForAnswer = false;
let lastQuestion = '';

// ---- Función para enviar pregunta ----
function sendSocraticQuestion() {
    const input = document.getElementById('userQuestion');
    const question = input.value.trim();
    if (!question) return;

    // Agregar mensaje del usuario
    addMessage('user', question);
    input.value = '';
    messageCount++;

    // Determinar el tema de la pregunta
    const topic = detectTopic(question);
    currentTopic = topic;

    // Obtener respuesta socrática
    let response = getSocraticResponse(question, topic);
    
    // Mostrar "escribiendo..." y luego la respuesta
    const typingId = addTypingIndicator();
    setTimeout(() => {
        removeTypingIndicator(typingId);
        addMessage('bot', response);
    }, 1200 + Math.random() * 800);
}

// ---- Detectar tema de la pregunta ----
function detectTopic(question) {
    const q = question.toLowerCase();
    if (q.includes('estad') || q.includes('media') || q.includes('desviación') || q.includes('dato')) return 'estadistica';
    if (q.includes('prob') || q.includes('azar') || q.includes('moneda') || q.includes('dado') || q.includes('posibilidad')) return 'probabilidad';
    if (q.includes('geomet') || q.includes('triáng') || q.includes('cuadrado') || q.includes('círculo') || q.includes('ángulo') || q.includes('perímetro') || q.includes('área')) return 'geometria';
    if (q.includes('funci') || q.includes('gráfica') || q.includes('pendiente') || q.includes('dominio') || q.includes('rango')) return 'funciones';
    if (q.includes('trig') || q.includes('sen') || q.includes('cos') || q.includes('tan') || q.includes('sec') || q.includes('csc') || q.includes('cot')) return 'trigonometria';
    if (q.includes('álgebra') || q.includes('ecuación') || q.includes('variable') || q.includes('despejar') || q.includes('incógnita') || q.includes('x')) return 'algebra';
    return null;
}

// ---- Obtener respuesta socrática ----
function getSocraticResponse(question, topic) {
    // Si reconoce el tema, usa la respuesta específica
    if (topic && socraticResponses[topic]) {
        const r = socraticResponses[topic];
        // A veces usamos respuestas diferentes para no repetir
        const variations = [
            `${r.validation}\n\n💡 ${r.hint}\n\n❓ ${r.question}`,
            `${r.validation}\n\n🔍 ${r.hint}\n\n🎯 ${r.question}`,
            `${r.validation}\n\n🤔 ${r.hint}\n\n📝 ${r.question}`
        ];
        return variations[Math.floor(Math.random() * variations.length)];
    }
    
    // Si no reconoce el tema o ya hay muchas preguntas, usa respuestas más generales
    if (messageCount > 3) {
        const advancedResponses = [
            "✅ ¡Vas muy bien! Sigamos profundizando.\n\n💡 Piensa en cómo este concepto se relaciona con otros que ya has aprendido.\n\n❓ ¿Puedes encontrar una conexión entre lo que estás estudiando y algo que ya sabías?",
            "🌟 Excelente progreso. La práctica hace al maestro.\n\n💡 A veces, cambiar la perspectiva ayuda a ver soluciones que antes no veíamos.\n\n❓ Si tuvieras que explicar esto a un amigo, ¿cómo lo harías?",
            "🧠 Estás desarrollando un pensamiento matemático muy sólido.\n\n💡 Las matemáticas no son solo números, son formas de pensar y resolver problemas.\n\n❓ ¿Qué patrones o regularidades estás observando en este problema?"
        ];
        return advancedResponses[Math.floor(Math.random() * advancedResponses.length)];
    }
    
    // Respuesta por defecto
    const defaultRes = defaultResponses[Math.floor(Math.random() * defaultResponses.length)];
    return `${defaultRes.validation}\n\n💡 ${defaultRes.hint}\n\n❓ ${defaultRes.question}`;
}

// ---- Agregar mensaje al chat ----
function addMessage(sender, text) {
    const container = document.getElementById('chatMessages');
    const div = document.createElement('div');
    div.className = `message ${sender}`;
    
    if (sender === 'user') {
        div.innerHTML = `
            <div style="display: flex; gap: 10px; margin-bottom: 10px; justify-content: flex-end;">
                <div style="background: var(--accent); color: var(--bg); padding: 10px 14px; border-radius: 12px; max-width: 85%; white-space: pre-wrap;">
                    ${text}
                </div>
                <div style="background: var(--card); border-radius: 50%; width: 32px; height: 32px; display: flex; align-items: center; justify-content: center; flex-shrink: 0;">🧑‍🎓</div>
            </div>
        `;
    } else {
        // Procesar texto con formato (negritas, saltos de línea)
        const formattedText = text
            .replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>')
            .replace(/\n/g, '<br>');
        
        div.innerHTML = `
            <div style="display: flex; gap: 10px; margin-bottom: 10px;">
                <div style="background: var(--accent); color: var(--bg); border-radius: 50%; width: 32px; height: 32px; display: flex; align-items: center; justify-content: center; flex-shrink: 0;">🤖</div>
                <div style="background: var(--card); padding: 10px 14px; border-radius: 12px; max-width: 85%; white-space: pre-wrap;">
                    ${formattedText}
                </div>
            </div>
        `;
    }
    
    container.appendChild(div);
    scrollChatToBottom();
}

// ---- Agregar indicador de escritura ----
function addTypingIndicator() {
    const container = document.getElementById('chatMessages');
    const div = document.createElement('div');
    div.id = 'typingIndicator';
    div.innerHTML = `
        <div style="display: flex; gap: 10px; margin-bottom: 10px;">
            <div style="background: var(--accent); color: var(--bg); border-radius: 50%; width: 32px; height: 32px; display: flex; align-items: center; justify-content: center; flex-shrink: 0;">🤖</div>
            <div style="background: var(--card); padding: 10px 14px; border-radius: 12px; display: flex; gap: 4px; align-items: center;">
                <span style="animation: dots 1.4s infinite;">●</span>
                <span style="animation: dots 1.4s infinite 0.2s;">●</span>
                <span style="animation: dots 1.4s infinite 0.4s;">●</span>
            </div>
        </div>
    `;
    container.appendChild(div);
    scrollChatToBottom();
    return 'typingIndicator';
}

// ---- Eliminar indicador de escritura ----
function removeTypingIndicator(id) {
    const el = document.getElementById(id);
    if (el) el.remove();
}

// ---- Scroll al final del chat ----
function scrollChatToBottom() {
    const container = document.getElementById('chatContainer');
    container.scrollTop = container.scrollHeight;
}

// ---- Limpiar chat ----
function clearChat() {
    if (confirm('¿Seguro que quieres limpiar el chat?')) {
        const container = document.getElementById('chatMessages');
        container.innerHTML = `
            <div class="message bot" style="display: flex; gap: 10px; margin-bottom: 10px;">
                <div style="background: var(--accent); color: var(--bg); border-radius: 50%; width: 32px; height: 32px; display: flex; align-items: center; justify-content: center; flex-shrink: 0;">🤖</div>
                <div style="background: var(--card); padding: 10px 14px; border-radius: 12px; max-width: 85%;">
                    ¡Hola de nuevo! ¿Sobre qué tema te gustaría reflexionar hoy?<br>
                    <span style="display: block; font-size: 0.8rem; color: var(--text-secondary); margin-top: 4px;">(álgebra, geometría, funciones, trigonometría, estadística, probabilidad)</span>
                </div>
            </div>
        `;
        messageCount = 0;
        currentTopic = null;
    }
}

// ---- Ejemplos para probar ----
function addExample() {
    const examples = [
        "No entiendo cómo calcular la media de un conjunto de datos",
        "¿Cómo se calcula la probabilidad de que salga un 6 al lanzar un dado?",
        "¿Qué es el teorema de Pitágoras y para qué sirve?",
        "¿Cómo se resuelve una ecuación lineal?",
        "No entiendo cómo graficar una función cuadrática",
        "¿Cómo se usa la trigonometría en la vida real?"
    ];
    const example = examples[Math.floor(Math.random() * examples.length)];
    document.getElementById('userQuestion').value = example;
    sendSocraticQuestion();
}

// ---- Agregar estilos CSS para animación de dots ----
const style = document.createElement('style');
style.textContent = `
    @keyframes dots {
        0%, 20% { opacity: 0.2; }
        50% { opacity: 1; }
        100% { opacity: 0.2; }
    }
`;
document.head.appendChild(style);

// ---- Permitir enviar con Enter ----
document.addEventListener('DOMContentLoaded', function() {
    const input = document.getElementById('userQuestion');
    if (input) {
        input.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                sendSocraticQuestion();
            }
        });
    }
});
<!-- ==================== SCRIPTS ==================== -->
<script>
// ---- Navegación ----
document.querySelectorAll('#mainNav button').forEach(btn => {
btn.addEventListener('click', function() {
// Remover active de todos los botones
document.querySelectorAll('#mainNav button').forEach(b => b.classList.remove('active-tab'));
this.classList.add('active-tab');
// Mostrar sección
const sectionId = this.dataset.section;
document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
document.getElementById(sectionId).classList.add('active');
});
});

// ---- Toggle detalles de tabla ----
function toggleDetail(id) {
const row = document.getElementById(id);
if (row.style.display === 'none' || row.style.display === '') {
row.style.display = 'table-row';
} else {
row.style.display = 'none';
}
}

// ---- Referentes ----
const referentesInfo = {
bayes: '👤 <strong>Thomas Bayes</strong> (1701–1761): Clérigo y matemático británico. Su famoso teorema permite actualizar la probabilidad de una hipótesis a medida que se obtiene nueva evidencia. Es la base de la inferencia bayesiana, usada hoy en IA, machine learning y filtros de spam.',
gauss: '👤 <strong>Carl Friedrich Gauss</strong> (1777–1855): Matemático alemán, "príncipe de las matemáticas". Desarrolló la distribución normal (campana de Gauss) y el método de mínimos cuadrados, esenciales en estadística, física y ciencias sociales.',
pearson: '👤 <strong>Karl Pearson</strong> (1857–1936): Estadístico británico, fundador de la estadística matemática moderna. Introdujo el coeficiente de correlación de Pearson, la prueba chi-cuadrado y el concepto de desviación estándar.',
nightingale: '👤 <strong>Florence Nightingale</strong> (1820–1910): Enfermera y estadística británica. Pionera en la visualización de datos, usó gráficos de rosa (polar) para mostrar las causas de mortalidad en la guerra de Crimea, revolucionando la salud pública.'
};

function mostrarReferente(key) {
const infoDiv = document.getElementById('referenteInfo');
const texto = document.getElementById('referenteTexto');
if (referentesInfo[key]) {
texto.innerHTML = referentesInfo[key];
infoDiv.style.display = 'block';
}
}

// ---- Quiz 1 ----
function responderQuiz(acierto, mensaje) {
const feedback = document.getElementById('quizFeedback');
feedback.style.display = 'block';
feedback.style.borderLeftColor = acierto ? '#4CAF50' : '#f44336';
feedback.innerHTML = acierto ? '✅ ' + mensaje : '❌ ' + mensaje;
// Deshabilitar botones (opcional)
const container = document.getElementById('quizContainer');
const btns = container.querySelectorAll('.interactive-btn');
btns.forEach(b => b.disabled = true);
}

// ---- Quiz 2 ----
function responderQuiz2(acierto, mensaje) {
const feedback = document.getElementById('quizFeedback2');
feedback.style.display = 'block';
feedback.style.borderLeftColor = acierto ? '#4CAF50' : '#f44336';
feedback.innerHTML = acierto ? '✅ ' + mensaje : '❌ ' + mensaje;
const container = document.getElementById('eval');
const btns = container.querySelectorAll('.card:last-child .interactive-btn');
btns.forEach(b => b.disabled = true);
}

// ---- Calculadora de Probabilidad ----
function calcularComplemento() {
const input = document.getElementById('probInput');
const val = parseFloat(input.value);
const resultDiv = document.getElementById('resultadoProb');
const textSpan = document.getElementById('resultadoTexto');

if (isNaN(val) || val < 0 || val > 1) {
resultDiv.style.display = 'block';
textSpan.innerHTML = '⚠️ Ingresa un valor entre 0 y 1.';
resultDiv.style.borderLeftColor = '#f44336';
return;
}

const complemento = 1 - val;
resultDiv.style.display = 'block';
resultDiv.style.borderLeftColor = '#4CAF50';
textSpan.innerHTML = `P(evento) = ${val.toFixed(3)} → P(complementario) = ${complemento.toFixed(3)} (${(complemento * 100).toFixed(1)}%)`;
}

function ejemploProb(val) {
document.getElementById('probInput').value = val;
calcularComplemento();
}

// ---- Caso Práctico ----
function casoRespuesta(modelo, mensaje) {
const feedback = document.getElementById('casoFeedback');
feedback.style.display = 'block';
feedback.innerHTML = `📌 <strong>${modelo}</strong><br>${mensaje}`;
if (modelo === 'Distribución de Poisson') {
feedback.style.borderLeftColor = '#4CAF50';
} else {
feedback.style.borderLeftColor = '#f44336';
}
}

function casoPoisson() {
// P(X=k) = (e^-λ * λ^k) / k! con λ=3, k=2
const lambda = 3;
const k = 2;
const e = Math.exp(1);
const prob = (Math.pow(e, -lambda) * Math.pow(lambda, k)) / (2 * 1); // 2! = 2
const resultDiv = document.getElementById('poissonResult');
resultDiv.style.display = 'block';
resultDiv.style.borderLeftColor = '#4CAF50';
resultDiv.innerHTML = `📊 P(X = 2) = (e⁻³ · 3²) / 2! = ${prob.toFixed(4)} → <strong>${(prob * 100).toFixed(2)}%</strong>`;
}

// ---- Inicialización: mostrar sección activa por defecto ----
document.querySelector('#mainNav button.active-tab')?.click();

// ---- [Mejora] Permitir que los botones de quiz se habiliten si se recarga ----
// (No es necesario, pero se puede resetear si se cambia de sección)
// Al cambiar de sección, no afecta a los quiz.
</script>

</body>
</html>
