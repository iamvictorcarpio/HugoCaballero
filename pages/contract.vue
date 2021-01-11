<template>
  <div
    class="global bg-theme-black w-screen h-screen flex h-full items-center justify-center flex-col"
  >
    <div
      class="hint text-center fixed top-0 mt-8 z-10 text-theme-yellow w-full"
      to="/contract"
    >
      <div class="px-4 m-2">{{ hint }}</div>
    </div>
    <audio preload="auto" loop>
      <source
        src="~/assets/media/audio/star-wars-ambiental.mp3"
        type="audio/mpeg"
      />
      <p>Tu navegador no implementa el elemento audio.</p>
    </audio>
    <section class="w-3/4 my-1/2 bg-theme-white mx-auto p-4 text-center">
      <div class="question">
        <h1 class="text-center">{{ title }}</h1>
        <div class="m-6 text-xs">
          {{ question }}
          <input disabled class="mt-4 text-center w-full pb-1" type="text" />
          <div class="mt-6 w-full text-right">
            <button
              disabled
              class="px-4 py-2 border bg-theme-yellow rounded-md"
              @click="submit"
            >
              acceder
            </button>
          </div>
        </div>
      </div>
      <div class="hidden feedback text-center" />
    </section>
  </div>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      title: '',
      question: '',
      hint: 'espere a la descarga de datos...'
    };
  },
  mounted() {
    const input = this.$el.querySelector('input');
    const audio = document.querySelector('#ambiental');
    const hint = this.$el.querySelector('.hint');
    const button = this.$el.querySelector('button');
    const typing = document.querySelector('#typing');
    let title = 'datos de acceso';
    let text = 'en qué año se inauguró el observatorio fabra de barcelona?';

    audio.play();
    typing.play();

    const interval = setInterval(() => {
      this.title += title.slice(0, 1);
      title = title.slice(1);
      if (title === '') {
        this.question += text.slice(0, 1);
        text = text.slice(1);
        if (text === '') {
          typing.pause();
          clearInterval(interval);
          this.hint = 'datos descargados';
          hint.classList.remove('hint');
          input.disabled = false;
          button.disabled = false;
        }
      }
    }, 120);
  },
  methods: {
    submit() {
      const value = this.$el.querySelector('input').value;
      const question = this.$el.querySelector('.question');
      const feedback = this.$el.querySelector('.feedback');

      question.classList.add('hidden');
      if (value === '1904') {
        const audio = document.querySelector('#door');

        audio.play();
        feedback.classList.remove('feedback');
        feedback.innerHTML = `<p>bienvenido Hugo</p><br />
          <p>encuentra una persona de confianza para la misión</p><br/>
          <p>victor te dará los detalles</p>`;
        setTimeout(() => {
          feedback.classList.add('feedback');
          feedback.textContent = 'redirigiendo al objetivo';
          setTimeout(() => {
            window.location.href = 'https://www.youtube.com/embed/7WlphzFbwL4';
          }, 3000);
        }, 6000);
      } else {
        const audio = document.querySelector('#alarm');

        audio.play();
        feedback.classList.add('text-theme-red');
        feedback.textContent = 'datos incorrectos';
        setTimeout(() => {
          feedback.classList.add('hidden');
          feedback.classList.remove('text-theme-red');
          question.classList.remove('hidden');
          audio.pause();
        }, 3000);
      }

      feedback.classList.remove('hidden');
    }
  }
};
</script>

<style scoped>
button:disabled {
  background-color: #dddddd;
  pointer-events: none;
}

.global {
  font-family: 'Star-wars';
}

input {
  @apply inline-block border-b;
}

input:hover,
input:focus {
  @apply outline-none;
}

.hint {
  animation: flash linear 2s infinite;
}

.feedback {
  animation: flash ease-in-out 1.4s infinite;
}

@keyframes flash {
  0% {
    opacity: 1;
  }
  50% {
    opacity: 0.1;
  }
  100% {
    opacity: 1;
  }
}
</style>
