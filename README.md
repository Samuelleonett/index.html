<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🐱 Recuerdo de Gatos 🐱</title>
    <style>
        /* --- style.css start --- */
        body {
            margin: 0;
            background-color: #e0b0ff; /* Morado claro 💜 */
            font-family: 'Arial', sans-serif;
            overflow: hidden; /* Evita barras de desplazamiento si los elementos se salen */
            display: flex;
            justify-content: center; /* Centra el contenido horizontalmente */
            align-items: center; /* Centra el contenido verticalmente */
            min-height: 100vh; /* Ocupa al menos el 100% de la altura de la ventana */
            position: relative; /* Necesario para posicionar elementos hijos de forma absoluta */
        }

        .corner {
            position: absolute; /* Posicionamiento absoluto respecto al body */
            color: white; /* Color del texto blanco */
            font-size: 28px; /* Tamaño de fuente más grande */
            font-weight: bold; /* Negrita */
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3); /* Sombra para mejor visibilidad */
        }

        .top-left { top: 15px; left: 15px; }
        .top-right { top: 15px; right: 15px; }
        .bottom-left { bottom: 15px; left: 15px; }
        .bottom-right { bottom: 15px; right: 15px; }

        .paw-print {
            position: absolute; /* Posicionamiento absoluto */
            width: 50px; /* Tamaño de la huella */
            height: auto; /* Mantiene la proporción */
            filter: drop-shadow(2px 2px 3px rgba(0, 0, 0, 0.2)); /* Sombra para dar profundidad */
            transition: transform 0.1s ease-out; /* Transición suave para el movimiento */
        }

        .top-left-paw { top: 70px; left: 70px; transform: rotate(-20deg); }
        .top-right-paw { top: 70px; right: 70px; transform: rotate(20deg); }
        .bottom-left-paw { bottom: 70px; left: 70px; transform: rotate(160deg); }
        .bottom-right-paw { bottom: 70px; right: 70px; transform: rotate(-160deg); }

        .container {
            text-align: center; /* Centra el contenido (imagen y botón) */
            background-color: rgba(255, 255, 255, 0.7); /* Fondo semi-transparente para el contenedor */
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2); /* Sombra más pronunciada */
            backdrop-filter: blur(5px); /* Efecto de desenfoque detrás del contenedor */
        }

        #catImage {
            max-width: 90%; /* Asegura que la imagen no sea más ancha que su contenedor */
            max-height: 60vh; /* Limita la altura para pantallas pequeñas */
            border-radius: 10px; /* Bordes redondeados para la imagen */
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            margin-bottom: 25px; /* Espacio entre la imagen y el botón */
            object-fit: contain; /* Asegura que la imagen se ajuste sin cortarse */
            transition: transform 0.3s ease-out; /* Animación al cambiar de imagen */
        }

        #catImage.animate-in {
            animation: fadeInScale 0.5s ease-out forwards; /* Animación de entrada */
        }

        @keyframes fadeInScale {
            from {
                opacity: 0;
                transform: scale(0.9);
            }
            to {
                opacity: 1;
                transform: scale(1);
            }
        }

        #changeImageBtn {
            padding: 12px 25px; /* Más padding para un botón más grande */
            font-size: 18px; /* Fuente más grande */
            background-color: #d8bfd8; /* Lavanda */
            color: #333; /* Texto oscuro */
            border: none;
            border-radius: 30px; /* Bordes muy redondeados (píldora) */
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.1s ease-out; /* Animaciones en hover y click */
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        #changeImageBtn:hover {
            background-color: #c19acd; /* Tono más oscuro al pasar el mouse */
            transform: translateY(-2px); /* Ligero levantamiento al pasar el mouse */
        }

        #changeImageBtn:active {
            transform: translateY(0); /* Vuelve a su posición al hacer click */
            background-color: #aa86bb; /* Tono aún más oscuro al presionar */
        }

        .paw-print.active-paw {
            animation: pawMove 0.4s ease-out forwards;
        }

        @keyframes pawMove {
            0% { transform: scale(1) translateY(0); opacity: 1; }
            50% { transform: scale(1.2) translateY(-10px); opacity: 0.8; } /* Crece un poco y sube */
            100% { transform: scale(1) translateY(0); opacity: 1; } /* Vuelve a su tamaño original */
        }
        /* --- style.css end --- */
    </style>
</head>
<body>
    <div class="corner top-left">-444</div>
    <div class="corner top-right">-444</div>
    <div class="corner bottom-left">-444</div>
    <div class="corner bottom-right">-444</div>

    <img src="collage-gatitos/fotos/paw_print.png" alt="Huella de gato" class="paw-print top-left-paw">
    <img src="collage-gatitos/fotos/paw_print.png" alt="Huella de gato" class="paw-print top-right-paw">
    <img src="collage-gatitos/fotos/paw_print.png" alt="Huella de gato" class="paw-print bottom-left-paw">
    <img src="collage-gatitos/fotos/paw_print.png" alt="Huella de gato" class="paw-print bottom-right-paw">
    
    <div class="container">
        <img id="catImage" src="collage-gatitos/fotos/juntos.jpg" alt="Foto de gato">
        <button id="changeImageBtn">Siguiente Foto 🐾</button>
    </div>

    <script>
        /* --- script.js start --- */
        document.addEventListener('DOMContentLoaded', function() {
            const catImage = document.getElementById('catImage');
            const changeImageBtn = document.getElementById('changeImageBtn');
            const pawPrints = document.querySelectorAll('.paw-print'); 

            
            const imageNames = [
                'juntos.jpg', 'abrazos.jpg', 'dormidos.jpg', 'demyan.jpg', 'atenea.jpg',
                'dormido1.jpg', 'dormido2.jpg', 'dormido3.jpg', 'dormido4.jpg', 'dormido5.jpg',
                'dormido6.jpg', 'dormido7.jpg', 'dormido8.jpg', 'dormido9.jpg', 'dormido10.jpg',
                'dormido11.jpg', 'dormido12.jpg', 'dormido13.jpg'
            ];

            let currentIndex = 0;

            changeImageBtn.addEventListener('click', function() {
                currentIndex = (currentIndex + 1) % imageNames.length;
                
                catImage.classList.remove('animate-in');
                void catImage.offsetWidth; // Truco para forzar el reflow y reiniciar la animación
                catImage.classList.add('animate-in');

                // Ajusta la ruta de la imagen usando el nuevo directorio
                catImage.src = `collage-gatitos/fotos/${imageNames[currentIndex]}`;
                
                animatePawPrints();
            });

            function animatePawPrints() {
                pawPrints.forEach(paw => {
                    paw.classList.add('active-paw');
                    setTimeout(() => {
                        paw.classList.remove('active-paw');
                    }, 500); // Debe coincidir o ser ligeramente mayor que la duración de la animación CSS
                });
            }
        });
        /* --- script.js end --- */
    </script>
</body>
</html>
