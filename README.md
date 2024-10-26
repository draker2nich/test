<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Управление машинкой</title>
    <style>
        body { text-align: center; font-family: Arial, sans-serif; }
        button { margin: 10px; padding: 15px 25px; font-size: 18px; cursor: pointer; }
    </style>
</head>
<body>
    <h1>Управление радиоуправляемой машинкой</h1>
    <button onclick="sendCommand('forward')">Вперед</button>
    <button onclick="sendCommand('backward')">Назад</button>
    <button onclick="sendCommand('left')">Влево</button>
    <button onclick="sendCommand('right')">Вправо</button>
    <button onclick="sendCommand('automode')">Автомод</button>
    <button onclick="sendCommand('sound')">Включить звук</button>
    <button onclick="sendCommand('changemode')">Изменить режим</button>

    <script>
        function sendCommand(command) {
            const ip = '192.168.100.4'; // Замените на IP-адрес вашего Wemos D1 Mini
            fetch(`http://${ip}/${command}`)
                .then(response => response.text())
                .then(data => {
                    console.log(data); // Для отладки, можно убрать в финальной версии
                })
                .catch(error => {
                    console.error('Ошибка:', error);
                });
        }
    </script>
</body>
</html>
