<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ping Pong Game</title>
    <style>
        body {
            background: #222;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        #gameCanvas {
            background: #fff;
            border: 4px solid #1877f2;
            border-radius: 10px;
            display: block;
        }
        .info {
            color: #fff;
            text-align: center;
            margin-bottom: 20px;
            font-size: 1.2rem;
        }
    </style>
</head>
<body>
    <div class="info">Dùng phím mũi tên lên/xuống để điều khiển vợt bên trái</div>
    <canvas id="gameCanvas" width="700" height="400"></canvas>
    <script>
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        // Paddle
        const paddleHeight = 80;
        const paddleWidth = 12;
        let paddleY = (canvas.height - paddleHeight) / 2;
        // AI Paddle
        let aiPaddleY = (canvas.height - paddleHeight) / 2;
        // Ball
        let ballX = canvas.width / 2;
        let ballY = canvas.height / 2;
        let ballRadius = 10;
        let ballSpeedX = 5;
        let ballSpeedY = 3;
        // Score
        let playerScore = 0;
        let aiScore = 0;
        // Controls
        let upPressed = false;
        let downPressed = false;
        document.addEventListener('keydown', function(e) {
            if(e.key === 'ArrowUp') upPressed = true;
            if(e.key === 'ArrowDown') downPressed = true;
        });
        document.addEventListener('keyup', function(e) {
            if(e.key === 'ArrowUp') upPressed = false;
            if(e.key === 'ArrowDown') downPressed = false;
        });
        function drawPaddle(x, y) {
            ctx.fillStyle = '#1877f2';
            ctx.fillRect(x, y, paddleWidth, paddleHeight);
        }
        function drawBall(x, y) {
            ctx.beginPath();
            ctx.arc(x, y, ballRadius, 0, Math.PI * 2);
            ctx.fillStyle = '#222';
            ctx.fill();
            ctx.closePath();
        }
        function drawScore() {
            ctx.font = '24px Arial';
            ctx.fillStyle = '#1877f2';
            ctx.fillText(playerScore, canvas.width/4, 40);
            ctx.fillText(aiScore, 3*canvas.width/4, 40);
        }
        function resetBall() {
            ballX = canvas.width / 2;
            ballY = canvas.height / 2;
            ballSpeedX = -ballSpeedX;
            ballSpeedY = 3 * (Math.random() > 0.5 ? 1 : -1);
        }
        function update() {
            // Player paddle movement
            if(upPressed && paddleY > 0) paddleY -= 7;
            if(downPressed && paddleY < canvas.height - paddleHeight) paddleY += 7;
            // AI paddle movement
            if(aiPaddleY + paddleHeight/2 < ballY) aiPaddleY += 5;
            else if(aiPaddleY + paddleHeight/2 > ballY) aiPaddleY -= 5;
            aiPaddleY = Math.max(0, Math.min(canvas.height - paddleHeight, aiPaddleY));
            // Ball movement
            ballX += ballSpeedX;
            ballY += ballSpeedY;
            // Top/bottom collision
            if(ballY - ballRadius < 0 || ballY + ballRadius > canvas.height) ballSpeedY = -ballSpeedY;
            // Player paddle collision
            if(ballX - ballRadius < paddleWidth && ballY > paddleY && ballY < paddleY + paddleHeight) {
                ballSpeedX = -ballSpeedX;
                ballX = paddleWidth + ballRadius;
            }
            // AI paddle collision
            if(ballX + ballRadius > canvas.width - paddleWidth && ballY > aiPaddleY && ballY < aiPaddleY + paddleHeight) {
                ballSpeedX = -ballSpeedX;
                ballX = canvas.width - paddleWidth - ballRadius;
            }
            // Score
            if(ballX - ballRadius < 0) {
                aiScore++;
                resetBall();
            }
            if(ballX + ballRadius > canvas.width) {
                playerScore++;
                resetBall();
            }
        }
        function draw() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            drawPaddle(0, paddleY); // Player
            drawPaddle(canvas.width - paddleWidth, aiPaddleY); // AI
            drawBall(ballX, ballY);
            drawScore();
        }
        function gameLoop() {
            update();
            draw();
            requestAnimationFrame(gameLoop);
        }
        gameLoop();
    </script>
</body>
</html>
