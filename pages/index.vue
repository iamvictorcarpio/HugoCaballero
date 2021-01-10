<template>
  <div class="bg-theme-black w-screen h-screen overflow-hidden">
    <aside
      class="blackout flex h-full text-theme-yellow items-center justify-center flex-col z-10 mx-2"
    >
      <div class="alert p-4 border-2 border-theme-yellow rounded-lg">
        <p>Este es un mensaje para Hugo Caballero</p>
        <div class="mt-2 text-right">
          <button
            @click="startIntro"
            class="px-2 py-1 border border-theme-yellow rounded-lg"
          >
            Proceder
          </button>
        </div>
      </div>
      <div class="hidden intro">Hugo<br />Wars</div>
    </aside>
    <audio>
      <source src="~/assets/media/audio/star-wars.mp3" type="audio/mpeg" />
      <p>Tu navegador no implementa el elemento audio.</p>
    </audio>
    <div class="fade"></div>
    <section class="star-wars">
      <div class="crawl">
        <div class="title">
          <p>Episode IV</p>
          <h1>A New Hope</h1>
        </div>

        <p>
          It is a period of civil war. Rebel spaceships, striking from a hidden
          base, have won their first victory against the evil Galactic Empire.
        </p>

        <p>
          During the battle, Rebel spies managed to steal secret plans to the
          Empire’s ultimate weapon, the DEATH STAR, an armored space station
          with enough power to destroy an entire planet.
        </p>

        <p>
          Pursued by the Empire’s sinister agents, Princess Leia races home
          aboard her starship, custodian of the stolen plans that can save her
          people and restore freedom to the galaxy….
        </p>
      </div>
    </section>
    <NuxtLink
      class="hidden link text-center fixed bottom-0 mb-1 z-10 text-theme-yellow w-full"
      to="/contract"
    >
      <div class="border-theme-yellow border px-4 py-2 m-2">
        Aceptar condiciones
      </div>
    </NuxtLink>
  </div>
</template>
<script>
export default {
  components: {},
  mounted() {},
  methods: {
    startIntro() {
      const audio = this.$el.querySelector('audio');
      const alert = this.$el.querySelector('.alert');
      const intro = this.$el.querySelector('.intro');
      const blackout = this.$el.querySelector('.blackout');
      const crawl = this.$el.querySelector('.crawl');
      const link = this.$el.querySelector('.link');

      alert.classList.add('hidden');
      audio.play();
      intro.classList.remove('hidden');
      link.addEventListener('click', () => {
        this.$router.push('/contract');
      });
      audio.addEventListener('ended', () => {
        link.classList.remove('hidden');
      });
      crawl.addEventListener('animationend', () => {
        link.classList.remove('hidden');
      });

      setTimeout(() => {
        blackout.classList.add('hidden');
        crawl.classList.add('start-crawl');
      }, 8500);
    }
  }
};
</script>

<style>
.blackout,
.link {
  font-family: 'Star-wars';
}

.intro {
  line-height: 1;
  transform: scale(3);
  animation: logo 8s ease 3s forwards;
}

.fade {
  position: relative;
  width: 100%;
  min-height: 60vh;
  background-image: linear-gradient(0deg, transparent, black 75%);
  z-index: 1;
}

.star-wars {
  display: flex;
  justify-content: center;
  position: relative;
  height: 800px;
  color: #feda4a;
  font-family: 'Pathway Gothic One', sans-serif;
  font-size: 500%;
  font-weight: 600;
  letter-spacing: 6px;
  line-height: 200%;
  perspective: 400px;
  text-align: justify;
}

.crawl {
  position: relative;
  top: 100vh;
  transform-origin: 50% 200%;
  flex-shrink: 0;
  width: 250%;
}

.start-crawl {
  animation: crawl 50s linear;
}

.crawl > .title {
  font-size: 90%;
  text-align: center;
}

.crawl > .title h1 {
  margin: 0 0 100px;
  text-transform: uppercase;
}

.crawl > p {
  margin: 10% 0;
}

@keyframes crawl {
  0% {
    top: 0;
    transform: rotateX(20deg) translateZ(0);
  }
  100% {
    top: -1000%;
    transform: rotateX(25deg) translateZ(-3000px);
  }
}

@keyframes logo {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
    transform: scale(1);
  }
}
</style>
