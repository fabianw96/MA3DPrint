<template>
  <div
    class="fixed z-auto top-0 left-0 w-full h-full bg-black/50 flex transition-opacity 0.3s ease-in"
  >
    <div
      class="md:w-3/6 m-auto bg-slate-800 p-5 shadow-md transition-all 0.3s ease-in overflow-hidden"
    >
      <div class="my-5">
        <div>
          <NuxtLink :to="image.uri" target="_blank">
            <img
              :src="image.uri"
              alt=""
              class="cursor-pointer object-cover w-full h-96"
            />
          </NuxtLink>
        </div>
      </div>

      <div>
        <div class="flex justify-around">
          <!-- Forward and Backwards button, selects next or previous image -->
          <button class="float-left tbutton" @click="$emit('prev')">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <polyline points="17 18 11 12 17 6"></polyline>
              <path d="M7 6v12"></path>
            </svg>
          </button>
          <button class="tbutton" @click.prevent="$emit('close')">Close</button>
          <button class="tbutton" @click="$emit('next')">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <polyline points="7 18 13 12 7 6"></polyline>
              <path d="M17 6v12"></path>
            </svg>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const { image } = defineProps(["image"]);
</script>

<style scoped></style>
