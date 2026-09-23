<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Love Heart Animation</title>

<style>
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    background: #000;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    font-family: Arial, sans-serif;
}

.container {
    width: 100vw;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
}

.heart {
    position: relative;
    width: 320px;
    height: 300px;
    filter: drop-shadow(0 0 8px #ff9fc7);
}

/* Текст по контуру сердца */
.word {
    position: absolute;
    color: #ea80b0;
    font-size: 15px;
    font-weight: 500;
    white-space: nowrap;
    letter-spacing: 2px;
    text-shadow:
        0 0 5px #ffb6d5,
        0 0 10px #ea80b0;
    animation: glow 1.8s infinite alternate;
}

/* Свечение */
@keyframes glow {
    from {
        opacity: .65;
        text-shadow:
            0 0 3px #ffb6d5,
            0 0 7px #ea80b0;
    }

    to {
        opacity: 1;
        text-shadow:
            0 0 8px #fff,
            0 0 15px #ff80b5;
    }
}

/* Движение каждого слоя */
.layer1 {
    animation: move1 5s linear infinite;
}

.layer2 {
    animation: move2 6s linear infinite;
}

.layer3 {
    animation: move3 7s linear infinite;
}

@keyframes move1 {
    from {
        transform: translateY(0);
    }
    50% {
        transform: translateY(8px);
    }
    to {
        transform: translateY(0);
    }
}

@keyframes move2 {
    from {
        transform: translateY(8px);
    }
    50% {
        transform: translateY(-5px);
    }
    to {
        transform: translateY(8px);
    }
}

@keyframes move3 {
    from {
        transform: translateY(-5px);
    }
    50% {
        transform: translateY(10px);
    }
    to {
        transform: translateY(-5px);
    }
}

/* Текстовая надпись сверху */
.title {
    position: absolute;
    top: 50px;
    color: white;
    font-size: 25px;
    font-weight: bold;
}

.title span {
    color: #f18bb8;
}
</style>
</head>

<body>

<div class="container">

    <div class="title">
        <span>Love Heart</span> Animation
    </div>

    <div class="heart" id="heart"></div>

</div>

<script>

const heart = document.getElementById("heart");

/*
    Формула сердца.
    Создаём несколько линий из текста "I love you".
*/

const layers = 9;

for (let layer = 0; layer < layers; layer++) {

    const group = document.createElement("div");

    group.className = "word layer" + ((layer % 3) + 1);

    /*
      Создаём много надписей.
    */

    for (let i = 0; i < 90; i++) {

        const text = document.createElement("span");

        text.textContent = "I love you ";

        /*
          Параметр сердца.
        */

        const t = (i / 90) * Math.PI * 2;

        /*
          Классическая параметрическая формула сердца.
        */

        const x =
            16 * Math.pow(Math.sin(t), 3);

        const y =
            -(13 * Math.cos(t)
            - 5 * Math.cos(2*t)
            - 2 * Math.cos(3*t)
            - Math.cos(4*t));

        /*
          Разные размеры слоёв.
        */

        const scale = 8 + layer * 1.5;

        const posX = 160 + x * scale;
        const posY = 145 + y * scale;

        /*
          Направление текста по контуру.
        */

        const nextT = t + 0.03;

        const nextX =
            16 * Math.pow(Math.sin(nextT), 3);

        const nextY =
            -(13 * Math.cos(nextT)
            - 5 * Math.cos(2*nextT)
            - 2 * Math.cos(3*nextT)
            - Math.cos(4*nextT));

        const angle =
            Math.atan2(
                nextY - y,
                nextX - x
            ) * 180 / Math.PI;

        text.style.position = "absolute";
        text.style.left = posX + "px";
        text.style.top = posY + "px";

        text.style.transform =
            `translate(-50%, -50%) rotate(${angle}deg)`;

        /*
          Немного разный размер,
          чтобы получилось как на видео.
        */

        text.style.fontSize =
            (11 + layer * 0.6) + "px";

        text.style.opacity =
            0.45 + layer * 0.06;

        group.appendChild(text);
    }

    heart.appendChild(group);
}

</script>

</body>
</html>
