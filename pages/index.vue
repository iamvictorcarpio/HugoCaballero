<template>
  <div class="w-screen h-screen overflow-hidden">
    <NuxtLink
      class="hidden link text-center z-10 h-full flex text-theme-yellow items-center justify-center w-full"
      to="/contract"
    >
      <div class="border-theme-yellow border px-4 py-2 m-2">Aceptar mision</div>
    </NuxtLink>
    <aside
      class="blackout flex h-full text-theme-yellow items-center justify-center flex-col z-10 mx-2"
    >
      <div
        class="alert text-center p-4 border-2 border-theme-yellow rounded-lg"
      >
        <p>
          Mensaje de la resistencia para:<br />
          Hugo Caballero
        </p>
        <div class="mt-2 text-center">
          <button
            class="px-3 py-2 mt-1 border border-theme-yellow rounded-lg"
            @click="startIntro"
          >
            Abrir
          </button>
        </div>
      </div>
      <div class="hidden intro text-center">Perreo<br />Wars</div>
    </aside>
    <audio>
      <source
        src="~/assets/media/audio/star-wars-intro.mp3"
        type="audio/mpeg"
      />
      <p>Tu navegador no implementa el elemento audio.</p>
    </audio>
    <div class="fade"></div>
    <section class="star-wars">
      <div class="crawl text-theme-yellow">
        <div class="title">
          <p>Episodio IV</p>
          <h1>Una nueva esperanza</h1>
        </div>

        <p>
          En un momento complicado para la humanidad, los rebeldes, conocidos
          como Perríto Susio, siguen amenazando y atemorizando toda la humanidad
          con sus implacables políticas.
        </p>

        <p>
          Desde el planeta Influencer, Anna Malignus sigue trabajando en el
          desarrollo de una máquina influencer para alargar los días. Quiere
          controlar las mentes de los humanos a través de su contenido barato de
          Instagram y TikTok.
        </p>

        <p>
          Además, parece que ha vuelto una de nuestras grandes adversarias,
          Opositorus Alba vuelve a amenazar la inteligencia mundial. Después de
          haber pasado 359 años estudiando, su intelecto no es alcanzable por
          ningún habitante de las 900 galaxias conocidas ni por los
          superordenadores.
        </p>

        <p>
          Rubén Houses, Doctor Honoris Causa licenciado por la Universidad de
          Liechestein, está acabando de ultimar un estudio en el que demuestra
          que la humanidad es gilipollas, de ser así todos seríamos gilipollas y
          nos extinguiríamos instantaneamente.
        </p>

        <p>
          "La paka", también apodada Blanca. Se le atribuye la mayor expropición
          hasta el momento, incluyendo las islas pitiusas, Soria, Venus y el
          Almo2bar. Su posterior coronación como la líder suprema le permite
          obligar a todos sus habitantes a escuchar cada día a las grecas.
        </p>

        <p>
          Vera "The fiesta", ha estado desaparecida durante un tiempo después de
          que fuera desterrada de Splash 3.14. Estuvo apunto de salirse con la
          suya de obtener el control del planeta y bebida, desgraciadamente para
          ella, fue expulsada a tiempo. Según nuestros informadores la han visto
          deambular sus alrededores otra vez, no descartamos un ataque
          premeditado.
        </p>

        <p>
          Albert "Colau", integrante del clan de los Colau. Este clan desterró
          del universo a Eduardo Inda, a los cuñaos y a los del fachaleco.
          Gracias a ellos el universo es algo mejor, pero sospechamos que Albert
          quiere tomar el mando del clan, y no tenemos aún claras sus
          intenciones.
        </p>
        <p>
          Y por último, mejor no meterse con este, Alex ELPI34. Huído de la
          cárcel interespacial de 4 vías lácteas. Se sospecha que actualmente se
          dedica al narcotráfico de porras y chocolate entre el planeta Lloreda
          4 y Pomar 5.
        </p>
        <p>Para Hugo:</p>
        <p>
          Necesitamos que te dirijas a nuestro transmisor de comunicaciones aquí
          en la Tierra y nos comuniques todo lo que has visto y aprendido de
          ellos en todo este tiempo. Si estás de acuerdo haz click en "Aceptar
          Misión" seguidamente.
        </p>
      </div>
    </section>
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

      window.document.documentElement.requestFullscreen();
      alert.classList.add('hidden');
      audio.play();
      intro.classList.remove('hidden');

      link.addEventListener('click', () => {
        this.$router.push('/contract');
      });
      audio.addEventListener('ended', () => {
        link.classList.remove('hidden');
      });
      intro.addEventListener('animationend', () => {
        const crawlEnding = this.$el.querySelector('.crawl > p:last-of-type');
        blackout.classList.add('hidden');
        const observer = new IntersectionObserver(
          ([entry]) => {
            if (
              entry.intersectionRatio === 0 &&
              entry.boundingClientRect.top > 0 &&
              entry.boundingClientRect.left > 0
            ) {
              observer.unobserve(entry.target);
              link.classList.remove('hidden');
            }
          },
          {
            root: this.$el.querySelector('.star-wars')
          }
        );

        observer.observe(crawlEnding);
        crawl.classList.add('start-crawl');
      });
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
  animation: logo 5s linear 2s forwards;
}

.fade {
  position: relative;
  width: 100%;
  min-height: 62%;
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
  letter-spacing: 2px;
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
  animation: crawl 125s linear;
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
    transform: rotateX(20deg) translateY(0) translateZ(0);
  }

  98% {
    opacity: 1;
  }

  100% {
    top: -1000%;
    opacity: 0;
    transform: rotateX(25deg) translateY(-1700%) translateZ(-3000px);
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
