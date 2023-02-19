<template>
  <form @submit.prevent="parseMessage" class="w-full max-w-lg">
    <div class="flex flex-wrap -mx-3 mb-6">
      <div class="w-full md:w-1/2 px-3 mb-6 md:mb-0">
        <label
          for="name"
          class="block uppercase tracking-wide text-white text-xs font-bold mb-2"
          >Name</label
        >
        <input
          id="name"
          v-model="name"
          placeholder="Enter name"
          required
          type="text"
          class="appearance-none block w-full bg-gray-200 text-gray-700 border border-red-500 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white"
        />
      </div>
      <div>
        <label
          for="email"
          class="block uppercase tracking-wide text-white text-xs font-bold mb-2"
          >Email</label
        >
        <input
          id="email"
          v-model="email"
          placeholder="Enter email"
          required
          type="email"
          class="appearance-none block w-full bg-gray-200 text-gray-700 border border-red-500 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white"
        />
      </div>
      <div>
        <label
          for="message"
          class="block uppercase tracking-wide text-white text-xs font-bold mb-2"
          >Message</label
        >
        <textarea
          id="message"
          v-model="message"
          placeholder="Enter message"
          required
          class="appearance-none block w-full bg-gray-200 text-gray-700 border border-red-500 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white"
        ></textarea>
      </div>
    </div>
    <button class="tbutton" type="submit">Submit</button>
  </form>
</template>

<script setup>
const name = ref("");
const email = ref("");
const message = ref("");

const parseMessage = () => {
  const newMessage = {
    name: name.value,
    email: email.value,
    message: message.value,
  };
  console.log(newMessage);
};
</script>

<style scoped></style>
