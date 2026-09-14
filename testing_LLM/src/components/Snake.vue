<template>
    <div class="snake-game">
        <canvas ref="gameCanvas" width="400" height="400"></canvas>
    </div>
</template>

<script>
export default {
    data() {
        return {
            snake: [{x: 200, y: 200}, {x: 190, y: 200}, {x: 180, y: 200}],
            food: {x: Math.floor(Math.random() * 40) * 10, y: Math.floor(Math.random() * 40) * 10},
            direction: 'right',
            score: 0,
            gameOver: false,
            length: 4
        }
    },

    mounted() {
        this.draw();
        this.intervalId = setInterval(() => {
                if (!this.gameOver) {
                    this.update();
                    this.draw();
                } else {
                    alert("Game Over");
                    this.gameOver = false;
                    this.score = 0;
                    this.direction = 'right';
                    this.food = {x: Math.floor(Math.random() * 40) * 10, y: Math.floor(Math.random() * 40) * 10};
                    this.snake = [{x: 200, y: 200}, {x: 190, y: 200}, {x: 180, y: 200}];
                    this.length = 4
                }
            },
            100);
    },

    methods: {
        draw() {
            const canvas = this.$refs.gameCanvas;
            const ctx = canvas.getContext('2d');
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            // Draw snake
            for (let i = 0; i < this.snake.length; i++) {
                ctx.fillStyle = 'green';
                ctx.fillRect(this.snake[i].x, this.snake[i].y, 10, 10);
            }
            // Draw food
            ctx.fillStyle = 'red';
            ctx.fillRect(this.food.x, this.food.y, 10, 10);
            // Display score
            ctx.font = '24px Arial';
            ctx.fillStyle = 'black';
            ctx.textAlign = 'left';
            ctx.textBaseline = 'top';
            ctx.fillText(`Score: ${this.score}`, 10, 10);
        },

        update() {
            const canvas = this.$refs.gameCanvas;
            const ctx = canvas.getContext('2d');

            // Add keyboard event listener here
            document.addEventListener('keydown', (event) => {
                switch (event.key) {
                    case 'w':
                        if (!this.gameOver) {
                            this.direction = 'up';
                        }
                        break;
                    case 's':
                        if (!this.gameOver) {
                            this.direction = 'down';
                        }
                        break;
                    case 'a':
                        if (!this.gameOver) {
                            this.direction = 'left';
                        }
                        break;
                    case 'd':
                        if (!this.gameOver) {
                            this.direction = 'right';
                        }
                        break;
                }
            });

            // Move snake
            let headX = this.snake[0].x;
            let headY = this.snake[0].y;

            switch (this.direction) {
                case 'up':
                    headY -= 10;
                    break;
                case 'down':
                    headY += 10;
                    break;
                case 'left':
                    headX -= 10;
                    break;
                case 'right':
                    headX += 10;
                    break;

            }

            var ate = false;

            // Check collision with food
            if (headX === this.food.x && headY === this.food.y) {
                this.score++;
                this.food = {x: Math.floor(Math.random() * 40) * 10, y: Math.floor(Math.random() * 40) * 10};
                ate = true;
            }

            // Check collision with border
            if (headX < 0 || headY < 0 || headX >= canvas.width || headY >= canvas.height) {
                this.gameOver = true;
            }

            // Check collision with self
            for (let i = 1; i < this.snake.length; i++) {
                if (
                    headX === this.snake[i].x &&
                    headY === this.snake[i].y
                ) {
                    this.gameOver = true;
                }
            }

            // Update snake head
            this.snake.unshift({x: headX, y: headY});

            // Remove last element in snake array
            if (this.snake.length > this.length && !ate) {
                this.snake.pop();
            }

            if (ate) {
                this.length ++;
            }
        },
    },
}
</script>

<style>
.snake-game {
    position: relative;
    width: 400px;
    height: 400px;
}

.snake-game canvas {
    border: 1px solid black;
}
</style>