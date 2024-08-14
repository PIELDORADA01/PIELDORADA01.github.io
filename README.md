
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Control de vehículos DGA</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            height: 100vh;
        }
        h1 {
            color: #00bcd4;
            font-weight: bold;
            text-align: center;
        }
        h2 {
            text-align: center;
            color: #333;
        }
        #content {
            width: 100%;
            display: flex;
            justify-content: space-between;
            padding: 20px;
        }
        #inputSection {
            flex: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        #inputDisplay {
            width: 80%;
            font-size: 2em;
            text-align: center;
            margin: 20px 0;
            padding: 10px;
            border: 2px solid #00bcd4;
            border-radius: 10px;
            color: #000;
            background-color: #fff;
        }
        #numberList {
            flex: 1;
            list-style: none;
            padding: 0;
            text-align: left;
            width: 30%;
            max-width: 400px;
            margin-top: 20px;
            background-color: #e0f7fa;
            border-radius: 10px;
            overflow-y: auto;
            max-height: 60vh;
        }
        #numberList li {
            padding: 10px;
            margin-bottom: 5px;
            background-color: #fff;
            border-radius: 5px;
            font-size: 1.2em;
            border-left: 5px solid #00bcd4;
        }
        .keyboard {
            width: 200px;
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            justify-self: flex-end;
            margin-bottom: 20px;
        }
        .keyboard button {
            padding: 15px;
            font-size: 1.5em;
            border: none;
            border-radius: 10px;
            background-color: #00bcd4;
            color: #fff;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
        .keyboard button:hover {
            background-color: #0097a7;
        }
        #voiceButton,
        #addButton {
            margin-top: 10px;
            padding: 15px 0;
            font-size: 1.5em;
            border: none;
            border-radius: 10px;
            background-color: #ff5722;
            color: #fff;
            cursor: pointer;
            transition: background-color 0.3s ease;
            width: 100%;
            text-align: center;
        }
        #voiceButton:hover {
            background-color: #e64a19;
        }
        #addButton {
            background-color: #4caf50;
        }
        #addButton:hover {
            background-color: #388e3c;
        }
        #exportButton {
            margin-top: 20px;
            padding: 15px 30px;
            font-size: 1.5em;
            border: none;
            border-radius: 10px;
            background-color: #ff9800;
            color: #fff;
            cursor: pointer;
            transition: background-color 0.3s ease;
            align-self: center;
        }
        #exportButton:hover {
            background-color: #f57c00;
        }
    </style>
</head>
<body>
    <h1>Control de vehículos DGA</h1>
    <h2>plataforma creada por Javier Astaroth</h2>

    <div id="content">
        <ul id="numberList"></ul>

        <div id="inputSection">
            <div id="inputDisplay">0000</div>
        </div>

        <div>
            <div class="keyboard">
                <button onclick="enterNumber('1')">1</button>
                <button onclick="enterNumber('2')">2</button>
                <button onclick="enterNumber('3')">3</button>
                <button onclick="enterNumber('4')">4</button>
                <button onclick="enterNumber('5')">5</button>
                <button onclick="enterNumber('6')">6</button>
                <button onclick="enterNumber('7')">7</button>
                <button onclick="enterNumber('8')">8</button>
                <button onclick="enterNumber('9')">9</button>
                <button onclick="clearInput()">C</button>
                <button onclick="enterNumber('0')">0</button>
                <button onclick="removeLast()">←</button>
            </div>

            <button id="voiceButton" onclick="startVoiceInput()">Dictar por voz</button>
            <button id="addButton" onclick="addToList()">Agregar</button>
        </div>
    </div>

    <button id="exportButton" onclick="exportList()">Exportar lista</button>

    <script>
        let input = '';

        function enterNumber(num) {
            if (input.length < 4) {
                input += num;
                updateDisplay();
            }
        }

        function clearInput() {
            input = '';
            updateDisplay();
        }

        function removeLast() {
            input = input.slice(0, -1);
            updateDisplay();
        }

        function updateDisplay() {
            document.getElementById('inputDisplay').innerText = input.padStart(4, '0');
        }

        function addToList() {
            if (input.length === 4) {
                const listItem = document.createElement('li');
                listItem.textContent = `${document.getElementById('numberList').children.length + 1}. ${input}`;
                document.getElementById('numberList').appendChild(listItem);
                clearInput();
            } else {
                alert('Por favor ingresa 4 dígitos.');
            }
        }

        function exportList() {
            const listItems = document.getElementById('numberList').children;
            let listContent = 'Lista de números:\n';
            for (let i = 0; i < listItems.length; i++) {
                listContent += listItems[i].textContent + '\n';
            }
            const phoneNumber = '+50577693150';
            const whatsappUrl = `https://wa.me/${phoneNumber}?text=${encodeURIComponent(listContent)}`;
            window.open(whatsappUrl, '_blank');
        }

        function startVoiceInput() {
            const recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
            recognition.lang = 'es-ES';
            recognition.interimResults = false;
            recognition.maxAlternatives = 1;

            recognition.start();

            recognition.onresult = function(event) {
                const voiceInput = event.results[0][0].transcript;
                const numbers = voiceInput.replace(/\D/g, ''); // Remover todo excepto números
                input = numbers.slice(0, 4); // Tomar solo los primeros 4 números
                updateDisplay();
            };

            recognition.onspeechend = function() {
                recognition.stop();
            };

            recognition.onerror = function(event) {
                alert('Error en el reconocimiento de voz: ' + event.error);
            };
        }
    </script>
</body>
</html>
