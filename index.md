# 抽人程序下载链接
[<button style="padding: 10px 20px; background-color: #4CAF50; color: white; border: none; border-radius: 5px;">点击下载</button>](https://www.123865.com/s/KypqVv-lnJzH)

<!-- 在需要显示游戏的位置插入这个容器 -->
<div class="game-container">
  <canvas id="snakeGame" width="400" height="400"></canvas>
  <div id="score">得分：0</div>
  <button onclick="resetGame()">重新开始</button>
</div>

<style>
.game-container {
  text-align: center;
  margin: 20px auto;
  max-width: 400px;
}

#snakeGame {
  border: 2px solid #333;
  background: #000;
  border-radius: 8px;
}

button {
  padding: 10px 20px;
  background: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  margin-top: 10px;
  cursor: pointer;
}
</style>

<script>
const canvas = document.getElementById('snakeGame');
const ctx = canvas.getContext('2d');
const gridSize = 20;
const tileCount = canvas.width / gridSize;

let snake = [
  { x: 10, y: 10 }
];
let food = { x: 15, y: 15 };
let dx = 0;
let dy = 0;
let score = 0;

// 控制方向（支持触控滑动）
let touchStartX = 0;
let touchStartY = 0;

document.addEventListener('keydown', changeDirection);
canvas.addEventListener('touchstart', handleTouchStart);
canvas.addEventListener('touchmove', handleTouchMove);

function handleTouchStart(e) {
  touchStartX = e.touches[0].clientX;
  touchStartY = e.touches[0].clientY;
}

function handleTouchMove(e) {
  if (!touchStartX) return;
  
  let touchEndX = e.touches[0].clientX;
  let touchEndY = e.touches[0].clientY;
  
  let dx = touchEndX - touchStartX;
  let dy = touchEndY - touchStartY;
  
  if (Math.abs(dx) > Math.abs(dy)) {
    changeDirection({ key: dx > 0 ? 'ArrowRight' : 'ArrowLeft' });
  } else {
    changeDirection({ key: dy > 0 ? 'ArrowDown' : 'ArrowUp' });
  }
  
  touchStartX = null;
}

function changeDirection(e) {
  const LEFT_KEY = 37, RIGHT_KEY = 39, UP_KEY = 38, DOWN_KEY = 40;
  
  const keyPressed = e.keyCode ? e.keyCode : e.key.replace('Arrow', '');
  const goingUp = dy === -1;
  const goingDown = dy === 1;
  const goingRight = dx === 1;
  const goingLeft = dx === -1;

  if (keyPressed === 'Left' || keyPressed === LEFT_KEY) {
    if (!goingRight) { dx = -1; dy = 0; }
  }
  if (keyPressed === 'Up' || keyPressed === UP_KEY) {
    if (!goingDown) { dx = 0; dy = -1; }
  }
  if (keyPressed === 'Right' || keyPressed === RIGHT_KEY) {
    if (!goingLeft) { dx = 1; dy = 0; }
  }
  if (keyPressed === 'Down' || keyPressed === DOWN_KEY) {
    if (!goingUp) { dx = 0; dy = 1; }
  }
}

function drawGame() {
  // 移动蛇
  const head = { x: snake[0].x + dx, y: snake[0].y + dy };
  snake.unshift(head);

  // 吃到食物
  if (head.x === food.x && head.y === food.y) {
    score += 10;
    document.getElementById('score').textContent = `得分：${score}`;
    generateFood();
  } else {
    snake.pop();
  }

  // 碰撞检测
  if (isGameOver()) {
    alert(`游戏结束！得分：${score}`);
    resetGame();
    return;
  }

  // 清空画布
  ctx.fillStyle = '#000';
  ctx.fillRect(0, 0, canvas.width, canvas.height);

  // 绘制蛇
  ctx.fillStyle = '#4CAF50';
  snake.forEach((segment, index) => {
    ctx.fillRect(segment.x * gridSize, segment.y * gridSize, gridSize-2, gridSize-2);
    if (index === 0) { // 蛇头
      ctx.fillStyle = '#45a049';
    }
  });

  // 绘制食物
  ctx.fillStyle = '#ff0000';
  ctx.beginPath();
  ctx.arc(
    food.x * gridSize + gridSize/2,
    food.y * gridSize + gridSize/2,
    gridSize/2 - 2,
    0,
    Math.PI * 2
  );
  ctx.fill();

  setTimeout(drawGame, 100);
}

function generateFood() {
  food.x = Math.floor(Math.random() * tileCount);
  food.y = Math.floor(Math.random() * tileCount);
  // 确保食物不在蛇身上
  snake.forEach(segment => {
    if (segment.x === food.x && segment.y === food.y) generateFood();
  });
}

function isGameOver() {
  const head = snake[0];
  return (
    head.x < 0 || head.x >= tileCount ||
    head.y < 0 || head.y >= tileCount ||
    snake.slice(1).some(segment => segment.x === head.x && segment.y === head.y)
  );
}

function resetGame() {
  snake = [{ x: 10, y: 10 }];
  dx = 0;
  dy = 0;
  score = 0;
  document.getElementById('score').textContent = '得分：0';
  generateFood();
}

// 开始游戏
generateFood();
drawGame();
</script>
