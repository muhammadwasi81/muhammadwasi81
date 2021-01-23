### Hi there 👋 I'm Muhammad wasi

Here are some ideas to get you started:

- 🔭 I’m currently working on websites and web applications
- 🌱 I’m currently learning MERN STACK..
- 📫 How to reach me: 
email: wasiarain819@gmail.com
phone: +92 3162493262

<html>
<canvas></canvas>
<h1>Muhammad wasi<span class="last"></span></h1>
  </html>
  
<style>
* {
  box-sizing: border-box;
}

html, body {
  margin: 0;
  padding: 0;
  background-color: hsla(220deg, 35%, 10%, 1);
  width: 100%;
  height: 100%;

}

body {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: clamp(12px, 2vw, 26px);
}

h1 {
  position: absolute;
  font-family: 'Roboto';
  font-weight: 100;
  text-transform: uppercase;
  letter-spacing: 1em;
  color: hsla(320deg, 100%, 95%, 0.3);
  font-size: 2em;
  animation: breathe 20000ms alternate infinite ease-in-out;
}
h1 > .last {
  letter-spacing: 0em;
}

@keyframes breathe {
  0% {
    transform: scale(1);
    color: hsla(320deg, 100%, 95%, 0.3);
  }
  100% {
    transform: scale(0.9);
    color: hsla(320deg, 100%, 95%, 0.8);
  }
}

canvas {
  width: 100%;
  height: 30em;
  box-shadow: 0 1em 2em 0.5em hsla(210deg, 35%, 0%, 0.1)
}

</style>
<script>
(function global() {
  const canvas = document.querySelector('canvas');
  const ctx = canvas.getContext('2d');
  let width;
  let height;
  function resize() {
    width = window.innerWidth;
    height = window.innerHeight;
    canvas.width = width;
    canvas.height = height;
  }
  resize();
  function animation() {
    let id;
    return function updater(fn) {
      if (id) {
        cancelAnimationFrame(id);
        id = null;
      }
      id = requestAnimationFrame(function() {
        fn().update(id);
        updater(fn);
      });
    }
  }
  function randomRange(min, max) {
    return min + Math.random() * (max - min);
  }
  function randomControlPoint(partSize, index) {
    const controlPoint = {
      x: randomRange(-partSize * index, partSize * index),
      y: randomRange(-partSize, partSize)
    }
    const magnitude = Math.hypot(controlPoint.x, controlPoint.y);
    return {
      x: ((controlPoint.x)).toFixed(0),
      y: ((controlPoint.y)).toFixed(0)
    }
  }
  function xCoord(index, partSize) {
    return (index * partSize + randomRange(-partSize / 8, partSize / 8)).toFixed(0);
  }
  function yCoord(index, partSize) {
    return (height / 2 + randomRange(-1, 1)).toFixed(0);
  }
  function reducePathVectors() {
    return function (p, v, idx) {
      if (idx === 0) {
        p = `M${v.x},${v.y}`;
        return p;
      }
      if (idx === 1) {
        p += `Q${v.dx},${v.dy},${v.x},${v.y}`
        return p;
      }
        p += `T${v.x},${v.y}`;
        return p;
    }
  }
  function generatePath() {
    const partitions = Math.floor(randomRange(3, 5));
    const partSize = width / partitions;
    const positionVectors = [];
    for(let index = 0; index <= partitions; index += 1) {
      let controlPoint = randomControlPoint(partSize, index);
      positionVectors.push({
        dx: controlPoint.x,
        dy: controlPoint.y,
        x: xCoord(index, partSize),
        y: yCoord(index, partSize),
      });
    }
    const path = positionVectors.reduce(reducePathVectors(), '');
    return path;
  }
  class Curve {
    constructor(color) {   
      this.color = color
      this.path = generatePath();
      this.scale = {x: randomRange(-1, 1), y: randomRange(-1, 1)};
      this.alpha = 0;
      this.hue = color.h
      this.rangeX = randomRange(0.99, 1.01) ** 9
      this.rangeY = randomRange(0.9, 1.1) ** 9
      this.translate = {
        tx: randomRange(-0.2, 0.5),
        ty: randomRange(-0.2, 0.5)
      };
      this.translateRange = {
        rx: randomRange(-0.5, 0.5),
        ry: randomRange(-0.5, 0.5)
      }
      this.t = 0;
      this.tIncrement = randomRange(0.0001, 0.00001);
      this.alphaOffset = randomRange(0.2, 0.8);
      this.alphaSpeed = randomRange(400, 1000);
    }
    getColorString() {
      return `hsla(${this.hue}deg,${this.color.s}%,${this.color.l}%,${this.alpha})`;
    }
    updateTranslate() {
      this.translate.x += 10 * this.translateRange.rx
      this.translate.y += 10 * this.translateRange.ry
    }
    resetScale() {
      this.rangeX = randomRange(0.99, 1.01) ** 9
      this.rangeY = randomRange(0.99, 1.01) ** 9
      this.scale = {x: randomRange(-1, 1), y: randomRange(-1, 1)};
    }
    updateScale() {
      this.scale.x += 0.001 * this.rangeX + this.t
      this.scale.y += 0.001 * this.rangeY + this.t
    }
    updateHue() {
      this.hue += Math.sin(this.t * 1000)
    }
    resetHue() {
      this.hue = this.color.h;
    }
    updateAlpha() {
      this.alpha = this.alphaOffset * Math.sin(this.t * this.alphaSpeed + 0.1) ** 2
    }
    resetAlpha() {
      this.alpha = 0;
      this.alphaOffset = randomRange(0.1, 0.6);
      this.alphaSpeed = randomRange(300, 1000);
    }
    updateT() {
      this.t += this.tIncrement
    }
    resetT() {
      if (Math.random() < 0.9) {
        this.t = 0;
      }
    }
    rotate() {
      this.rotation += this.t;
    }
    update() {
      this.updateT()
      this.updateScale()
      this.updateHue();
      this.rotate();
      this.alpha <= 1 && this.updateAlpha()
      if (this.alpha < 0.001) {
        this.resetHue()
        this.path = generatePath();
        this.resetAlpha();
        this.resetScale();
        this.resetT();
      }
      return this;
    }
    draw() {
      ctx.save();
      ctx.beginPath();
      ctx.strokeStyle = this.getColorString();
      ctx.rotate(this.rotation);
      ctx.translate(width / 2, height / 2);
      ctx.scale(this.scale.x, this.scale.y);
      ctx.stroke(new Path2D(this.path));
      ctx.restore()
      return this;
    }
  }
  function fader() {
    var gradient = ctx.createRadialGradient(width / 2,height / 2,0,width / 2,height / 2, Math.max(width / 2, height / 2));

    gradient.addColorStop(0, `hsla(220deg, 35%, 15%, 0.2)`);
    gradient.addColorStop(1, `hsla(220deg, 35%, 15%, 0.02)`);

    ctx.fillStyle = gradient;
    ctx.fillRect(0,0,width,height);
  }
  const animator = animation();
  function actions() {
    resize();
    const c = [];
    for (let i = 0; i < 30; i += 1) {
      c.push(new Curve({h:340, s:100, l:50, a:1}).draw())
    }
    
    animator(function() {
      return {
        update: (frameId) => {
          if (!(frameId % 4)) {
            fader();
          }
          c.forEach(d => d.update().draw());
        },
      }
    });

  }
  actions();
  window.addEventListener('resize', () => {
    requestAnimationFrame(actions)
  }, {passive: true});
}());
</script>
