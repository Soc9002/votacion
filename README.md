<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Votación</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; }
        .hidden { display: none; }
    </style>
</head>
<body>
    <div id="registro">
        <h2>Registro</h2>
        <input type="text" id="nombre" placeholder="Ingrese su nombre">
        <button onclick="registrar()">Continuar</button>
    </div>
    
    <div id="votacion" class="hidden">
        <h2>Votación</h2>
        <p>Seleccione su candidato:</p>
        <button onclick="votar('X')">Candidato X</button>
        <button onclick="votar('Y')">Candidato Y</button>
        <button onclick="votar('Z')">Candidato Z</button>
    </div>
    
    <div id="agradecimiento" class="hidden">
        <h2>Gracias por votar</h2>
        <p>Tu voto ha sido registrado.</p>
    </div>

    <script>
        function getIP() {
            return localStorage.getItem('votoIP');
        }
        
        function setIP() {
            localStorage.setItem('votoIP', 'true');
        }
        
        function registrar() {
            let nombre = document.getElementById("nombre").value;
            if (nombre.trim() === "") {
                alert("Ingrese un nombre válido");
                return;
            }
            localStorage.setItem("nombreUsuario", nombre);
            document.getElementById("registro").classList.add("hidden");
            document.getElementById("votacion").classList.remove("hidden");
        }
        
        function votar(candidato) {
            if (getIP()) {
                document.getElementById("votacion").classList.add("hidden");
                document.getElementById("agradecimiento").classList.remove("hidden");
            } else {
                alert("Has votado por: " + candidato);
                let votos = JSON.parse(localStorage.getItem("votos")) || [];
                votos.push({ nombre: localStorage.getItem("nombreUsuario"), candidato });
                localStorage.setItem("votos", JSON.stringify(votos));
                setIP();
                document.getElementById("votacion").classList.add("hidden");
                document.getElementById("agradecimiento").classList.remove("hidden");
            }
        }
        
        window.onload = function() {
            if (getIP()) {
                document.getElementById("registro").classList.add("hidden");
                document.getElementById("agradecimiento").classList.remove("hidden");
            }
        };
    </script>
</body>
</html>
# votacion
