<template>
    <canvas id="canvas"></canvas>
</template>

<script>
export default {
  name: 'Canvas',
  methods: {
      updateCanvas: function() {
          var canvas = document.getElementById("canvas");
          var ctx = canvas.getContext('2d');
          var innerWidth = canvas.width = window.innerWidth;
          var innerHeight = canvas.height = window.innerHeight;

          function Dot(x, y, vx, vy, radius) {
              this.x = x;
              this.y = y;
              this.vx = vx;
              this.vy = vy;
              this.radius = radius;

              this.draw = function() {
                  ctx.beginPath();
                  ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2, false);
                  ctx.fillStyle = "#333";
                  ctx.fill();
              };

              this.update = function() {
                  this.handleCollision();
                  this.handleMovement();
              };

              this.handleMovement = function() {
                  this.x += this.vx;
                  this.y += this.vy;

                  this.draw();
              };

              this.handleCollision = function() {
                  if (this.x + this.radius > innerWidth || this.x - this.radius < 0) {
                      this.vx = -this.vx;
                  }

                  if (this.y + this.radius > innerHeight || this.y - this.radius < 0) {
                      this.vy = -this.vy;
                  }
              };
          }

          var dots = [];

          for(var i = 0; i < 100; i++) {
              var radius = Math.random() * 5;
              var x = Math.random() * (innerWidth - radius * 2) + radius;
              var y = Math.random() * (innerHeight - radius * 2) + radius;
              var vx = Math.random() - 0.5;
              var vy = Math.random() - 0.5;

              dots.push(new Dot(x, y, vx, vy, radius));
          }

          function animate() {
            requestAnimationFrame(animate);
            ctx.clearRect(0, 0, innerWidth, innerHeight);

              dots.forEach((dot, i) => {
                  dot.update();
              });
          }

          animate();
      }
  },
  data() {
    return {

    }
  },
  mounted() {
      this.updateCanvas();
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
#canvas {
  position: absolute;
  left: 0;
  top: 0;
}
</style>
