<template>
  <div class="flex justify-center items-center h-screen gap-x-16">
    <div class="relative">
      <div
        class="absolute bottom-0 pointer-events-none overflow-visible w-[300px] translate-x-[-50px] origin-bottom translate-y-6"
        v-if="showCard"
      >
        <img
          :src="`https://picsum.photos/id/${images[0]}/300/150`"
          alt="zero"
          class="image-transition"
        />
        <p class="text-transition bg-pink-300">Lorem ipsum dolor,</p>
      </div>
      <img
        :src="`https://picsum.photos/id/${images[0]}/200/100`"
        alt="zero"
        class="block"
      />
    </div>
    <button @click="toggleCard" class="border bg-pink-500 px-4 py-2">
      Toggle Card
    </button>
  </div>
</template>
<script setup lang="ts">
const images = [34, 345, 42, 32, 23, 66, 77, 96, 34, 23];
const showCard = ref(false);
const toggleCard = () => {
  document.startViewTransition(() => (showCard.value = !showCard.value));
};
</script>
<style>
@keyframes scale-in {
  from {
    scale: 66%;
  }
  to {
    scale: 100%;
  }
}
@keyframes scale-out {
  from {
    scale: 100%;
  }
  to {
    scale: 66%;
  }
}

@keyframes fade-in {
  0% {
    transform: translateY(-100%);
    opacity: 0;
  }
  100% {
    opacity: 100;
    transform: translateY(0);
  }
}

.image-transition {
  view-transition-name: image-transition;
}

.text-transition {
  view-transition-name: text-transition;
}

::view-transition-old(image-transition) {
  animation: scale-out ease-in-out both 0.3s;
  transform-origin: bottom;
}
::view-transition-new(image-transition) {
  animation: scale-in ease-in-out both 0.3s;
  transform-origin: bottom;
}

::view-transition-old(text-transition),
::view-transition-new(text-transition) {
  transform-origin: top;
}

::view-transition-old(text-transition) {
  animation: scale-out ease-in-out both 0.3s, fade-in ease-in-out 0.3s reverse;
}
::view-transition-new(text-transition) {
  animation: scale-in ease-in-out both 0.3s, fade-in ease-in-out 0.3s;
}
</style>
