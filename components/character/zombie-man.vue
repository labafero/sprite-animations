<script setup>
const charClasses = ref([
  {
    name: "idle",
    size: "-768px",
    animationIterationCount: "infinite",
    steps: 8,
    img: "/img/zombie-man/Idle.png",
  },
  {
    name: "walk",
    size: "-768px",
    animationIterationCount: "infinite",
    steps: 8,
    img: "/img/zombie-man/Walk.png",
  },
  {
    name: "attack-1",
    size: "-480px",
    animationIterationCount: "1",
    steps: 5,
    img: "/img/zombie-man/Attack_1.png",
  },
  {
    name: "attack-2",
    size: "-384px",
    animationIterationCount: "1",
    steps: 4,
    img: "/img/zombie-man/Attack_2.png",
  },
  {
    name: "hurt",
    size: "-288px",
    animationIterationCount: "1",
    steps: 3,
    img: "/img/zombie-man/Hurt.png",
  },
  {
    name: "bite",
    size: "-1056px",
    animationIterationCount: "1",
    steps: 11,
    img: "/img/zombie-man/Bite.png",
  },
  {
    name: "dead",
    size: "-480px",
    animationIterationCount: "1",
    steps: 5,
    img: "/img/zombie-man/Dead.png",
  },
]);
const state = reactive({
  currentCharClass: { class: "", size: "", steps: 0, img: "" },
});

function setCurrentCharClass(c) {
  state.currentCharClass = c;
  for (const animation of document.getAnimations()) {
    animation.cancel()
    animation.play()
  }
}
</script>

<template>
  <div class="flex space-x-4">
    <button
      v-for="charClass in charClasses"
      type="button"
      class="text-sm px-5 py-2 border border-gray-300 rounded-lg active:ring-1"
      @click="setCurrentCharClass(charClass)"
    >
      {{ charClass.name }}
    </button>
  </div>
  <div
    class="w-[96px] h-[100px] bg-no-repeat scale-150 pointer-events-none"
    :style="{
      animationName: 'sprite',
      animationDuration: '2s',
      animationIterationCount: state.currentCharClass.animationIterationCount,
      animationPlayState: 'play',
      animationTimingFunction: `steps(${state.currentCharClass.steps})`,
      backgroundImage: `url(${state.currentCharClass.img})`,
    }"
  ></div>
</template>

<style>
@keyframes sprite {
  from {
    background-position: 0 0;
  }
  to {
    background-position: v-bind("state.currentCharClass.size") 0;
  }
}
</style>
