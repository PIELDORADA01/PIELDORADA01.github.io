<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Plataforma de Contenedores</title>
    <style>
        body {
            background-color: #87CEEB;
            color: white;
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
        }
        input {
            width: 200px;
            padding: 10px;
            margin: 10px;
            border: none;
            border-radius: 5px;
            font-size: 18px;
        }
        button {
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            background-color: #4CAF50;
            color: white;
            font-size: 18px;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        .container-list {
            margin-top: 20px;
            padding: 10px;
            border: 1px solid white;
            border-radius: 5px;
            max-height: 300px;
            overflow-y: auto;
            text-align: left;
        }
        .entry {
            padding: 5px;
            border-bottom: 1px solid #fff;
        }
        .entry:last-child {
            border-bottom: none;
        }
        #mic-status {
            margin-top: 20px;
            font-weight: bold;
        }
        .naviera-banner {
            background-color: rgba(255, 255, 255, 0.2);
            color: white;
            padding: 10px;
            border-radius: 5px;
            margin-bottom: 20px;
            display: inline-block;
            font-size: 16px;
        }
    </style>
</head>
<body>

    <h1>DGA - Plataforma de Contenedores</h1>
    <h2>Ingreso y Seguimiento</h2>

    <div class="naviera-banner">
        Navieras: 1. Maersk Line | 2. Sealand | 3. CMA | 4. Hapag Lloyd | 5. Evergreen | 6. MSC | 7. OOCL
    </div>

    <input type="text" id="contenedor" placeholder="Contenedor" readonly>
    <input type="text" id="sello" placeholder="Sello" readonly>
    <input type="text" id="naviera" placeholder="Naviera" readonly>

    <button id="add-container">Agregar Contenedor</button>

    <div id="mic-status">Micrófono: Desactivado</div>
    <div class="container-list" id="container-list"></div>

    <script>
        const containerInput = document.getElementById('contenedor');
        const sealInput = document.getElementById('sello');
        const navieraInput = document.getElementById('naviera');
        const containerList = document.getElementById('container-list');
        const micStatus = document.getElementById('mic-status');

        const navieras = {
            1: "Maersk Line",
            2: "Sealand",
            3: "CMA",
            4: "Hapag Lloyd",
            5: "Evergreen",
            6: "MSC",
            7: "OOCL"
        };

        let recognition;
        let isMicActive = false;

        function startRecognition() {
            recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
            recognition.continuous = true;
            recognition.interimResults = false;

            recognition.onstart = () => {
                isMicActive = true;
                micStatus.innerText = "Micrófono: Activado";
            };

            recognition.onresult = (event) => {
                const transcript = event.results[event.resultIndex][0].transcript.toLowerCase().trim();
                handleVoiceCommands(transcript);
            };

            recognition.onerror = (event) => {
                console.error("Error de reconocimiento:", event.error);
            };

            recognition.onend = () => {
                isMicActive = false;
                micStatus.innerText = "Micrófono: Desactivado";
                startRecognition(); // Reiniciar el reconocimiento
            };

            recognition.start();
        }

        function handleVoiceCommands(command) {
            if (command.includes("contenedor")) {
                const numbers = command.match(/\d+/g);
                if (numbers) {
                    numbers.forEach(num => {
                        if (containerInput.value.length < 7) {
                            containerInput.value += num;
                        }
                    });
                }
            } else if (command.includes("sello")) {
                const numbers = command.match(/\d+/g);
                if (numbers) {
                    numbers.forEach(num => {
                        if (sealInput.value.length < 4) {
                            sealInput.value += num;
                        }
                    });
                }
            } else if (command.includes("naviera")) {
                const navieraMatch = command.match(/\d+/);
                if (navieraMatch && navieras[navieraMatch[0]]) {
                    navieraInput.value = navieras[navieraMatch[0]];
                } else {
                    alert("Naviera no válida. Por favor, di un número del 1 al 7.");
                }
            } else if (command.includes("agregar")) {
                addContainer();
            } else if (command.includes("limpiar")) {
                clearInputs();
            }
        }

        function addContainer() {
            const contenedor = containerInput.value;
            const sello = sealInput.value;
            const naviera = navieraInput.value;

            if (contenedor.length === 7 && sello.length === 4 && naviera) {
                const date = new Date();
                const entry = document.createElement('div');
                entry.className = 'entry';
                entry.innerText = `Contenedor: ${contenedor}, Sello: ${sello}, Naviera: ${naviera}, Fecha: ${date.toLocaleString()}`;
                containerList.appendChild(entry);
                clearInputs();
            } else {
                alert("Por favor, completa todos los campos correctamente.");
            }
        }

        function clearInputs() {
            containerInput.value = '';
            sealInput.value = '';
            navieraInput.value = '';
        }

        document.getElementById('add-container').addEventListener('click', addContainer);

        startRecognition();
    </script>

</body>
</html>
