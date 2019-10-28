<template>
  <canvas id="canvas"></canvas>
</template>

<script>

let canvas;
let ctx;
let cw, cx, ch, cy;
let linesNum = 16;
let linesRy = [];
let requestId = null;

function Line(flag) {
  this.flag = flag;
  this.a = {};
  this.b = {};
  if (flag == "v") {
    this.a.y = 0;
    this.b.y = ch;
    this.a.x = randomIntFromInterval(0, ch);
    this.b.x = randomIntFromInterval(0, ch);
  } else if (flag == "h") {
    this.a.x = 0;
    this.b.x = cw;
    this.a.y = randomIntFromInterval(0, cw);
    this.b.y = randomIntFromInterval(0, cw);
  }
  this.va = randomIntFromInterval(25, 100) / 100;
  this.vb = randomIntFromInterval(25, 100) / 100;

  this.draw = () => {
    ctx.strokeStyle = "rgb(47, 43, 56)";
    ctx.beginPath();
    ctx.moveTo(this.a.x, this.a.y);
    ctx.lineTo(this.b.x, this.b.y);
    ctx.stroke();
  };

  this.update = () => {
    if (this.flag == "v") {
      this.a.x += this.va;
      this.b.x += this.vb;
    } else if (flag == "h") {
      this.a.y += this.va;
      this.b.y += this.vb;
    }

    this.edges();
  };

  this.edges = function() {
    if (this.flag == "v") {
      if (this.a.x < 0 || this.a.x > cw) {
        this.va *= -1;
      }
      if (this.b.x < 0 || this.b.x > cw) {
        this.vb *= -1;
      }
    } else if (flag == "h") {
      if (this.a.y < 0 || this.a.y > ch) {
        this.va *= -1;
      }
      if (this.b.y < 0 || this.b.y > ch) {
        this.vb *= -1;
      }
    }
  };
}

function Draw() {
  requestId = window.requestAnimationFrame(Draw);
  ctx.clearRect(0, 0, cw, ch);

  for (let i = 0; i < linesRy.length; i++) {
    let l = linesRy[i];
    l.draw();
    l.update();
  }
  for (let i = 0; i < linesRy.length; i++) {
    let l = linesRy[i];
    for (let j = i + 1; j < linesRy.length; j++) {
      let l1 = linesRy[j];
      Intersect2lines(l, l1);
    }
  }
}

function Intersect2lines(l1, l2) {
  let p1 = l1.a,
    p2 = l1.b,
    p3 = l2.a,
    p4 = l2.b;
  let denominator =
    (p4.y - p3.y) * (p2.x - p1.x) - (p4.x - p3.x) * (p2.y - p1.y);
  let ua =
    ((p4.x - p3.x) * (p1.y - p3.y) - (p4.y - p3.y) * (p1.x - p3.x)) /
    denominator;
  let ub =
    ((p2.x - p1.x) * (p1.y - p3.y) - (p2.y - p1.y) * (p1.x - p3.x)) /
    denominator;
  let x = p1.x + ua * (p2.x - p1.x);
  let y = p1.y + ua * (p2.y - p1.y);
  if (ua > 0 && ub > 0) {
    markPoint({
      x: x,
      y: y
    });
  }
}

function markPoint(p) {
  ctx.beginPath();
  ctx.arc(p.x, p.y, 1, 0, 2 * Math.PI);
  ctx.fillStyle = "#fff";
  ctx.fill();
}

function randomIntFromInterval(mn, mx) {
  return ~~(Math.random() * (mx - mn + 1) + mn);
}

export default {
  mounted() {
    // 监听屏幕变化，变化后重置canvas
    window.addEventListener("scroll", this.scrollToTop);
    this.initCanvas();
    // 定时器，动画
    requestAnimationFrame(() => {
      this.Init();
      addEventListener("resize", this.initCanvas, false);
    })
  },
  methods: {
    initCanvas() {
      linesRy.length = 0;
      canvas = document.getElementById("canvas");
      ctx = canvas.getContext("2d");
      cw = canvas.width = window.innerWidth;
      cx = cw / 2;
      (ch = canvas.height = window.innerHeight), (cy = ch / 2);
      for (let i = 0; i < linesNum; i++) {
        let flag = i % 2 == 0 ? "h" : "v";
        let l = new Line(flag);
        linesRy.push(l);
      }
    },
    Init() {
      linesRy.length = 0;
      for (let i = 0; i < linesNum; i++) {
        let flag = i % 2 == 0 ? "h" : "v";
        let l = new Line(flag);
        linesRy.push(l);
      }

      if (requestId) {
        window.cancelAnimationFrame(requestId);
        requestId = null;
      }

      (cw = canvas.width = window.innerWidth), (cx = cw / 2);
      (ch = canvas.height = window.innerHeight), (cy = ch / 2);

      Draw();
    }
  }
}
</script>

<style lang="less" scoped>
#canvas {
  position: fixed;
  top: 0;
  left: 0;
  z-index: -1;
  background: #100e17;
}
</style>