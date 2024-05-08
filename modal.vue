<template>
  <transition name="fade">
    <div v-if="isOpen">
      <div
        class="fixed bottom-0 left-0 right-0 top-0 z-50 mx-auto bg-color-lufthansa-1-60 lg:max-h-[800px] lg:min-h-[800px] lg:max-w-[430px]"
      />

      <div
        ref="containerRef"
        class="fixed left-1/2 top-1/2 z-50 w-[calc(100%-40px)] max-w-[390px] -translate-x-1/2 -translate-y-1/2 rounded-xl bg-neutral-2 p-6 shadow-40 lg:top-[400px]"
      >
        <div class="flex w-full justify-between gap-6">
          <div class="font-lufthansa-2 text-color-lufthansa-1">
            <slot name="title" />
          </div>

          <button
            type="button"
            class="h-11 w-11 rounded-md border-[0.5px] border-neutral-1-12 bg-neutral-2-60 p-[10px]"
            @click="close"
          >
            <close-icon class="h-6 w-6 text-color-lufthansa-1" />
          </button>
        </div>
        <slot name="content" />
      </div>
    </div>
  </transition>
</template>

<script lang="ts" setup>
import {
  ref,
} from 'vue';
import {
  onClickOutside,
} from '@vueuse/core';
import CloseIcon from '@/assets/icons/close.svg?component';

interface IProps {
  isOpen: boolean;
}

const props = defineProps<IProps>();

// eslint-disable-next-line no-spaced-func, func-call-spacing
const emit = defineEmits<{
  (event: 'close'): void;
}>();

const containerRef = ref<HTMLElement | null>(null);
const pageShell = document.getElementById('page-shell');

const close = () => {
  emit('close');
  pageShell?.classList.remove('no-scroll');
};

onClickOutside(containerRef, () => {
  close();
});

if (props.isOpen) {
  pageShell?.classList.add('no-scroll');
}
</script>

<style lang="css" scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease-in-out;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
