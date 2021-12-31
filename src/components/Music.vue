<template>
  <div class="absolute bottom-0 left-0 z-20 bg-black text-white flex flex-col">
    <button v-on:click="toggle" class="flex flex-row-reverse">
      <MusicNoteIcon class="h-5 w-5 text-white opacity-40 hover:opacity-100" />
    </button>
    <div :class="visible && 'hidden'">
      <label>
        Music page, like YouTube embed:
        <input
          class="bg-black"
          v-model="url"
          placeholder="Music url page here"
        />
      </label>

      <iframe
        width="560"
        height="315"
        :src="url"
        title="YouTube video player"
        frameborder="0"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
        allowfullscreen
      ></iframe>
    </div>
  </div>
</template>
<script>
import { MusicNoteIcon } from "@heroicons/vue/solid";
export default {
  data() {
    return {
      visible: false,
      url: "https://www.youtube.com/embed/5qap5aO4i9A",
    };
  },
  components: {
    MusicNoteIcon,
  },
  methods: {
    toggle() {
      this.visible = !this.visible;
    },
  },
};
</script>
