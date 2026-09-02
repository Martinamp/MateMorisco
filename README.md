<!DOCTYPE html>
<html lang="es-CO">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tutor Socrático + GeoGebra | IB</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        /* ===== ESTILOS ===== */
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
            --shadow: 0 8px 32px rgba(0, 0, 0, 0.6);
            --radius: 16px;
            --transition: all 0.3s ease;
            --geogebra: #2a4a6e;
        }

        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
            background: var(--bg);
            color: var(--text-primary);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 1.5rem;
            line-height: 1.6;
        }

        .container {
            max-width: 880px;
            width: 100%;
            margin: 0 auto;
        }

        .header {
            text-align: center;
            margin-bottom: 2rem;
        }

        .header h1 {
            font-size: 2.2rem;
            font-weight: 700;
            letter-spacing: -0.02em;
            background: linear-gradient(135deg, var(--accent) 0%, #e8c84a 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .header p {
            color: var(--text-secondary);
            font-size: 1rem;
            margin-top: 0.3rem;
        }

        .badge {
            display: inline-block;
            background: var(--accent);
            color: var(--bg);
            font-size: 0.65rem;
            font-weight: 700;
            padding: 0.2rem 0.8rem;
            border-radius: 40px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            -webkit-text-fill-color: var(--bg);
        }

        .badge-geogebra {
            display: inline-block;
            background: var(--geogebra);
            color: #fff;
            font-size: 0.65rem;
            font-weight: 700;
            padding: 0.2rem 0.8rem;
            border-radius: 40px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .status-badge {
            display: inline-block;
            font-size: 0.7rem;
            padding: 0.2rem 0.8rem;
            border-radius: 40px;
            margin-left: 6px;
        }

        .status-online {
            background: #4CAF50;
            color: #fff;
        }

        .status-offline {
            background: #f44336;
            color: #fff;
        }

        .tutor-card {
            background: var(--card);
            border-radius: var(--radius);
            padding: 1.8rem;
            border: 1px solid var(--border);
            box-shadow: var(--shadow);
            transition: var(--transition);
        }

        .tutor-card:hover {
            border-color: var(--accent);
            transform: translateY(-2px);
        }

        .reglas {
            background: var(--surface);
            border-radius: 12px;
            padding: 1rem 1.4rem;
            margin-bottom: 1.5rem;
            border-left: 4px solid var(--accent);
            font-size: 0.85rem;
            color: var(--text-secondary);
        }

        .reglas strong {
            color: var(--accent);
        }

        .reglas ul {
            list-style: none;
            padding-left: 0;
            margin-top: 0.4rem;
        }

        .reglas ul li {
            padding: 0.2rem 0 0.2rem 1.6rem;
            background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="%23F5A623" stroke-width="2"><polyline points="20 6 9 17 4 12"/></svg>') left center no-repeat;
            background-size: 1rem;
        }

        .reglas .geogebra-highlight {
            background: var(--geogebra);
            color: #fff;
            padding: 0.1rem 0.6rem;
            border-radius: 40px;
            font-size: 0.75rem;
            font-weight: 600;
        }

        .geogebra-tip {
            background: var(--geogebra);
            border-radius: 8px;
            padding: 0.8rem 1.2rem;
            margin: 0.5rem 0;
            font-size: 0.9rem;
            border-left: 4px solid #6ab0e6;
        }

        .geogebra-tip strong {
            color: #6ab0e6;
        }

        .chat-container {
            background: var(--surface);
            border-radius: 12px;
            padding: 1rem;
            max-height: 420px;
            min-height: 320px;
            overflow-y: auto;
            margin: 1rem 0;
            scroll-behavior: smooth;
        }

        .chat-container::-webkit-scrollbar {
            width: 5px;
        }
        .chat-container::-webkit-scrollbar-track {
            background: var(--bg);
            border-radius: 8px;
        }
        .chat-container::-webkit-scrollbar-thumb {
            background: var(--accent);
            border-radius: 8px;
        }

        .message {
            display: flex;
            gap: 10px;
            margin-bottom: 12px;
            animation: fadeIn 0.3s ease;
        }

        .message.user {
            justify-content: flex-end;
        }

        .message .avatar {
            width: 34px;
            height: 34px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.1rem;
            flex-shrink: 0;
            background: var(--card);
        }

        .message.bot .avatar {
            background: var(--accent);
            color: var(--bg);
        }

        .message .bubble {
            padding: 10px 16px;
            border-radius: 14px;
            max-width: 85%;
            word-wrap: break-word;
            white-space: pre-wrap;
            line-height: 1.5;
            font-size: 0.95rem;
        }

        .message.user .bubble {
            background: var(--accent);
            color: var(--bg);
            border-bottom-right-radius: 4px;
        }

        .message.bot .bubble {
            background: var(--card);
            color: var(--text-primary);
            border-bottom-left-radius: 4px;
            border: 1px solid var(--border);
        }

        .message.bot .bubble strong {
            color: var(--accent);
        }

        .message.bot .bubble .geogebra-tag {
            display: inline-block;
            background: var(--geogebra);
            color: #fff;
            font-size: 0.7rem;
            padding: 2px 10px;
            border-radius: 40px;
            margin-right: 6px;
            font-weight: 600;
        }

        .message.bot .bubble .step-number {
            display: inline-block;
            background: var(--accent);
            color: var(--bg);
            font-weight: 700;
            font-size: 0.7rem;
            width: 20px;
            height: 20px;
            border-radius: 50%;
            text-align: center;
            line-height: 20px;
            margin-right: 6px;
        }

        @keyframes fadeIn {
            0% { opacity: 0; transform: translateY(8px); }
            100% { opacity: 1; transform: translateY(0); }
        }

        .typing-indicator {
            display: flex;
            gap: 10px;
            margin-bottom: 12px;
        }

        .typing-indicator .avatar {
            width: 34px;
            height: 34px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.1rem;
            flex-shrink: 0;
            background: var(--accent);
            color: var(--bg);
        }

        .typing-indicator .dots {
            background: var(--card);
            padding: 12px 18px;
            border-radius: 14px;
            border-bottom-left-radius: 4px;
            border: 1px solid var(--border);
            display: flex;
            gap: 5px;
        }

        .typing-indicator .dots span {
            display: inline-block;
            width: 8px;
            height: 8px;
            background: var(--text-secondary);
            border-radius: 50%;
            animation: typing 1.4s infinite;
        }

        .typing-indicator .dots span:nth-child(2) {
            animation-delay: 0.2s;
        }
        .typing-indicator .dots span:nth-child(3) {
            animation-delay: 0.4s;
        }

        @keyframes typing {
            0%, 60%, 100% { transform: translateY(0); opacity: 0.3; }
            30% { transform: translateY(-6px); opacity: 1; }
        }

        .input-area {
            display: flex;
            gap: 10px;
            margin-top: 0.5rem;
        }

        .input-area input {
            flex: 1;
            padding: 12px 16px;
            border-radius: 40px;
            border: 1px solid var(--border);
            background: var(--surface);
            color: var(--text-primary);
            font-family: 'Inter', sans-serif;
            font-size: 0.95rem;
            outline: none;
            transition: var(--transition);
        }

        .input-area input::placeholder {
            color: var(--text-secondary);
            opacity: 0.6;
        }

        .input-area input:focus {
            border-color: var(--accent);
            box-shadow: 0 0 0 3px rgba(245, 166, 35, 0.15);
        }

        .input-area input:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        .btn {
            padding: 12px 24px;
            border: none;
            border-radius: 40px;
            font-weight: 600;
            font-size: 0.95rem;
            cursor: pointer;
            transition: var(--transition);
            font-family: 'Inter', sans-serif;
            white-space: nowrap;
        }

        .btn-primary {
            background: var(--accent);
            color: var(--bg);
        }

        .btn-primary:hover:not(:disabled) {
            background: var(--accent-dim);
            transform: scale(1.02);
            box-shadow: 0 0 24px rgba(245, 166, 35, 0.25);
        }

        .btn-primary:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        .btn-geogebra {
            background: var(--geogebra);
            color: #fff;
        }

        .btn-geogebra:hover:not(:disabled) {
            background: #1d3a55;
            transform: scale(1.02);
        }

        .btn-geogebra:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        .btn-secondary {
            background: transparent;
            color: var(--text-secondary);
            border: 1px solid var(--border);
        }

        .btn-secondary:hover {
            background: var(--card);
            color: var(--text-primary);
        }

        .acciones {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-top: 12px;
        }

        .acciones button {
            background: transparent;
            border: none;
            color: var(--text-secondary);
            font-size: 0.8rem;
            cursor: pointer;
            text-decoration: underline;
            padding: 4px 8px;
            transition: var(--transition);
            font-family: 'Inter', sans-serif;
        }

        .acciones button:hover:not(:disabled) {
            color: var(--accent);
        }

        .acciones button:disabled {
            opacity: 0.3;
            cursor: not-allowed;
        }

        .footer {
            text-align: center;
            margin-top: 1.5rem;
            font-size: 0.75rem;
            color: var(--text-secondary);
            opacity: 0.5;
        }

        .geo-link {
            color: #6ab0e6;
            text-decoration: none;
            font-weight: 600;
        }

        .geo-link:hover {
            text-decoration: underline;
        }

        @media (max-width: 600px) {
            body { padding: 1rem; }
            .header h1 { font-size: 1.6rem; }
            .tutor-card { padding: 1.2rem; }
            .chat-container { max-height: 340px; min-height: 220px; padding: 0.8rem; }
            .input-area { flex-direction: column; }
            .input-area input { width: 100%; }
            .btn { width: 100%; text-align: center; }
            .message .bubble { font-size: 0.88rem; max-width: 90%; }
        }
    </style>
</head>
<body>

<div class="container">

    <header class="header">
        <h1>🤖 Tutor Socrático + GeoGebra</h1>
        <p>
            Matemáticas · IB <span class="badge">Apps NM</span>
            <span class="badge-geogebra">📐 Experto en GeoGebra</span>
            <span id="statusBadge" class="status-badge status-offline">⚪ Desconectado</span>
        </p>
    </header>

    <div class="tutor-card">

        <div class="reglas">
            <strong>🧠 Metodología Socrática + <span class="geogebra-highlight">📐 GeoGebra</span></strong>
            <ul>
                <li><strong>NUNCA</strong> doy respuestas directas</li>
                <li>Guío con <strong>preguntas</strong> para que descubras por ti mismo</li>
                <li>Si es necesario, te guío <strong>paso a paso en GeoGebra</strong></li>
                <li>Te doy comandos específicos para construir figuras y gráficas</li>
                <li><strong>UNA pregunta por turno</strong> (regla absoluta)</li>
            </ul>
        </div>

        <!-- Configuración API -->
        <div style="background: var(--surface); border-radius: 12px; padding: 0.8rem 1.2rem; margin-bottom: 1rem; display: flex; flex-wrap: wrap; gap: 8px; align-items: center;">
            <span style="font-size: 0.8rem; color: var(--text-secondary);">🔑 API Key:</span>
            <input type="password" id="apiKeyInput" placeholder="Pega tu clave de Gemini aquí..." 
                   style="flex: 1; min-width: 200px; padding: 6px 12px; border-radius: 40px; border: 1px solid var(--border); background: var(--bg); color: var(--text-primary); font-size: 0.8rem; outline: none;">
            <button class="btn btn-primary" id="connectBtn" onclick="connectAPI()" style="padding: 6px 18px; font-size: 0.8rem;">Conectar</button>
            <span id="connectionStatus" style="font-size: 0.75rem; color: var(--text-secondary);">⚪ Esperando conexión</span>
        </div>

        <!-- CHAT -->
        <div class="chat-container" id="chatContainer">
            <div id="chatMessages">
                <div class="message bot">
                    <div class="avatar">🤖</div>
                    <div class="bubble">
                        <strong>¡Hola!</strong> Soy tu tutor socrático experto en GeoGebra.<br><br>
                        <span class="geogebra-tag">📐 GeoGebra</span> Puedo guiarte paso a paso para construir figuras, graficar funciones y crear construcciones interactivas.<br><br>
                        <strong>Reglas:</strong>
                        <ul style="margin: 6px 0 6px 18px; color: var(--text-secondary); font-size: 0.9rem;">
                            <li>❌ No doy respuestas directas</li>
                            <li>✅ Guío con preguntas</li>
                            <li>📐 Te enseño a usar GeoGebra</li>
                            <li>🎯 Una pregunta por turno</li>
                        </ul>
                        <strong>¿Sobre qué tema te gustaría reflexionar hoy?</strong><br>
                        <span style="font-size:0.8rem;color:var(--text-secondary);">(álgebra, geometría, funciones, trigonometría, estadística, probabilidad)</span>
                    </div>
                </div>
            </div>
        </div>

        <!-- INPUT -->
        <div class="input-area">
            <input type="text" id="userQuestion" placeholder="Escribe tu pregunta o problema..." autofocus disabled>
            <button class="btn btn-primary" id="sendBtn" onclick="sendQuestion()" disabled>Enviar ➤</button>
        </div>

        <!-- ACCIONES -->
        <div class="acciones">
            <button onclick="addExample()" id="exampleBtn" disabled>📝 Ejemplo</button>
            <button onclick="addGeoGebraExample()" id="geogebraBtn" disabled>📐 GeoGebra</button>
            <button onclick="clearChat()">🗑️ Limpiar</button>
            <button onclick="openGeoGebra()" style="color: #6ab0e6; font-weight: 600;">🌐 Abrir GeoGebra</button>
        </div>

    </div>

    <div class="footer">
        Tutor Socrático · IA con Gemini · Experto en GeoGebra · Basado en el método de Sócrates
    </div>
</div>

<script>
    // ============================================================
    // TUTOR SOCRÁTICO EXPERTO EN GEOGEBRA CON GEMINI API
    // ============================================================

    // ---- ESTADO ----
    let isConnected = false;
    let apiKey = 'AQ.Ab8RN6IRQjXRQdd_Q112bgQVpKLuVwMo3aCBLKPqQHYBpmDbiA';
    let isProcessing = false;
    let chatHistory = [];
    let geogebraStep = 0;
    let currentTopic = null;

    // ---- ELEMENTOS DOM ----
    const apiKeyInput = document.getElementById('apiKeyInput');
    const connectBtn = document.getElementById('connectBtn');
    const connectionStatus = document.getElementById('connectionStatus');
    const statusBadge = document.getElementById('statusBadge');
    const userInput = document.getElementById('userQuestion');
    const sendBtn = document.getElementById('sendBtn');
    const exampleBtn = document.getElementById('exampleBtn');
    const geogebraBtn = document.getElementById('geogebraBtn');

    // ---- ABRIR GEOGEBRA ----
    function openGeoGebra() {
        window.open('https://www.geogebra.org/classic', '_blank');
        addMessage('bot', '📐 **GeoGebra abierto en una nueva pestaña.**\n\nRecuerda que puedes usar:\n- La **barra de entrada** para escribir comandos\n- Las **herramientas** de la barra lateral\n- Los **deslizadores** para explorar cambios\n\n¿Qué te gustaría construir?');
    }

    // ---- CONEXIÓN ----
    function connectAPI() {
        const key = apiKeyInput.value.trim();

        if (!key) {
            connectionStatus.textContent = '⚠️ Ingresa una API Key válida';
            connectionStatus.style.color = '#f44336';
            return;
        }

        if (!key.startsWith('AIza')) {
            connectionStatus.textContent = '⚠️ Clave inválida. Debe empezar con "AIza"';
            connectionStatus.style.color = '#f44336';
            return;
        }

        apiKey = key;
        isConnected = true;

        statusBadge.textContent = '🟢 Conectado';
        statusBadge.className = 'status-badge status-online';
        connectionStatus.textContent = '✅ Conectado a Gemini';
        connectionStatus.style.color = '#4CAF50';
        connectBtn.textContent = '✅ Conectado';
        connectBtn.style.background = '#4CAF50';
        connectBtn.style.color = '#fff';

        userInput.disabled = false;
        sendBtn.disabled = false;
        exampleBtn.disabled = false;
        geogebraBtn.disabled = false;
        userInput.focus();

        addMessage('bot', '🔌 **Conexión establecida.**\n\n📐 Recuerda: soy experto en GeoGebra. Si necesitas construir figuras o graficar funciones, te guiaré paso a paso.\n\n¿Qué tema te gustaría explorar?');
    }

    // ---- DETECTAR GEOGEBRA ----
    function detectGeoGebra(question) {
        const q = question.toLowerCase();
        const keywords = [
            'geogebra', 'graficar', 'dibujar', 'construir',
            'figura', 'triángulo', 'cuadrado', 'circunferencia', 'círculo',
            'función', 'gráfica', 'ángulo', 'polígono', 'rectángulo',
            'parábola', 'lineal', 'cuadrática', 'exponencial'
        ];
        return keywords.some(k => q.includes(k));
    }

    // ---- DETECTAR CONFUSIÓN ----
    function detectConfusion(question) {
        const q = question.toLowerCase();
        const phrases = [
            'no entiendo', 'no comprendo', 'no sé', 'no lo sé',
            'me confundo', 'estoy perdido', 'no tengo idea',
            'explicame', 'explícame', 'ayuda', 'ayúdame'
        ];
        return phrases.some(p => q.includes(p));
    }

    // ---- DETECTAR TEMA ----
    function detectTopic(question) {
        const q = question.toLowerCase();
        if (q.includes('triángulo') || q.includes('cuadrado') || q.includes('rectángulo') || q.includes('círculo') || q.includes('polígono')) return 'geometria';
        if (q.includes('función') || q.includes('gráfica') || q.includes('parábola')) return 'funciones';
        if (q.includes('seno') || q.includes('coseno') || q.includes('tangente') || q.includes('ángulo')) return 'trigonometria';
        if (q.includes('media') || q.includes('promedio') || q.includes('desviación')) return 'estadistica';
        if (q.includes('probabilidad') || q.includes('azar') || q.includes('dado')) return 'probabilidad';
        if (q.includes('ecuación') || q.includes('despejar') || q.includes('incógnita')) return 'algebra';
        return null;
    }

    // ---- FUNCIÓN PRINCIPAL ----
    async function sendQuestion() {
        const question = userInput.value.trim();

        if (!question) {
            addMessage('bot', '🤔 **Parece que no escribiste nada.**\n\n💡 Tómate un momento para pensar qué te gustaría explorar.\n\n❓ ¿Qué tema de matemáticas te gustaría reflexionar hoy?');
            return;
        }

        if (!isConnected) {
            addMessage('bot', '⚠️ **Primero debes conectar la API.**\n\nPega tu clave de Gemini en el campo de arriba y haz clic en "Conectar".');
            return;
        }

        if (isProcessing) return;

        const isGeoGebra = detectGeoGebra(question);
        const isConfused = detectConfusion(question);
        const topic = detectTopic(question);

        if (isGeoGebra) {
            geogebraStep = 0;
        }

        addMessage('user', question);
        userInput.value = '';
        isProcessing = true;
        userInput.disabled = true;
        sendBtn.disabled = true;

        const typingId = addTypingIndicator();

        try {
            const response = await callGeminiAPI(question, isConfused, isGeoGebra, topic);
            removeTypingIndicator(typingId);
            addMessage('bot', response);

            if (isGeoGebra) {
                geogebraStep++;
            }
        } catch (error) {
            removeTypingIndicator(typingId);
            console.error('Error:', error);
            addMessage('bot', '❌ **Lo siento, hubo un error.**\n\n' + error.message + '\n\nPor favor, intenta de nuevo.');
        }

        isProcessing = false;
        userInput.disabled = false;
        sendBtn.disabled = false;
        userInput.focus();
    }

    // ---- LLAMADA A LA API DE GEMINI ----
    async function callGeminiAPI(question, isConfused, isGeoGebra, topic) {
        let prompt = `Eres un tutor Socrático de matemáticas para educación secundaria. Eres también un EXPERTO en el software GeoGebra.

        TU IDENTIDAD:
        - Enseñas álgebra, geometría, funciones, trigonometría, estadística y probabilidad.
        - Eres un maestro en GeoGebra: conoces todas las herramientas, comandos y posibilidades.
        - Tu objetivo es guiar al estudiante para que desarrolle razonamiento lógico y autonomía.

        REGLAS ABSOLUTAS:
        1. NUNCA des la respuesta final a un problema.
        2. NUNCA escribas la resolución completa paso a paso.
        3. NUNCA hagas el cálculo algebraico o aritmético por el alumno.
        4. SOLO puedes hacer UNA pregunta por turno.
        5. Toda intervención debe contener: validación emocional + micro-pista + UNA pregunta guiada.

        PROTOCOLO GEOGEBRA (¡IMPORTANTE!):
        Si el problema involucra geometría, funciones, trigonometría o visualización:
        1. Guía al alumno para que ABRA GeoGebra (geogebra.org/classic)
        2. Da instrucciones ESPECÍFICAS de qué herramientas usar:
           - "Usa la herramienta 'Polígono' en la barra lateral"
           - "Escribe en la barra de entrada: f(x) = x^2"
           - "Usa la herramienta 'Deslizador' para crear un parámetro"
           - "Selecciona la herramienta 'Punto Medio' y haz clic en los puntos A y B"
        3. Da comandos EXACTOS para la barra de entrada:
           - "Escribe: Polígono(A, B, C)"
           - "Escribe: f(x) = 2*x + 3"
           - "Escribe: Circunferencia(O, radio)"
        4. Pregunta: "Si arrastras el punto A, ¿qué observas? ¿Qué propiedades se mantienen?"
        5. Guía para explorar: "Usa el deslizador para cambiar el valor de k. ¿Cómo afecta a la gráfica?"

        Si el estudiante dice "no entiendo", da un paso atrás, simplifica y valida su esfuerzo.`;

        if (isGeoGebra) {
            prompt += `

        📐 **EL ESTUDIANTE QUIERE USAR GEOGEBRA.**
        - Da instrucciones PASO A PASO.
        - Sé específico con las herramientas y comandos.
        - Pregunta qué observa al manipular la construcción.`;
        }

        if (isConfused) {
            prompt += `

        ⚠️ **EL ESTUDIANTE ESTÁ CONFUNDIDO.**
        - Valida su esfuerzo: "Es normal sentirse así, las matemáticas son desafiantes."
        - Simplifica el problema.
        - Usa una analogía de la vida cotidiana.`;
        }

        if (topic) {
            prompt += `

        TEMA DETECTADO: ${topic}
        - Adapta tus preguntas a este tema específico.
        - Si es geometría o funciones, usa GeoGebra.`;
        }

        if (chatHistory.length > 0) {
            prompt += `

        HISTORIAL DE CONVERSACIÓN:
        ${chatHistory.slice(-6).join('\n')}`;
        }

        prompt += `

        La pregunta del estudiante es: "${question}"

        Responde SIGUIENDO ESTRICTAMENTE las reglas. Solo haz UNA pregunta. NO des respuestas directas.`;

        try {
            const response = await fetch(
                `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${apiKey}`,
                {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        contents: [{ parts: [{ text: prompt }] }],
                        generationConfig: {
                            temperature: 0.8,
                            maxOutputTokens: 600,
                            topK: 1,
                            topP: 1
                        }
                    })
                }
            );

            if (!response.ok) {
                const errorData = await response.json();
                let errorMsg = 'Error en la API';
                if (errorData.error && errorData.error.message) {
                    errorMsg = errorData.error.message;
                }
                throw new Error(errorMsg);
            }

            const data = await response.json();

            if (data.candidates && data.candidates[0] && data.candidates[0].content) {
                let text = data.candidates[0].content.parts[0].text;

                text = text
                    .replace(/^Validación Emocional:\s*/gm, '')
                    .replace(/^Micro-pista:\s*/gm, '')
                    .replace(/^Pregunta:\s*/gm, '')
                    .trim();

                if (!text.includes('❓') && !text.includes('?') && !text.includes('¿')) {
                    text += '\n\n❓ ¿Qué crees que deberías hacer primero?';
                }

                chatHistory.push(`Estudiante: ${question}`);
                chatHistory.push(`Tutor: ${text.substring(0, 80)}...`);

                if (chatHistory.length > 10) {
                    chatHistory.splice(0, 2);
                }

                return text;
            } else {
                throw new Error('No se pudo obtener una respuesta de la IA.');
            }
        } catch (error) {
            if (error.message.includes('API key')) {
                throw new Error('Clave de API inválida. Verifica tu clave de Gemini.');
            }
            throw error;
        }
    }

    // ---- FUNCIONES DEL CHAT ----
    function addMessage(sender, text) {
        const container = document.getElementById('chatMessages');
        const div = document.createElement('div');
        div.className = `message ${sender}`;

        const formattedText = text
            .replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>')
            .replace(/\n/g, '<br>')
            .replace(/📐/g, '<span class="geogebra-tag">📐 GeoGebra</span>');

        if (sender === 'user') {
            div.innerHTML = `
                <div class="bubble">${formattedText}</div>
                <div class="avatar">🧑‍🎓</div>
            `;
        } else {
            div.innerHTML = `
                <div class="avatar">🤖</div>
                <div class="bubble">${formattedText}</div>
            `;
        }

        container.appendChild(div);
        scrollChatToBottom();
    }

    function addTypingIndicator() {
        const container = document.getElementById('chatMessages');
        const div = document.createElement('div');
        div.className = 'typing-indicator';
        div.id = 'typingIndicator';
        div.innerHTML = `
            <div class="avatar">🤖</div>
            <div class="dots">
                <span></span>
                <span></span>
                <span></span>
            </div>
        `;
        container.appendChild(div);
        scrollChatToBottom();
        return 'typingIndicator';
    }

    function removeTypingIndicator(id) {
        const el = document.getElementById(id);
        if (el) el.remove();
    }

    function scrollChatToBottom() {
        const container = document.getElementById('chatContainer');
        container.scrollTop = container.scrollHeight;
    }

    function clearChat() {
        if (!confirm('¿Seguro que quieres limpiar el chat?')) return;

        const container = document.getElementById('chatMessages');
        container.innerHTML = `
            <div class="message bot">
                <div class="avatar">🤖</div>
                <div class="bubble">
                    <strong>¡Hola de nuevo!</strong><br><br>
                    <span class="geogebra-tag">📐 GeoGebra</span> Recuerda que soy experto en GeoGebra. Si necesitas construir figuras o graficar funciones, te guiaré paso a paso.<br><br>
                    <strong>¿Sobre qué tema te gustaría reflexionar hoy?</strong><br>
                    <span style="font-size:0.8rem;color:var(--text-secondary);">(álgebra, geometría, funciones, trigonometría, estadística, probabilidad)</span>
                </div>
            </div>
        `;

        chatHistory = [];
        geogebraStep = 0;

        if (isConnected) {
            userInput.focus();
        }
    }

    function addExample() {
        if (!isConnected) {
            addMessage('bot', '⚠️ **Primero conecta la API.**');
            return;
        }

        const examples = [
            "¿Cómo puedo resolver una ecuación lineal?",
            "¿Cómo calculo el área de un triángulo?",
            "No entiendo cómo graficar una función cuadrática",
            "¿Cómo se usa el teorema de Pitágoras?",
            "¿Cómo calculo la media de un conjunto de datos?"
        ];
        const example = examples[Math.floor(Math.random() * examples.length)];
        userInput.value = example;
        sendQuestion();
    }

    function addGeoGebraExample() {
        if (!isConnected) {
            addMessage('bot', '⚠️ **Primero conecta la API.**');
            return;
        }

        const examples = [
            "¿Cómo puedo construir un triángulo equilátero en GeoGebra?",
            "¿Cómo grafico la función f(x)=x² en GeoGebra?",
            "¿Cómo encuentro el área de un círculo usando GeoGebra?",
            "¿Cómo construyo un rectángulo con medidas específicas en GeoGebra?"
        ];
        const example = examples[Math.floor(Math.random() * examples.length)];
        userInput.value = example;
        sendQuestion();
    }

    // ---- ENTER PARA ENVIAR ----
    document.addEventListener('DOMContentLoaded', function() {
        userInput.addEventListener('keypress', function(e) {
            if (e.key === 'Enter' && isConnected && !isProcessing) {
                e.preventDefault();
                sendQuestion();
            }
        });
    });
</script>

</body>
</html>
