<!DOCTYPE html>
<html lang="es-CO">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tutor Socrático + GeoGebra | IB</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --bg: #0B0D11;
            --surface: #151A21;
            --card: #1E2630;
            --accent: #F5A623;
            --text-primary: #F0F2F5;
            --text-secondary: #A8B2C0;
            --border: #2D3748;
            --shadow: 0 8px 32px rgba(0, 0, 0, 0.6);
            --radius: 16px;
            --geogebra: #2a4a6e;
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

        .btn-primary:hover {
            background: #c4881c;
            transform: scale(1.02);
            box-shadow: 0 0 24px rgba(245, 166, 35, 0.25);
        }

        .btn-geogebra {
            background: var(--geogebra);
            color: #fff;
        }

        .btn-geogebra:hover {
            background: #1d3a55;
            transform: scale(1.02);
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

        .acciones button:hover {
            color: var(--accent);
        }

        .footer {
            text-align: center;
            margin-top: 1.5rem;
            font-size: 0.75rem;
            color: var(--text-secondary);
            opacity: 0.5;
        }

        .status-online {
            color: #4CAF50;
            font-weight: 600;
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
            <span class="status-online">🟢 Conectado</span>
        </p>
    </header>

    <div class="tutor-card">

        <div class="reglas">
            <strong>🧠 Metodología Socrática + 📐 GeoGebra</strong>
            <ul>
                <li><strong>NUNCA</strong> doy respuestas directas</li>
                <li>Guío con <strong>preguntas</strong> para que descubras por ti mismo</li>
                <li>Si es necesario, te guío <strong>paso a paso en GeoGebra</strong></li>
                <li>Te doy comandos específicos para construir figuras y gráficas</li>
                <li><strong>UNA pregunta por turno</strong> (regla absoluta)</li>
            </ul>
        </div>

        <div class="chat-container" id="chatContainer">
            <div id="chatMessages">
                <div class="message bot">
                    <div class="avatar">🤖</div>
                    <div class="bubble">
                        <strong>¡Hola!</strong> Soy tu tutor socrático experto en GeoGebra.<br><br>
                        <span class="geogebra-tag">📐 GeoGebra</span> Puedo guiarte paso a paso para construir figuras, graficar funciones y crear construcciones interactivas.<br><br>
                        <strong>¿Sobre qué tema te gustaría reflexionar hoy?</strong><br>
                        <span style="font-size:0.8rem;color:var(--text-secondary);">(álgebra, geometría, funciones, trigonometría, estadística, probabilidad)</span>
                    </div>
                </div>
            </div>
        </div>

        <div class="input-area">
            <input type="text" id="userQuestion" placeholder="Escribe tu pregunta o problema..." autofocus>
            <button class="btn btn-primary" onclick="sendQuestion()">Enviar ➤</button>
        </div>

        <div class="acciones">
            <button onclick="addExample()">📝 Ejemplo</button>
            <button onclick="addGeoGebraExample()">📐 GeoGebra</button>
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
    // TUTOR SOCRÁTICO EXPERTO EN GEOGEBRA
    // 🔑 CLAVE INTEGRADA - REEMPLAZA "TU_CLAVE_AQUI" CON TU CLAVE
    // ============================================================

    // ---- 🔑 PON AQUÍ TU CLAVE DE API DE GEMINI ----
    const API_KEY = 'AQ.Ab8RN6IRQjXRQdd_Q112bgQVpKLuVwMo3aCBLKPqQHYBpmDbiA';
    // =====================================================

    // ---- ESTADO ----
    let isProcessing = false;
    let chatHistory = [];
    let confusionCount = 0;

    // ---- ABRIR GEOGEBRA ----
    function openGeoGebra() {
        window.open('https://www.geogebra.org/classic', '_blank');
        addMessage('bot', '📐 **GeoGebra abierto en una nueva pestaña.**\n\nRecuerda que puedes usar:\n- La **barra de entrada** para escribir comandos\n- Las **herramientas** de la barra lateral\n- Los **deslizadores** para explorar cambios\n\n¿Qué te gustaría construir?');
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

    // ---- DETECTAR TEMA ----
    function detectTopic(question) {
        const q = question.toLowerCase();
        if (q.includes('triángulo') || q.includes('cuadrado') || q.includes('rectángulo') || q.includes('círculo') || q.includes('polígono')) return 'geometria';
        if (q.includes('función') || q.includes('gráfica') || q.includes('parábola') || q.includes('f(x)')) return 'funciones';
        if (q.includes('seno') || q.includes('coseno') || q.includes('tangente') || q.includes('ángulo')) return 'trigonometria';
        if (q.includes('media') || q.includes('promedio') || q.includes('desviación') || q.includes('dato')) return 'estadistica';
        if (q.includes('probabilidad') || q.includes('azar') || q.includes('dado') || q.includes('moneda')) return 'probabilidad';
        if (q.includes('ecuación') || q.includes('despejar') || q.includes('incógnita') || q.includes('x')) return 'algebra';
        return null;
    }

    // ---- ENVIAR PREGUNTA ----
    async function sendQuestion() {
        const input = document.getElementById('userQuestion');
        const question = input.value.trim();

        if (!question) {
            addMessage('bot', '🤔 **Parece que no escribiste nada.**\n\n💡 Tómate un momento para pensar qué te gustaría explorar.\n\n❓ ¿Qué tema de matemáticas te gustaría reflexionar hoy?');
            return;
        }

        if (isProcessing) return;

        const isConfused = detectConfusion(question);
        const isGeoGebra = detectGeoGebra(question);
        const topic = detectTopic(question);

        if (isConfused) {
            confusionCount++;
        } else {
            confusionCount = 0;
        }

        addMessage('user', question);
        input.value = '';
        isProcessing = true;
        input.disabled = true;

        const typingId = addTypingIndicator();

        try {
            const response = await callGeminiAPI(question, isConfused, isGeoGebra, topic);
            removeTypingIndicator(typingId);
            addMessage('bot', response);
        } catch (error) {
            removeTypingIndicator(typingId);
            console.error('Error:', error);
            addMessage('bot', '❌ **Lo siento, hubo un error.**\n\n' + error.message + '\n\nPor favor, intenta de nuevo.');
        }

        isProcessing = false;
        input.disabled = false;
        input.focus();
    }

    // ---- LLAMADA A LA API DE GEMINI (VERSIÓN CORREGIDA) ----
    async function callGeminiAPI(question, isConfused, isGeoGebra, topic) {
        // Verificar que la clave esté configurada
        if (!API_KEY || API_KEY === 'AQ.Ab8RN6IRQjXRQdd_Q112bgQVpKLuVwMo3aCBLKPqQHYBpmDbiA') {
            throw new Error('🔑 No se ha configurado la clave de API. Edita el código y pon tu clave en la variable API_KEY.');
        }

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
    3. Da comandos EXACTOS para la barra de entrada:
       - "Escribe: Polígono(A, B, C)"
       - "Escribe: f(x) = 2*x + 3"
       - "Escribe: Circunferencia(O, radio)"
    4. Pregunta: "Si arrastras el punto A, ¿qué observas?"`;

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
            // --- USAR EL MODELO CORRECTO: gemini-pro ---
            const response = await fetch(
                `https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent?key=${API_KEY}`,
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
                throw new Error('Clave de API inválida. Verifica tu clave en el código.');
            }
            if (error.message.includes('model')) {
                throw new Error('Error con el modelo. Intenta con: gemini-1.0-pro');
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
        confusionCount = 0;
        document.getElementById('userQuestion').focus();
    }

    function addExample() {
        const examples = [
            "¿Cómo puedo resolver una ecuación lineal con fracciones?",
            "¿Cómo calculo el área de un triángulo?",
            "No entiendo cómo graficar una función cuadrática",
            "¿Cómo se usa el teorema de Pitágoras?",
            "¿Cómo calculo la media de un conjunto de datos?"
        ];
        const example = examples[Math.floor(Math.random() * examples.length)];
        document.getElementById('userQuestion').value = example;
        sendQuestion();
    }

    function addGeoGebraExample() {
        const examples = [
            "¿Cómo puedo construir un triángulo equilátero en GeoGebra?",
            "¿Cómo grafico la función f(x)=x² en GeoGebra?",
            "¿Cómo encuentro el área de un círculo usando GeoGebra?",
            "¿Cómo construyo un rectángulo con medidas específicas en GeoGebra?"
        ];
        const example = examples[Math.floor(Math.random() * examples.length)];
        document.getElementById('userQuestion').value = example;
        sendQuestion();
    }

    // ---- ENTER PARA ENVIAR ----
    document.addEventListener('DOMContentLoaded', function() {
        const input = document.getElementById('userQuestion');
        input.addEventListener('keypress', function(e) {
            if (e.key === 'Enter' && !isProcessing) {
                e.preventDefault();
                sendQuestion();
            }
        });
    });
</script>

</body>
</html>
