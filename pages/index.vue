<template>
  <div>
    <!-- Loader, only shown when getting data from the DB -->
    <section class="flex items-center justify-center">
      <div class="loader justify-center" v-if="loading"></div>
    </section>
    <!-- display image gallery with Click event handler to open modal -->
    <section class="grid grid-cols-1 md:grid-cols-5">
      <div v-for="image in images" :key="image.id">
        <img
          class="rounded-xl p-2 h-48 w-full object-cover scale-95 hover:scale-100 hover:cursor-pointer transition-transform duration-300 ease-in "
          :alt="image.id"
          :src="image.uri"
          @click="openModal(image.id)"
        />
      </div>
      <!-- Custom ModalComponent that displays the clicked image -->
      <ModalComponent
        :image="currentImage"
        v-if="isModalOpen"
        @close="isModalOpen = false"
        @prev="openModal(currentImage.id - 1)"
        @next="openModal(currentImage.id + 1)"
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
const lastImage = ref(null);
const images = ref([]);

// Get all images from the supabase DB
const getImages = async () => {
  loading.value = true;
  const { data, error } = await supabase.from('images').select();
  if (error) {
    console.log(error);
  } else {
    images.value = data;
    //console.log(images.value);
    loading.value = false;
  }
};

// Open modal and set currentImage to the clicked image
// If the clicked image is the first or last image, set currentImage to the first or last image
const openModal = (id) => {
  isModalOpen.value = true;

  if (currentImage.value != null) {
    lastImage.value = currentImage.value;
  }
  currentImage.value = images.value.find((image) => image.id === id);


  if (
    currentImage.value === undefined &&
    lastImage.value.id === 1
  ) {
    currentImage.value = images.value[images.value.length - 1];
  } else if (
      currentImage.value === undefined &&
      lastImage.value.id !== 1
  ) {
    currentImage.value = images.value[0];
  }
};

// Get images on page load
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
