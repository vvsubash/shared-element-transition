<template>
  <div class="relative">
    <div class="flex justify-between h-40" ref="container">
      <div
        class="top-10 left-10 size-10 border border-orange-700"
        ref="avatar"
      ></div>
      <div
        class="top-[200px] left-[300px] size-10 border border-green-700 self-end hover:transalte-y-1"
        ref="message"
      >
        hello
      </div>
    </div>
    <svg
      :width="width"
      :height="height"
      class="absolute top-0 left-0 border border-orange-600"
    >
      <g>
        <path
          :d="`M ${avatarBottomX} ${avatarBottomY} V ${messageLeftY} H ${messageLeftX}`"
          fill="transparent"
          stroke="black"
        />
      </g>
    </svg>
  </div>
</template>
<script setup lang="ts">
import { useWindowSize } from "@vueuse/core";
const container = ref<null | HTMLDivElement>(null);
const avatar = ref<null | HTMLDivElement>(null);
const message = ref<null | HTMLDivElement>(null);
const width = ref(0);
const height = ref(0);
const avatarBottomX = ref(0);
const avatarBottomY = ref(0);
const messageLeftX = ref(0);
const messageLeftY = ref(0);
const { width: vw, height: vh } = useWindowSize();

watch([container, vw], () => {
  let d = container.value?.getBoundingClientRect();
  width.value = d?.width ?? 0;
  height.value = d?.height ?? 0;

  let avatarBounding = avatar?.value?.getBoundingClientRect();
  avatarBottomX.value =
    (avatarBounding?.x ?? 0) + (avatarBounding?.width ?? 0) / 2;
  avatarBottomY.value =
    (avatarBounding?.bottom ?? 0) - (avatarBounding?.top ?? 0);
  let messageBounding = message.value?.getBoundingClientRect();
  console.log(messageBounding);
  messageLeftX.value = messageBounding?.left ?? 0;
  messageLeftY.value = messageBounding?.top ?? 0;
});
</script>
