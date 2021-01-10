<template>
  <div
    class="global bg-theme-black w-screen h-screen flex h-full items-center justify-center flex-col"
  >
    <div
      class="hint text-center fixed top-0 mt-4 z-10 text-theme-yellow w-full"
      to="/contract"
    >
      <div class="px-4 m-2">{{ hint }}</div>
    </div>
    <audio>
      <source
        src="~/assets/media/audio/star-wars-ambiental.mp3"
        type="audio/mpeg"
      />
      <p>Tu navegador no implementa el elemento audio.</p>
    </audio>
    <section class="w-3/4 my-1/2 bg-theme-white mx-auto p-4 text-center">
      <div class="question">
        <h1 class="text-center">acceso</h1>
        <div class="m-6 text-xs">
          {{ question }}
          <input class="mt-4 text-center w-full pb-1" type="text" />
          <div class="mt-6 w-full text-right">
            <button
              @click="submit"
              disabled
              class="px-4 py-2 border bg-theme-yellow rounded-md"
            >
              acceder
            </button>
          </div>
        </div>
      </div>
      <div class="hidden feedback text-center" />
    </section>
    <aside class="hidden">
      <audio id="alarm">
        <source src="~/assets/media/audio/alarm-effect.mp3" type="audio/mpeg" />
        <p>Tu navegador no implementa el elemento audio.</p>
      </audio>
      <audio id="door">
        <source src="~/assets/media/audio/door-effect.mp3" type="audio/mpeg" />
        <p>Tu navegador no implementa el elemento audio.</p>
      </audio>
    </aside>
  </div>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      question: '',
      hint: 'descargando datos...'
    };
  },
  mounted() {
    const audio = this.$el.querySelector('audio');
    const hint = this.$el.querySelector('.hint');
    const button = this.$el.querySelector('button');
    let text = 'en qué año se inauguró el observatorio fabra de barcelona?';
    const interval = setInterval(() => {
      this.question += text.slice(0, 1);
      text = text.slice(1);

      if (text === '') {
        clearInterval(interval);
        this.hint = 'datos descargados';
        hint.classList.remove('hint');
        button.disabled = false;
      }
    }, 350);

    audio.play();
  },
  methods: {
    submit() {
      const value = this.$el.querySelector('input').value;
      const question = this.$el.querySelector('.question');
      const feedback = this.$el.querySelector('.feedback');

      question.classList.add('hidden');
      if (value === '1904') {
        const audio = this.$el.querySelector('#door');

        audio.play();
        feedback.textContent = 'cargando';
        setTimeout(() => {
          window.location.href = 'https://www.youtube.com/embed/7WlphzFbwL4';
        }, 3500);
      } else {
        const audio = this.$el.querySelector('#alarm');

        audio.play();
        feedback.classList.add('text-theme-red');
        feedback.textContent = 'error';
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
