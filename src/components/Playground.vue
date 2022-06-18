<script setup lang="ts">
import { ref, computed } from "vue";

let perspective = ref(100);
let rotateX = ref(0);
let rotateY = ref(0);
let rotateZ = ref(0);

const box = computed(() => ({
  transform: `perspective(${perspective.value}px) rotateX(${rotateX.value}deg) rotateY(${rotateY.value}deg) rotateZ(${rotateZ.value}deg)`,
}));

const reset = () => {
  perspective.value = 100;
  rotateX.value = 0;
  rotateY.value = 0;
  rotateZ.value = 0;
};


const copy = () => {
  const el = document.createElement("textarea");
  el.setAttribute("readonly", "");
  el.style.position = "absolute";
  el.style.left = "-9999px";
  el.value = `transform: ${JSON.stringify(box.value.transform)}`;
  document.body.appendChild(el);
  el.select();
  document.execCommand("copy");
  document.body.removeChild(el);
};
</script>

<template>
  <div class="content">
    <h2>CSS3 Perspective Playground</h2>
    <main>
      <section class="settings">
        <div class="settings-container">
          <label>perspective: {{ perspective }}px;</label>
          <input type="range" min="0" max="999" v-model="perspective" />

          <label>rotateX: {{ rotateX }}deg; </label>
          <input type="range" min="-180" max="180" v-model="rotateX" />

          <label>rotateY: {{ rotateY }}deg; </label>
          <input type="range" min="-180" max="180" v-model="rotateY" />

          <label>rotateZ: {{ rotateZ }}deg; </label>
          <input type="range" min="-180" max="180" v-model="rotateZ" />

          <button type="button" @click.prevent="reset">Reset</button>
          <button type="button" @click.prevent="copy">Copy</button>
        </div>
      </section>
      <section class="output">
        <div class="box-container">
          <div class="box" :style="box"></div>
        </div>
      </section>
    </main>
  </div>

  <css-doodle>
    :doodle { @grid: 1x3 / 100vmax; position: absolute; top: 0; left: 0;
    z-index: 0; } @size: 100% 150%; position: absolute; background: @m(100, (
    linear-gradient(transparent, @p( #FFFDE1@repeat(2, @p([0-9a-f])),
    #FB3569@repeat(2, @p([0-9a-f])) )) @r(0%, 100%) @r(0%, 100%) / @r(1px)
    @r(23vmin) no-repeat )); will-change: transform; animation: f 50s linear
    calc(-50s / @size() * @i()) infinite; @keyframes f { from { transform:
    translateY(-100%) } to { transform: translateY(100%) } }
  </css-doodle>
</template>
