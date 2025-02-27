# 抽人程序下载链接
[<button style="padding: 10px 20px; background-color: #4CAF50; color: white; border: none; border-radius: 5px;">点击下载</button>](https://www.123865.com/s/KypqVv-lnJzH)

<div class="game-container">
  <canvas id="snakeGame" width="400" height="400"></canvas>
  <div id="score">得分：0</div>
  <button id="resetBtn">重新开始</button>
</div>

<style>
/* 新增移动端优化样式 */
.game-container {
  touch-action: none; /* 禁用默认触摸行为 */
  overscroll-behavior: contain; /* 阻止页面滚动 */
}

#snakeGame {
  touch-action: none; /* 禁用画布区域的触摸滚动 */
}
</style>

<script>
// 修改后的重置按钮事件绑定
document.getElementById('resetBtn').addEventListener('click', resetGame);

// 优化后的触摸事件处理
let touchStartTime = 0;
let validTouch = false;

canvas.addEventListener('touchstart', function(e) {
  e.preventDefault();
  touchStartX = e.touches[0].clientX;
  touchStartY = e.touches[0].clientY;
  touchStartTime = Date.now();
  validTouch = true;
});

canvas.addEventListener('touchmove', function(e) {
  e.preventDefault();
  if (!validTouch) return;
  
  const touchEndX = e.touches[0].clientX;
  const touchEndY = e.touches[0].clientY;
  
  // 判断滑动有效性（防止误触）
  if (Date.now() - touchStartTime < 50) return;
  
  const deltaX = touchEndX - touchStartX;
  const deltaY = touchEndY - touchStartY;
  
  if (Math.abs(deltaX) > 10 || Math.abs(deltaY) > 10) {
    handleSwipe(deltaX, deltaY);
    validTouch = false; // 防止持续触发
  }
});

function handleSwipe(deltaX, deltaY) {
  if (Math.abs(deltaX) > Math.abs(deltaY)) {
    // 水平滑动
    changeDirection({ key: deltaX > 0 ? 'ArrowRight' : 'ArrowLeft' });
  } else {
    // 垂直滑动
    changeDirection({ key: deltaY > 0 ? 'ArrowDown' : 'ArrowUp' });
  }
}

// 强化重置功能
function resetGame() {
  snake = [{ x: 10, y: 10 }];
  dx = 0;
  dy = 0;
  score = 0;
  document.getElementById('score').textContent = '得分：0';
  generateFood();
  
  // 确保游戏循环重启
  if (typeof gameLoop !== 'undefined') cancelAnimationFrame(gameLoop);
  gameLoop = requestAnimationFrame(drawGame);
}

// 修改游戏循环为requestAnimationFrame
let gameLoop;
function drawGame() {
  // ...原有drawGame内容...
  gameLoop = requestAnimationFrame(drawGame);
}

// 初始化时启动游戏
resetGame();
</script>
