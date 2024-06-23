<template>
  <div
    class="flex justify-center relative items-center h-screen"

  >
    <div class="relative max-w-[200px] group transition-all duration-1000">
      <div class="absolute top-0 hidden group-hover:block scale-150 transition-all duration-1000">
        <img
          :src="`https://picsum.photos/id/${images[1]}/200/100`"
          alt="zero"
          class="block"
        />
        <p>
          Lorem ipsum dolor, sit amet consectetur adipisicing elit. Distinctio
          cupiditate necessitatibus
        </p>
      </div>
      <img
        :src="`https://picsum.photos/id/${images[0]}/200/100`"
        alt="zero"
        class="block"
      />
    </div>
  </div>
</template>
<script setup lang="ts">
    const images = [34, 345, 42, 32, 23, 66, 77, 96, 34, 23];
    const showCard = ref(false)

</script>
<style>
:view

</style>
