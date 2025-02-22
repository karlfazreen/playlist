<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Feel Free to Use It</title>
    <style>
        body {
            background: url('https://media.giphy.com/media/l0HlNaQ6gWfllcjDO/giphy.gif') no-repeat center center fixed;
            background-size: cover;
            position: relative;
            height: 100vh;
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        /* Overlay untuk buat background jadi transparent 30% */
        body::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7); /* 70% hitam, jadi GIF nampak 30% */
        }

        h1 {
            font-size: 80px; /* Tulisan besar */
            font-weight: bold;
            color: #00ff00;
            text-shadow: 0 0 20px #00ff00, 0 0 40px #00ff00, 0 0 80px #00ff00;
            position: relative; /* Supaya teks tak kena overlay */
            animation: floating 3s infinite ease-in-out;
        }

        @keyframes floating {
            0% { transform: translateY(0); }
            50% { transform: translateY(-30px); }
            100% { transform: translateY(0); }
        }
    </style>
</head>
<body>
    <h1>FEEL FREE TO USE IT</h1>
</body>
</html>
