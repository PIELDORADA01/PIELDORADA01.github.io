<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title><span style="font-style: italic; color: #e91e63; text-shadow: 1px 1px 2px rgba(0,0,0,0.5);">Isla Piel Dorada</span></title>
    <style>
        body {
            background-color: #000000; /* Fondo negro */
            color: #FFFFFF; /* Fuentes blancas */
            font-family: 'Times New Roman', serif;
            text-align: center;
            margin: 0;
            padding: 0;
            animation: fadeIn 1s ease-out; /* Animación de entrada */
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
        }
        h1, p, li, h2 {
            font-style: italic;
            color: #FFFFFF;
            text-shadow: 1px 1px 2px rgba(255,255,255,0.5);
            margin-bottom: 20px; /* Espacio entre secciones */
        }
        img {
            max-width: 100%;
            height: auto;
            border-radius: 15px;
            box-shadow: 0 4px 8px rgba(255, 255, 255, 0.1); /* Sombra suave */
            transition: transform 0.3s ease-in-out; /* Transición en hover */
            margin-bottom: 20px; /* Espacio entre imágenes */
        }
        img:hover {
            transform: scale(1.05); /* Aumento en hover */
        }
        .carousel {
            display: flex;
            overflow-x: auto;
            scroll-snap-type: x mandatory;
            margin-bottom: 20px; /* Espacio entre carruseles */
        }
        .carousel img {
            scroll-snap-align: center;
            flex: none;
            width: 100%;
            height: auto;
            border-radius: 15px;
            box-shadow: 0 4px 8px rgba(255, 255, 255, 0.1); /* Sombra suave */
            transition: transform 0.3s ease-in-out; /* Transición en hover */
            margin-right: 10px; /* Espacio entre imágenes del carrusel */
        }
        .carousel img:last-child {
            margin-right: 0;
        }
        .carousel::-webkit-scrollbar {
            display: none;
        }
        .services {
            text-align: left;
            margin-bottom: 20px; /* Espacio entre secciones */
        }
        .button {
            display: inline-block;
            padding: 10px 20px;
            margin: 10px;
            background-color: #e91e63; /* Rosa intenso */
            color: white;
            text-decoration: none;
            border-radius: 5px;
            transition: background-color 0.3s ease-in-out; /* Transición de color */
        }
        .button:hover {
            background-color: #c2185b; /* Color más oscuro en hover */
        }
        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <img src="https://i.postimg.cc/43RsVCqh/IMG-20240706-WA0009.jpg" alt="Logo del hotel Isla Piel Dorada">

        <h1>Isla Piel Dorada</h1>
        <p>Bienvenido a Isla Piel Dorada, un paraíso escondido en las isletas de Granada, Nicaragua. Disfruta de una experiencia única en cabañas frente al lago y con vistas al majestuoso volcán Mombacho. Ven y descubre el lujo y la serenidad en cada rincón de nuestra isla.</p>

        <h2>Video</h2>
        <iframe width="800" height="450" src="https://www.youtube.com/embed/GcUBnhc-zLo?autoplay=1&loop=1&playlist=GcUBnhc-zLo&controls=0&mute=0&rel=0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

        <h2>Destinos Destacados</h2>
        <div class="carousel">
            <img src="https://i.postimg.cc/0jjsP9Mh/IMG-20240706-WA0000.jpg" alt="Destino 1">
            <img src="https://i.postimg.cc/t4WHXSJR/IMG-20240706-WA0001.jpg" alt="Destino 2">
            <img src="https://i.postimg.cc/X7Tb6SVD/IMG-20240706-WA0002.jpg" alt="Destino 3">
            <img src="https://i.postimg.cc/CLZg2LVq/IMG-20240706-WA0003.jpg" alt="Destino 4">
            <img src="https://i.postimg.cc/zD2NpH4N/IMG-20240706-WA0004.jpg" alt="Destino 5">
            <img src="https://i.postimg.cc/C52VK9b5/IMG-20240706-WA0005.jpg" alt="Destino 6">
            <img src="https://i.postimg.cc/zfw5ktY2/IMG-20240706-WA0006.jpg" alt="Destino 7">
            <img src="https://i.postimg.cc/hjSnZLSD/IMG-20240706-WA0007.jpg" alt="Destino 8">
            <img src="https://i.postimg.cc/mD8svPDQ/IMG-20240706-WA0008.jpg" alt="Destino 9">
        </div>

        <h2>Servicios</h2>
        <ul class="services">
            <li><strong>Hospedaje en las isletas de Granada:</strong> Bella isla con cabañas frente al lago y al volcán Mombacho.</li>
            <li><strong>Paquete Hospedaje Incluye:</strong></li>
            <ul>
                <li>Transporte en lancha.</li>
                <li>Hospedaje en la isla Piel Dorada.</li>
                <li>Desayuno, almuerzo y cena.</li>
                <li>Bebidas durante las comidas.</li>
            </ul>
            <li>Precio: <strong>$78 USD por persona</strong></li>
            <li><strong>Horarios:</strong></li>
            <ul>
                <li>Check-in: 2 pm</li>
                <li>Check-out: 12 pm del día siguiente.</li>
            </ul>
            <li><strong>Instalaciones:</strong> Piscina, bar, TV por cable, y kayaks para explorar las isletas.</li>
            <li>Descubre el paraíso en cada rincón, donde cada detalle está diseñado para tu confort y deleite.</li>
        </ul>

        <a class="button" href="https://wa.me/50587685045" target="_blank">Contáctanos</a>
        <a class="button" href="https://maps.app.goo.gl/E6xgBatRrZAYjKVx6" target="_blank">Ver Ubicación</a>
    </div>
</body>
</html>
