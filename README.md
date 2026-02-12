<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>For You ❤️</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
    body {
        height: 100vh;
        margin: 0;
        display: flex;
        justify-content: center;
        align-items: center;
        background: linear-gradient(135deg, #ff6f91, #ff9671, #ffc75f);
        font-family: Arial, sans-serif;
        overflow: hidden;
        backdrop-filter: blur(8px);
    }

    /* Soft floating light particles */
    .particles span {
        position: absolute;
        width: 6px;
        height: 6px;
        background: rgba(255,255,255,0.6);
        border-radius: 50%;
        animation: float 10s linear infinite;
    }

    @keyframes float {
        from { transform: translateY(100vh); opacity: 0; }
        10% { opacity: 1; }
        to { transform: translateY(-10vh); opacity: 0; }
    }

    .card {
        background: rgba(255, 255, 255, 0.9);
        padding: 35px;
        border-radius: 25px;
        text-align: center;
        box-shadow: 0 20px 40px rgba(0,0,0,0.3);
        max-width: 380px;
        position: relative;
        z-index: 2;
        transition: opacity 1s ease, transform 1s ease;
    }

    .fade-out {
        opacity: 0;
        transform: scale(0.9);
    }

    .fade-in {
        animation: fadeIn 1.5s ease forwards;
    }

    @keyframes fadeIn {
        from { opacity: 0; transform: scale(0.9); }
        to { opacity: 1; transform: scale(1); }
    }

    h1 {
        color: #ff2e63;
    }

    p {
        font-size: 18px;
        margin-bottom: 25px;
        color: #333;
    }

    button {
        padding: 12px 24px;
        font-size: 16px;
        border: none;
        border-radius: 30px;
        cursor: pointer;
        margin: 10px;
        transition: transform 0.2s ease;
    }

    button:hover {
        transform: scale(1.05);
    }

    #yes {
        background: #ff2e63;
        color: white;
    }

    #no {
        background: #ddd;
        position: absolute;
    }

    /* Hearts after YES */
    .hearts span {
        position: absolute;
        bottom: -20px;
        font-size: 20px;
        animation: floatUp 5s linear infinite;
        opacity: 0.8;
    }

    @keyframes floatUp {
        0% { transform: translateY(0); opacity: 0; }
        10% { opacity: 1; }
        100% { transform: translateY(-110vh); opacity: 0; }
    }
</style>
</head>

<body>

<div class="particles" id="particles"></div>

<div class="card" id="card">
    <h1>Hey Kochee ❤️</h1>
    <p>Will you be my Valentine? 💘</p>

    <button id="yes" onclick="yesClicked()">Yes 💖</button>
    <button id="no" onmouseover="moveNo()">No 🙈</button>
</div>

<div class="hearts" id="hearts"></div>

<audio id="bgm" loop>
    <source src="Husn.mp3" type="audio/mpeg">
</audio>

<script>

// Generate soft floating particles
function createParticles() {
    const container = document.getElementById("particles");
    for (let i = 0; i < 30; i++) {
        const dot = document.createElement("span");
        dot.style.left = Math.random() * 100 + "vw";
        dot.style.animationDuration = (5 + Math.random() * 5) + "s";
        container.appendChild(dot);
    }
}
createParticles();

function yesClicked() {
    const card = document.getElementById("card");
    const music = document.getElementById("bgm");

    music.play();

    card.classList.add("fade-out");

    setTimeout(() => {
        card.innerHTML = `
            <div class="fade-in">
                <h1>Yayyy! 💕</h1>
                <p>
                    You just made my heart the happiest ❤️<br><br>
                    From this moment… "Husn" will always remind me of you ✨<br><br>
                </p>
            </div>
        `;
        card.classList.remove("fade-out");
    }, 1000);

    startHearts();
}

function moveNo() {
    const noBtn = document.getElementById("no");
    const card = document.querySelector(".card");

    const x = Math.random() * (card.offsetWidth - noBtn.offsetWidth);
    const y = Math.random() * (card.offsetHeight - noBtn.offsetHeight);

    noBtn.style.left = x + "px";
    noBtn.style.top = y + "px";
}

function startHearts() {
    const heartsContainer = document.getElementById("hearts");

    for (let i = 0; i < 40; i++) {
        const heart = document.createElement("span");
        heart.innerHTML = "❤️";
        heart.style.left = Math.random() * 100 + "vw";
        heart.style.animationDuration = (3 + Math.random() * 3) + "s";
        heartsContainer.appendChild(heart);

        setTimeout(() => heart.remove(), 6000);
    }
}

</script>

</body>
</html>