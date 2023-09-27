<!DOCTYPE html>
<html>
<head>
    <title>Asistente Básico en JavaScript</title>
</head>
<body>
    <h1>Mi Asistente Básico</h1>
    <button id="startButton">Iniciar Asistente</button>
    <div id="output"></div>

    <script>
        const startButton = document.getElementById('startButton');
        const outputDiv = document.getElementById('output');
        let recognition;

        startButton.addEventListener('click', () => {
            recognition = new (webkitSpeechRecognition || SpeechRecognition)();
            recognition.lang = 'es-ES';
            recognition.onstart = () => {
                outputDiv.textContent = 'Escuchando...';
            };
            recognition.onresult = (event) => {
                const result = event.results[0][0].transcript;
                outputDiv.textContent = 'Has dicho: ' + result;
            };
            recognition.onerror = (event) => {
                outputDiv.textContent = 'Error: ' + event.error;
            };
            recognition.onend = () => {
                outputDiv.textContent += '\nAsistente detenido.';
            };
            recognition.start();
        });
    </script>
</body>
</html>
