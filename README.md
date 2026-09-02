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
<script>
    function show(id) {
        document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
        document.getElementById(id).classList.add('active');
    }
    function toggle(id) {
        let el = document.getElementById(id);
        el.style.display = (el.style.display === 'none') ? 'table-row' : 'none';
    }
    function calc() {
        let p = document.getElementById('prob').value;
        document.getElementById('res').innerText = "La probabilidad del evento complementario es: " + (1 - p);
    }
  
