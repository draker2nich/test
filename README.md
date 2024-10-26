<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Управление машинкой</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f0f0f0;
            padding: 20px;
        }
        h1 {
            color: #333;
        }
        .button {
            padding: 15px 30px;
            margin: 10px;
            font-size: 18px;
            cursor: pointer;
            border: none;
            border-radius: 5px;
            background-color: #007BFF;
            color: white;
            transition: background-color 0.3s;
        }
        .button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>

<h1>Управление машинкой</h1>
<button class="button" onclick="sendCommand('forward')">Вперед</button>
<button class="button" onclick="sendCommand('backward')">Назад</button>
<button class="button" onclick="sendCommand('left')">Влево</button>
<button class="button" onclick="sendCommand('right')">Вправо</button>
<button class="button" onclick="sendCommand('sound')">Включить звук</button>
<button class="button" onclick="sendCommand('mode')">Изменить режим</button>
<button class="button" onclick="sendCommand('automode')">Автомод</button>

<script>
    const socket = new WebSocket('ws://<IP_WEMOS>:81'); // Замените <IP_WEMOS> на IP адрес Wemos

    socket.onopen = function() {
        console.log('Соединение установлено');
    };

    socket.onmessage = function(event) {
        console.log('Получено сообщение: ', event.data);
    };

    function sendCommand(command) {
        if (socket.readyState === WebSocket.OPEN) {
            socket.send(command);
            console.log(`Команда "${command}" отправлена`);
        } else {
            console.error('WebSocket не открыт');
        }
    }
</script>

</body>
</html>
