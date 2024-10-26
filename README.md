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
        .remote {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            height: 300px; /* Задаем высоту для вертикального центрирования */
        }
        .button {
            padding: 30px 45px;
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
        .left, .center, .right {
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .right {
            align-items: flex-end; /* Выровнять кнопки вправо */
        }
    </style>
</head>
<body>

<h1>Управление машинкой</h1>
<div class="remote">
    <div class="left">
        <button class="button" onclick="sendCommand('forward')">Вперед</button>
        <button class="button" onclick="sendCommand('backward')">Назад</button>
    </div>
    <div class="center">
        <button class="button" onclick="sendCommand('sound')">Включить звук</button>
        <button class="button" onclick="sendCommand('mode')">Изменить режим</button>
        <button class="button" onclick="sendCommand('automode')">Автомод</button>
    </div>
    <div class="right">
        <button class="button" onclick="sendCommand('left')">Влево</button>
        <button class="button" onclick="sendCommand('right')">Вправо</button>
    </div>
</div>

<script>
    const socket = new WebSocket('ws://192.168.100.4:81'); // Замените <IP_WEMOS> на IP адрес Wemos

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
