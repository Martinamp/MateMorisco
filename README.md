<!DOCTYPE html>
<html lang="es-CO">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tutor Socrático con IA | IB</title>
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
            max-width: 860px;
            width: 100%;
            margin: 0 auto;
        }

        /* ===== HEADER ===== */
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

        /* ===== TARJETA PRINCIPAL ===== */
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

        /* ===== REGLAS DEL TUTOR ===== */
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

        /* ===== CHAT ===== */
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

        /* Mensajes */
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
            background: #2a4a6e;
            color: #fff;
            font-size: 0.7rem;
            padding: 2px 10px;
            border-radius: 40px;
            margin-right: 6px;
            font-weight: 600;
        }

        .message.bot .bubble .error-message {
            color: #f44336;
            font-weight: 600;
        }

        @keyframes fadeIn {
            0% { opacity: 0; transform: translateY(8px); }
            100% { opacity: 1; transform: translateY(0); }
        }

        /* Indicador de escritura */
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

        /* ===== INPUT Y BOTONES ===== */
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

        .btn-secondary {
            background: transparent;
            color: var(--text-secondary);
            border: 1px solid var(--border);
        }

        .btn-secondary:hover {
            background: var(--card);
            color: var(--text-primary);
        }

        /* ===== ACCIONES ===== */
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

        /* ===== FOOTER ===== */
        .footer {
            text-align: center;
            margin-top: 1.5rem;
            font-size: 0.75rem;
            color: var(--text-secondary);
            opacity: 0.5;
        }

        /* ===== RESPONSIVE ===== */
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

    <!-- ===== HEADER ===== -->
    <header class="header">
        <h1>🤖 Tutor Socrático con IA</h1>
        <p>
            Matemáticas · IB <span class="badge">Apps NM</span>
            <span id="statusBadge" class="status-badge status-offline">⚪ Desconectado</span>
        </p>
    </header>

    <!-- ===== TARJETA PRINCIPAL ===== -->
    <div class="tutor-card">

        <!-- Reglas del tutor -->
        <div class="reglas">
            <strong>🧠 Metodología Socrática + IA + GeoGebra</strong>
            <ul>
                <li><strong>NUNCA</strong> doy respuestas directas</li>
                <li>Guío con <strong>preguntas</strong> para que descubras por ti mismo</li>
                <li>Valido tu esfuerzo y normalizo los errores</li>
                <li><strong>UNA pregunta por turno</strong> (regla absoluta)</li>
                <li>Para geometría, funciones y visualización: te guío a construir en GeoGebra</li>
            </ul>
        </div>

        <!-- ===== CONFIGURACIÓN API ===== -->
        <div style="background: var(--surface); border-radius: 12px; padding: 0.8rem 1.2rem; margin-bottom: 1rem; display: flex; flex-wrap: wrap; gap: 8px; align-items: center;">
            <span style="font-size: 0.8rem; color: var(--text-secondary);">🔑 API Key:</span>
            <input type="password" id="apiKeyInput" placeholder="Pega tu clave de Gemini aquí..." 
                   style="flex: 1; min-width: 200px; padding: 6px 12px; border-radius: 40px; border: 1px solid var(--border); background: var(--bg); color: var(--text-primary); font-size: 0.8rem; outline: none;">
            <button class="btn btn-primary" id="connectBtn" onclick="connectAPI()" style="padding: 6px 18px; font-size: 0.8rem;">Conectar</button>
            <span id="connectionStatus" style="font-size: 0.75rem; color: var(--text-secondary);">⚪ Esperando conexión</span>
        </div>

        <!-- ===== CHAT ===== -->
        <div class="chat-container" id="chatContainer">
            <div id="chatMessages">
                <!-- Mensaje de bienvenida -->
                <div class="message bot">
                    <div class="avatar">🤖</div>
                    <div class="bubble">
                        <strong>¡Hola!</strong> Soy tu tutor socrático con IA.<br><br>
                        <strong>Reglas absolutas:</strong>
                        <ul style="margin: 6px 0 6px 18px; color: var(--text-secondary); font-size: 0.9rem;">
                            <li>❌ No doy respuestas directas</li>
                            <li>✅ Guío con preguntas</li>
                            <li>📐 Experto en GeoGebra</li>
                            <li>🎯 Una pregunta por turno</li>
                        </ul>
                        <strong>¿Sobre qué tema te gustaría reflexionar hoy?</strong><br>
                        <span style="font-size:0.8rem;color:var(--text-secondary);">(álgebra, geometría, funciones, trigonometría, estadística, probabilidad)</span>
                    </div>
                </div>
            </div>
        </div>

        <!-- ===== INPUT ===== -->
        <div class="input-area">
            <input type="text" id="userQuestion" placeholder="Escribe tu pregunta o problema..." autofocus disabled>
            <button class="btn btn-primary" id="sendBtn" onclick="sendQuestion()" disabled>Enviar ➤</button>
        </div>

        <!-- ===== ACCIONES ===== -->
        <div class="acciones">
            <button onclick="addExample()" id="exampleBtn" disabled>📝 Probar ejemplo</button>
            <button onclick="addGeoGebraExample()" id="geogebraBtn" disabled>📐 Ejemplo GeoGebra</button>
            <button onclick="clearChat()">🗑️ Limpiar chat</button>
        </div>

    </div>

    <!-- ===== FOOTER ===== -->
    <div class="footer">
        Tutor Socrático · IA con Gemini · Basado en el método de Sócrates · Experto en GeoGebra
    </div>
