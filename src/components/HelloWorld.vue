<script setup lang="ts">
import { ref } from "vue";

let isPurple = ref(false);
let selectedColor = ref("");
let size = ref(100);
let degree = ref(1);

const circle_classes = () => {
  return { purple: isPurple };
};
</script>

<template>
  <label for="color">
    <input type="checkbox" name="color" id="color" v-model="isPurple" />
    Purple
  </label>

  <select v-model="selectedColor">
    <option value="">White</option>
    <option value="text-black">Black</option>
    <option value="text-orange">Orange</option>
  </select>

  <input type="number" v-model="size" />

  <label>Degrees</label>
  <input type="range" min="1" max="360" v-model="degree" />

  <div
    class="circle"
    :class="[selectedColor, circle_classes]"
    :style="[
      {
        width: size + 'px',
        height: size + 'px',
        lineHeight: size + 'px',
      },
      { transform: 'rotate(' + degree + 'deg)' },
    ]"
  >
    Hi!
  </div>
</template>

<style scoped>
.circle {
  background-color: green;
  width: 2rem;
  height: 2rem;
  font-size: 1.5rem;
  color: white;
  padding: 2rem;
  border-radius: 50%;
  transition-duration: 0.3s;
  transition-property: background-color, color;
}

.purple {
  background-color: purple;
}
.text-black {
  color: #424242;
}
.text-orange {
  color: #ffc26f;
}
</style>
