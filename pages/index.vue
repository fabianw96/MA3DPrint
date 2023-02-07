<template>
  <div>
    <div class="flex items-center justify-center">
      <div class="loader justify-center" v-if="loading"></div>
    </div>
    <section class="grid grid-cols-1 md:grid-cols-3">
      <div v-for="image in images" :key="image.id">
        <img
          class="p-2 h-48 w-full object-cover scale-95 hover:scale-100 hover:cursor-pointer transition-transform duration-300 ease-in"
          :src="image.uri"
          @click="openModal(image.id)"
        />
      </div>
      <ModalComponent
        :image="currentImage"
        v-if="isModalOpen"
        @close="isModalOpen = false"
        class="transition-all duration-500 ease-in-out"
      />
    </section>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient();
const loading = ref(false);
const isModalOpen = ref(false);
const currentImage = ref(null);
const images = ref([]);

const getImages = async () => {
  loading.value = true;
  const { data, error } = await supabase.from('images').select();
  if (error) {
    console.log(error);
  } else {
    images.value = data;
    console.log(images.value);
    loading.value = false;
  }
};

const openModal = (id) => {
  isModalOpen.value = true;
  currentImage.value = images.value.find((image) => image.id === id);
  console.log(currentImage.value);
};

onMounted(() => {
  getImages();
});
</script>

<style scoped>
.loader {
  border: 0 solid transparent;
  border-radius: 50%;
  width: 100px;
  height: 100px;
  position: relative;
}

.loader::before,
.loader::after {
  content: '';
  border: 7px solid #ccc;
  border-radius: 50%;
  width: inherit;
  height: inherit;
  position: absolute;
  animation: loader 2s linear infinite;
  opacity: 0;
}

.loader::before {
  animation-delay: 1s;
}

@keyframes loader {
  0% {
    transform: scale(1);
    opacity: 0;
  }

  50% {
    opacity: 1;
  }

  100% {
    transform: scale(0);
    opacity: 0;
  }
}
</style>
