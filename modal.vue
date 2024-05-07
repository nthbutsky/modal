<template>
  <teleport to="#teleport-content">
    <div
      v-bind="$attrs"
      class="fixed top-0 left-0 right-0 bottom-0 z-50 flex flex-col justify-center items-center overflow-y-auto backdrop-blur-sm"
    />

    <div
      ref="containerRef"
      class="rounded-[20px] bg-neutral-100 fixed top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 z-50 min-w-full sm:min-w-[532px]"
    >
      <div class="pt-4 px-4 pb-2 w-full flex justify-end">
        <button-icon
          :icon="ClearIcon"
          class="text-neutral-900-48 ml-auto"
          @click="close"
        />
      </div>
      <slot />
    </div>
  </teleport>
</template>

<script lang="ts" setup>
import {
  ref,
} from 'vue';
import {
  onClickOutside, onKeyStroke,
} from '@vueuse/core';
import ButtonIcon from '@/components/button-icon/button-icon.vue';
import ClearIcon from '@/assets/icons/clear.svg?component';

// eslint-disable-next-line no-spaced-func, func-call-spacing
const emit = defineEmits<{
  (event: 'close'): void;
}>();

const containerRef = ref(null);

function close() {
  emit('close');
}

onClickOutside(containerRef, () => {
  close();
});

onKeyStroke('Escape', () => {
  close();
});
</script>