</div>

<!-- ===== JAVASCRIPT ===== -->
<script>
    // ============================================================
    // TUTOR SOCRÁTICO CON GEMINI API
    // ============================================================

    // ---- ESTADO ----
    let isConnected = false;
    let apiKey = '';
    let isProcessing = false;

    // ---- ELEMENTOS DOM ----
    const apiKeyInput = document.getElementById('apiKeyInput');
    const connectBtn = document.getElementById('connectBtn');
    const connectionStatus = document.getElementById('connectionStatus');
    const statusBadge = document.getElementById('statusBadge');
    const userInput = document.getElementById('userQuestion');
    const sendBtn = document.getElementById('sendBtn');
    const exampleBtn = document.getElementById('exampleBtn');
    const geogebraBtn = document.getElementById('geogebraBtn');

    // ---- CONEXIÓN A LA API ----
    function connectAPI() {
        const key = apiKeyInput.value.trim();

        if (!key) {
            connectionStatus.textContent = '⚠️ Ingresa una API Key válida';
            connectionStatus.style.color = '#f44336';
            return;
        }

        // Validar formato básico de la clave
        if (!key.startsWith('AIza')) {
            connectionStatus.textContent = '⚠️ Clave inválida. Debe empezar con "AIza"';
            connectionStatus.style.color = '#f44336';
            return;
        }

        AQ.Ab8RN6IRQjXRQdd_Q112bgQVpKLuVwMo3aCBLKPqQHYBpmDbiA = key;
        isConnected = true;

        // Actualizar UI
        statusBadge.textContent = '🟢 Conectado';
        statusBadge.className = 'status-badge status-online';
        connectionStatus.textContent = '✅ Conectado a Gemini';
        connectionStatus.style.color = '#4CAF50';
        connectBtn.textContent = '✅ Conectado';
        connectBtn.style.background = '#4CAF50';
        connectBtn.style.color = '#fff';

        // Habilitar input y botones
        userInput.disabled = false;
        sendBtn.disabled = false;
        exampleBtn.disabled = false;
        geogebraBtn.disabled = false;
        userInput.focus();

        // Mensaje de confirmación en el chat
        addMessage('bot', '🔌 **Conexión establecida con Gemini AI.**\n\nAhora puedo ayudarte con preguntas inteligentes. Recuerda: **no doy respuestas directas**, solo preguntas guía.\n\n¿Qué tema te gustaría explorar?');
    }

    // ---- FUNCIÓN PRINCIPAL PARA ENVIAR PREGUNTA ----
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

        // Mostrar pregunta del usuario
        addMessage('user', question);
        userInput.value = '';
        isProcessing = true;
        userInput.disabled = true;
        sendBtn.disabled = true;

        // Mostrar indicador de escritura
        const typingId = addTypingIndicator();

        try {
            const response = await callGeminiAPI(question);
            removeTypingIndicator(typingId);
            addMessage('bot', response);
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
    async function callGeminiAPI(question) {
        const prompt = `Eres un tutor Socrático de matemáticas para educación secundaria (álgebra, geometría, funciones, trigonometría, estadística, probabilidad). Eres también un experto maestro en el software GeoGebra.

        REGLAS ABSOLUTAS:
        1. NUNCA des la respuesta final a un problema.
        2. NUNCA escribas la resolución completa paso a paso.
        3. NUNCA hagas el cálculo algebraico o aritmético por el alumno.
        4. SOLO puedes hacer UNA pregunta por turno.
        5. Toda intervención debe contener: validación emocional + micro-pista conceptual + UNA única pregunta guiada.

        METODOLOGÍA:
        1. Validación Emocional: Si el alumno se equivoca o duda, valida su esfuerzo y normaliza el error.
        2. Micro-pista conceptual: Da una idea breve, analogía o conexión con conocimientos previos.
        3. UNA sola pregunta guiada: Clara, concreta, accionable.

        PROTOCOLO GEOGEBRA:
        Si el problema involucra geometría, trigonometría, funciones o visualización:
        - Guía al alumno para que construya la figura en GeoGebra.
        - Indica qué herramientas o comandos usar.
        - Pregunta: "Si arrastras el punto, ¿qué observas?"

        TONO: Equilibrado entre formal y cercano. Claro, paciente y motivador.

        La pregunta del estudiante es: "${question}"

        Responde SIGUIENDO ESTRICTAMENTE las reglas. Solo haz UNA pregunta. NO des respuestas directas.`;

        try {
            const response = await fetch(
                `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${apiKey}`,
                {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({
                        contents: [{
                            parts: [{
                                text: prompt
                            }]
                        }],
                        generationConfig: {
                            temperature: 0.7,
                            maxOutputTokens: 500,
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

                // Limpiar y formatear la respuesta
                text = text
                    .replace(/\*\*(.*?)\*\*/g, '**$1**')
                    .replace(/^Validación Emocional:/gm, '')
                    .replace(/^Micro-pista:/gm, '')
                    .replace(/^Pregunta:/gm, '');

                // Asegurar que tenga el formato correcto
                if (!text.includes('❓') && !text.includes('?') && !text.includes('¿')) {
                    text += '\n\n❓ ¿Qué crees que deberías hacer primero?';
                }

                return text.trim();
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
            .replace(/\n/g, '<br>');

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

    // ---- LIMPIAR CHAT ----
    function clearChat() {
        if (!confirm('¿Seguro que quieres limpiar el chat?')) return;

        const container = document.getElementById('chatMessages');
        container.innerHTML = `
            <div class="message bot">
                <div class="avatar">🤖</div>
                <div class="bubble">
                    <strong>¡Hola de nuevo!</strong><br><br>
                    <strong>Reglas absolutas:</strong>
                    <ul style="margin: 6px 0 6px 18px; color: var(--text-secondary); font-size: 0.9rem;">
                        <li>❌ No doy respuestas directas</li>
                        <li>✅ Guío con preguntas</li>
                        <li>📐 Experto en GeoGebra</li>
                        <li>🎯 Una pregunta por turno</li>
                    </ul>
                    <strong>¿Sobre qué tema te gustaría reflexionar hoy?</strong><br>
                    <span style="font-size:0.8rem;color:var(--text-secondary);">(álgebra, geometría, funciones, trigonometría, estadística, probabilidad)</span>
                </div>
            </div>
        `;

        if (isConnected) {
            userInput.focus();
        }
    }

    // ---- EJEMPLOS ----
    function addExample() {
        if (!isConnected) {
            addMessage('bot', '⚠️ **Primero conecta la API** para usar ejemplos.');
            return;
        }

        const examples = [
            "¿Cómo puedo resolver una ecuación lineal con fracciones?",
            "¿Cómo calculo el área de un triángulo si solo conozco sus lados?",
            "No entiendo cómo graficar una función cuadrática",
            "¿Cómo se usa el teorema de Pitágoras?",
            "¿Cómo calculo la media de un conjunto de datos con valores grandes?",
            "¿Cuál es la probabilidad de que salga un número par al lanzar un dado?"
        ];
        const example = examples[Math.floor(Math.random() * examples.length)];
        userInput.value = example;
        sendQuestion();
    }

    function addGeoGebraExample() {
        if (!isConnected) {
            addMessage('bot', '⚠️ **Primero conecta la API** para usar ejemplos con GeoGebra.');
            return;
        }

        const examples = [
            "¿Cómo puedo construir un triángulo equilátero en GeoGebra?",
            "¿Cómo grafico la función f(x)=x² en GeoGebra?",
            "¿Cómo encuentro el área de un círculo usando GeoGebra?"
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
