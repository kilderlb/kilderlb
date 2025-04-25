# Clone o repositório vazio
git clone https://github.com/seu-usuario/velocimetro-html.git

# Entre no diretório do repositório
cd velocimetro-html

# Crie o arquivo HTML
echo "<!DOCTYPE html>
<html lang=\"pt-BR\">
<head>
    <meta charset=\"UTF-8\">
    <meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0\">
    <title>Gráfico de Velocímetro</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f4f4f9;
            font-family: Arial, sans-serif;
        }
        canvas {
            border-radius: 50%;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
    </style>
</head>
<body>
    <canvas id=\"velocimetro\" width=\"300\" height=\"300\"></canvas>
    <script>
        const canvas = document.getElementById('velocimetro');
        const ctx = canvas.getContext('2d');
        const centerX = canvas.width / 2;
        const centerY = canvas.height / 2;
        const radius = 100;
        const maxValue = 180; // Velocidade máxima
        const currentValue = 120; // Velocidade atual

        function drawVelocimetro() {
            // Fundo do velocímetro
            ctx.beginPath();
            ctx.arc(centerX, centerY, radius, Math.PI, 2 * Math.PI);
            ctx.fillStyle = '#ddd';
            ctx.fill();

            // Setores de cores
            const sectors = [
                { start: Math.PI, end: Math.PI + (Math.PI / 3), color: '#4CAF50' }, // Verde
                { start: Math.PI + (Math.PI / 3), end: Math.PI + (2 * Math.PI / 3), color: '#FFC107' }, // Amarelo
                { start: Math.PI + (2 * Math.PI / 3), end: 2 * Math.PI, color: '#F44336' }, // Vermelho
            ];
            sectors.forEach(sector => {
                ctx.beginPath();
                ctx.arc(centerX, centerY, radius, sector.start, sector.end);
                ctx.lineWidth = 20;
                ctx.strokeStyle = sector.color;
                ctx.stroke();
            });

            // Ponteiro
            const angle = Math.PI + (currentValue / maxValue) * Math.PI;
            const pointerLength = radius - 20;
            ctx.beginPath();
            ctx.moveTo(centerX, centerY);
            ctx.lineTo(centerX + Math.cos(angle) * pointerLength, centerY + Math.sin(angle) * pointerLength);
            ctx.lineWidth = 5;
            ctx.strokeStyle = '#000';
            ctx.stroke();

            // Texto de velocidade
            ctx.font = '20px Arial';
            ctx.fillStyle = '#333';
            ctx.textAlign = 'center';
            ctx.fillText(`${currentValue} km/h`, centerX, centerY + 60);
        }

        drawVelocimetro();
    </script>
</body>
</html>" > index.html

# Adicione os arquivos ao repositório
git add index.html

# Faça o commit
git commit -m "Adiciona velocímetro em HTML"

# Envie para o GitHub
git push origin main
