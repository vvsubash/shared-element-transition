<template>
  <TransitionGroup as="div" name="list">
    <div class="relative">
      <div class="slider-transition w-full flex gap-x-2 mx-16">
        <NuxtImg
          v-for="i in imagesInView"
          :key="i"
          class="w-1/6 border p-2"
          :src="`https://picsum.photos/id/${i}/200/300`"
          alt="sd"
        />
      </div>

      <button class="absolute bg-gray-400 p-1 top-1/2 right-4" @click="next">
        next
      </button>
      <button
        class="absolute bg-gray-400 p-1 top-1/2 right-4 -translate-y-full"
        @click="nextTG"
      >
        nextTG
      </button>
    </div>
  </TransitionGroup>
  <div>{{ imagesInView.join(",") }}</div>
  <div>{{ initialImageIndex }}</div>
</template>
<script setup lang="ts">
const images = [34, 345, 42, 32, 23, 66, 77, 96, 34, 23];
const initialImageIndex = ref(0);
const imagesInView = computed(() =>
  [...images].splice(initialImageIndex.value, 5)
);
const next = () => {
  () => setTimeout(() => {}, 500);
  document.startViewTransition(() => initialImageIndex.value++);
};

const nextTG = () => {
  initialImageIndex.value++;
};
</script>

<style>
.slider-transition {
  view-transition-name: slider;
}

@keyframes fade-in {
  from {
    opacity: 0;
  }
}

@keyframes fade-out {
  to {
    opacity: 0;
  }
}

@keyframes slide-from-right {
  from {
    transform: translateX(20%);
  }
}

@keyframes slide-to-left {
  to {
    transform: translateX(-20%);
  }
}
::view-transition-old(slider) {
  animation: 190ms ease-in-out both fade-out,
    300ms ease-in-out both slide-to-left;
}

::view-transition-new(slider) {
  animation: 310ms ease-in-out 90ms both fade-in,
    300ms ease-in-out both slide-from-right;
}

.list-move, /* apply transition to moving elements */
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(20%);
}

/* ensure leaving items are taken out of layout flow so that moving
   animations can be calculated correctly. */
.list-leave-active {
  position: absolute;
}
</style>
