<h1>Практическая работа №5. Введение в разработку игр с использованием C++ и raylib</h1>
<h2>1. Инициализация окна и переменных</h2>
    <code>const int screenWidth = 800;
const int screenHeight = 450;
InitWindow(screenWidth, screenHeight, "Arkanoid на raylib");
SetTargetFPS(60);</code>
    <h2></h2>Данный код:
    <ul>
      <li>Создает окно размером 800x450 пикселей с заголовком "Arkanoid на raylib".</li>
      <li>Устанавливает частоту обновления экрана на 60 FPS.</li>
    </ul>
<h2>2. Создание игровых объектов</h2>
    <p><b>Мяч:</b> начальная позиция в центре экрана, скорость 5 по X и 4 по Y, радиус 20.</p>
    <code>Vector2 ballPosition = { (float)screenWidth / 2, (float)screenHeight / 2 };
Vector2 ballSpeed = { 5.0f, 4.0f };
int ballRadius = 20;</code>
    <p><b>Ракетка:</b> начальная позиция 50 пикселей от левого края, высота 100, ширина 20.</p>
    <code>Vector2 paddlePosition = { 50.0f, (float)screenHeight / 2 - 50.0f };
Vector2 paddleSize = { 20.0f, 100.0f };</code>
    <p><b>Счет:</b> Изначально 0.</p>
    <code>int score = 0;</code>
    <p><b></b></p>
<h2>3. Движения мяча</h2>
    <p>Мяч движется по X и Y, обновляя свою позицию.</p>
    <code>ballPosition.x += ballSpeed.x;
ballPosition.y += ballSpeed.y;</code>
    <p>Если мяч касается <b>верхней</b> или <b>нижней</b> границы, он отскакивает (меняем знак скорости по Y).</p>
    <code>if ((ballPosition.y >= (screenHeight - ballRadius)) ||
    (ballPosition.y <= ballRadius))
{
    ballSpeed.y *= -1.0f;
}</code>
      <p>Если мяч касается <b>правой границы</b>, он отскакивает (меняем знак скорости по X).</p>
      <code>if (ballPosition.x >= (screenWidth - ballRadius))
{
    ballSpeed.x *= -1.0f;
}
</code>
<p>Если мяч уходит за <b>левую границу</b>, игра сбрасывает <b>позицию мяча</b>, <b>скорость</b> и <b>счет</b>.</p>
<code>if (ballPosition.x < 0)
{
    Vector2 ballPosition = { (float)screenWidth / 2, (float)screenHeight / 2 };
    Vector2 ballSpeed = { 5.0f, 4.0f };
    score = 0;
}
</code>
<h3>4. Движение ракетки (управление мышью)</h3>
