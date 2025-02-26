# simulador-del-Movimiento-Parab-lico-de-un-Proyectil.<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simulación de Movimiento Parabólico</title>
    <style>
        body { text-align: center; font-family: Arial, sans-serif; }
        canvas { border: 1px solid black; margin-top: 10px; }
    </style>
</head>
<body>
    <h2>Simulación del Movimiento Parabólico</h2>
    <label for="velocidad">Velocidad inicial (m/s):</label>
    <input type="number" id="velocidad" value="20">
    <label for="angulo">Ángulo de lanzamiento (°):</label>
    <input type="number" id="angulo" value="45">
    <button onclick="simular()">Simular</button>
    <canvas id="canvas" width="600" height="400"></canvas>
    
    <script>
        function simular() {
            const canvas = document.getElementById("canvas");
            const ctx = canvas.getContext("2d");
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            const velocidadInicial = parseFloat(document.getElementById("velocidad").value);
            const angulo = parseFloat(document.getElementById("angulo").value) * Math.PI / 180;
            const g = 9.81; 
            const escala = 5;
            
            let x = 0, y = 0;
            let t = 0, dt = 0.05;
            const v0x = velocidadInicial * Math.cos(angulo);
            const v0y = velocidadInicial * Math.sin(angulo);
            
            function actualizar() {
                t += dt;
                x = v0x * t;
                y = (v0y * t) - (0.5 * g * t * t);
                
                if (y < 0) return;
                
                ctx.fillStyle = "red";
                ctx.beginPath();
                ctx.arc(x * escala, canvas.height - y * escala, 3, 0, Math.PI * 2);
                ctx.fill();
                
                requestAnimationFrame(actualizar);
            }
            actualizar();
        }
    </script>
</body>
</html>
