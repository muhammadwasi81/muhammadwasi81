### Hi there 👋 I'm Muhammad wasi

Here are some ideas to get you started:

- 🔭 I’m currently working on websites and web applications
- 🌱 I’m currently learning MERN STACK..
- 📫 How to reach me: 
email: wasiarain819@gmail.com
phone: +92 3162493262

<div id="particles-js"></div> <!-- stats - count particles -->
<div class="count-particles"> <span class="js-count-particles">--</span> particles </div> <!-- particles.js lib - https://github.com/VincentGarreau/particles.js -->
<script src="http://cdn.jsdelivr.net/particles.js/2.0.0/particles.min.js"></script> <!-- stats.js lib -->
<script src="http://threejs.org/examples/js/libs/stats.min.js"></script>

/* ---- reset ---- */
body {
  margin: 0;
  font: normal 75% Arial, Helvetica, sans-serif;
}
canvas {
  display: block;
  vertical-align: bottom;
} /* ---- particles.js container ---- */
#particles-js {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: #b61924;
  background-image: url("");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 50% 50%;
} /* ---- stats.js ---- */
.count-particles {
  background: #000022;
  position: absolute;
  top: 48px;
  left: 0;
  width: 80px;
  color: #13e8e9;
  font-size: 0.8em;
  text-align: left;
  text-indent: 4px;
  line-height: 14px;
  padding-bottom: 2px;
  font-family: Helvetica, Arial, sans-serif;
  font-weight: bold;
}
.js-count-particles {
  font-size: 1.1em;
}
#stats,
.count-particles {
  -webkit-user-select: none;
  margin-top: 5px;
  margin-left: 5px;
}
#stats {
  border-radius: 3px 3px 0 0;
  overflow: hidden;
}
.count-particles {
  border-radius: 0 0 3px 3px;
}


particlesJS("particles-js", {
  particles: {
    number: { value: 80, density: { enable: true, value_area: 800 } },
    color: { value: "#ffffff" },
    shape: {
      type: "circle",
      stroke: { width: 0, color: "#000000" },
      polygon: { nb_sides: 5 },
      image: { src: "img/github.svg", width: 100, height: 100 }
    },
    opacity: {
      value: 0.5,
      random: false,
      anim: { enable: false, speed: 1, opacity_min: 0.1, sync: false }
    },
    size: {
      value: 3,
      random: true,
      anim: { enable: false, speed: 40, size_min: 0.1, sync: false }
    },
    line_linked: {
      enable: true,
      distance: 150,
      color: "#ffffff",
      opacity: 0.4,
      width: 1
    },
    move: {
      enable: true,
      speed: 6,
      direction: "none",
      random: false,
      straight: false,
      out_mode: "out",
      bounce: false,
      attract: { enable: false, rotateX: 600, rotateY: 1200 }
    }
  },
  interactivity: {
    detect_on: "canvas",
    events: {
      onhover: { enable: true, mode: "repulse" },
      onclick: { enable: true, mode: "push" },
      resize: true
    },
    modes: {
      grab: { distance: 400, line_linked: { opacity: 1 } },
      bubble: { distance: 400, size: 40, duration: 2, opacity: 8, speed: 3 },
      repulse: { distance: 200, duration: 0.4 },
      push: { particles_nb: 4 },
      remove: { particles_nb: 2 }
    }
  },
  retina_detect: true
});
var count_particles, stats, update;
stats = new Stats();
stats.setMode(0);
stats.domElement.style.position = "absolute";
stats.domElement.style.left = "0px";
stats.domElement.style.top = "0px";
document.body.appendChild(stats.domElement);
count_particles = document.querySelector(".js-count-particles");
update = function () {
  stats.begin();
  stats.end();
  if (window.pJSDom[0].pJS.particles && window.pJSDom[0].pJS.particles.array) {
    count_particles.innerText = window.pJSDom[0].pJS.particles.array.length;
  }
  requestAnimationFrame(update);
};
requestAnimationFrame(update);
