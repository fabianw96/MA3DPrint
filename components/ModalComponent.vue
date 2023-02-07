<template>
  <Transition name="modal">
    <div
      class="fixed z-auto top-0 left-0 w-full h-full bg-black/50 flex transition-opacity 0.3s ease-in"
      @click="$emit('close')"
    >
      <div
        class="md:w-3/6 m-auto bg-slate-800 p-5 shadow-md transition-all 0.3s ease-in"
      >
        <div class="mt-0 text-green-500">
          <slot name="header">{{ image.id }}</slot>
        </div>

        <div class="my-5">
          <slot name="body">
            <img :src="image.uri" alt="" />
          </slot>
        </div>

        <div>
          <slot name="footer">
            <p></p>
            <button
              class="float-right tbutton hover:bg-slate-400 hover:text-black transition 0.3s ease-in-out"
              @click.prevent="$emit('close')"
            >
              OK
            </button>
          </slot>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script setup>
const { image } = defineProps(['image']);
</script>

<style scoped>
.modal-enter-active,
.modal-leave-active {
  transition: all 4.3s;
}

.modal-enter,
.modal-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>
