# snake-game
<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8" />
<title>���� ������</title>
<style>
  canvas {
    border: 1px solid black;
    display: block;
    margin: 0 auto;
  }
</style>
</head>
<body>
<h2 style="text-align:center;">���� ������</h2>
<canvas id="gameCanvas" width="400" height="400"></canvas>

<script>
const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');

const box = 20;
let snake = [{x: 200, y: 200}];
let direction = 'RIGHT';
let food = {
  x: Math.floor(Math.random() * 20) * box,
  y: Math.floor(Math.random() * 20) * box
};
let score = 0;

// ���� ������
document.addEventListener('keydown', changeDirection);

function changeDirection(event) {
  if (event.keyCode == 37 && direction != 'RIGHT') {
    direction = 'LEFT';
  } else if (event.keyCode == 38 && direction != 'DOWN') {
    direction = 'UP';
  } else if (event.keyCode == 39 && direction != 'LEFT') {
    direction = 'RIGHT';
  } else if (event.keyCode == 40 && direction != 'UP') {
    direction = 'DOWN';
  }
}

function draw() {
  ctx.fillStyle = 'white';
  ctx.fillRect(0, 0, 400, 400);

  // ��� ������
  ctx.fillStyle = 'green';
  for (let part of snake) {
    ctx.fillRect(part.x, part.y, box, box);
  }

  // ��� ������
  ctx.fillStyle = 'red';
  ctx.fillRect(food.x, food.y, box, box);

  // ���� ���������� �������
  let snakeX = snake[0].x;
  let snakeY = snake[0].y;

  if (direction == 'LEFT') snakeX -= box;
  if (direction == 'UP') snakeY -= box;
  if (direction == 'RIGHT') snakeX += box;
  if (direction == 'DOWN') snakeY += box;

  // ������ �� �������� �������� �� �����
  if (
    snakeX < 0 || snakeY < 0 ||
    snakeX >= 400 || snakeY >= 400 ||
    snake.some((part, index) => index !== 0 && part.x === snakeX && part.y === snakeY)
  ) {
    alert('����� ������! �����: ' + score);
    clearInterval(game);
    return;
  }

  // ����� �����
  let newHead = {x: snakeX, y: snakeY};
  snake.unshift(newHead);

  // ������ �� ������
  if (snakeX == food.x && snakeY == food.y) {
    score++;
    food = {
      x: Math.floor(Math.random() * 20) * box,
      y: Math.floor(Math.random() * 20) * box
    };
  } else {
    snake.pop();
  }
}

const game = setInterval(draw, 200);
</script>
</body>
</html>
