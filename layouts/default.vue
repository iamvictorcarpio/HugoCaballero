<template>
  <main class="overflow-hidden">
    <canvas id="starfield" class="absolute w-screen h-screen bg-theme-black" />
    <nuxt class="absolute" />
    <aside class="hidden">
      <audio id="intro" preload="auto">
        <source
          src="~/assets/media/audio/star-wars-intro.mp3"
          type="audio/mpeg"
        />
        <p>Tu navegador no implementa el elemento audio.</p>
      </audio>
      <audio id="ambiental" preload="auto" loop>
        <source
          src="~/assets/media/audio/star-wars-ambiental.mp3"
          type="audio/mpeg"
        />
        <p>Tu navegador no implementa el elemento audio.</p>
      </audio>
      <audio id="alarm" preload="auto" loop>
        <source src="~/assets/media/audio/alarm-effect.mp3" type="audio/mpeg" />
        <p>Tu navegador no implementa el elemento audio.</p>
      </audio>
      <audio id="door" preload="auto" loop>
        <source src="~/assets/media/audio/door-effect.mp3" type="audio/mpeg" />
        <p>Tu navegador no implementa el elemento audio.</p>
      </audio>
      <audio id="typing" preload="auto" loop>
        <source
          src="~/assets/media/audio/typing-sound-effect.mp3"
          type="audio/mpeg"
        />
        <p>Tu navegador no implementa el elemento audio.</p>
      </audio>
    </aside>
  </main>
</template>

<script>
const DEFAULT_STARS_NUMBER = 120;
const COLOR_RANGE = [0, 60, 240];
function getRandom(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

export default {
  mounted() {
    const canvas = document.getElementById('starfield');
    const context = canvas.getContext('2d');
    const { innerWidth, innerHeight } = window;
    const startsNumber = (innerWidth / innerHeight) * 10 * DEFAULT_STARS_NUMBER;

    canvas.width = innerWidth;
    canvas.height = innerHeight;

    for (let i = 0; i < startsNumber; i++) {
      const x = Math.random() * canvas.offsetWidth;
      const y = Math.random() * canvas.offsetHeight;
      const radius = Math.random() * 0.2;
      const hue = COLOR_RANGE[getRandom(0, COLOR_RANGE.length - 1)];
      const sat = getRandom(50, 100);

      context.beginPath();
      context.arc(x, y, radius, 0, 360);
      context.fillStyle = 'hsl(' + hue + ', ' + sat + '%, 88%)';
      context.fill();
    }
  }
};
</script>
