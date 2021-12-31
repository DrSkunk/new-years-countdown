<template>
  <div
    class="
      relative
      w-screen
      h-screen
      flex
      justify-center
      items-center
      bg-skyline bg-cover bg-black bg-center
      text-white text-center
    "
  >
    <h1 class="text-9xl drop-shadow z-10" v-if="isNewYear">
      Gelukkig Nieuwjaar!
    </h1>
    <h1 class="text-9xl drop-shadow z-10 tabular-nums" v-else>
      {{ remaining }}
    </h1>
    <img
      src="/img/nerdland.png"
      class="absolute left-5 top-5 w-12 opacity-50"
    />

    <Music />
  </div>
  <Fireworks v-if="isNewYear" />
</template>
<!-- BG source https://unsplash.com/photos/AEKdzZn_bBI -->
<script>
import { add, intervalToDuration } from "date-fns";
import Fireworks from "./components/Fireworks.vue";
import Music from "./components/Music.vue";

const endTime = add(new Date("2022-01-01"), {
  minutes: new Date().getTimezoneOffset(),
});

function zeroPad(input) {
  return input < 10 ? `0${input}` : input;
}

export default {
  components: {
    Fireworks,
    Music,
  },
  setup() {},
  data() {
    return {
      remaining: "Gezellig hoor",
      isNewYear: false,
    };
  },
  methods: {
    timer: function () {
      setInterval(() => {
        const { hours, minutes, seconds } = intervalToDuration({
          start: new Date(),
          end: endTime,
        });
        if (endTime - new Date() < 0) {
          this.isNewYear = true;
        } else {
          this.remaining = `${zeroPad(hours)}:${zeroPad(minutes)}:${zeroPad(
            seconds
          )}`;
        }
      }, 1000);
    },
  },
  beforeMount() {
    this.timer();
  },
};
</script>
