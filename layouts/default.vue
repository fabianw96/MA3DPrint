<template>
  <div>
    <section class="flex gap-x-4 justify-around m-4">
      <NuxtLink class="btn" to="/">Home</NuxtLink>
      <NuxtLink class="btn" to="/contact">Kontakt</NuxtLink>

    </section>

    <slot />

    <section>
      <footer
        class="fixed bottom-0 left-0 z-20 w-full p-4 bg-white border-t border-gray-200 shadow md:flex md:items-center md:justify-between md:p-6 dark:bg-gray-800 dark:border-gray-600"
      >
        <span class="text-sm text-gray-500 sm:text-center dark:text-gray-400"
          >© 2023 MA. All Rights Reserved.
        </span>
        <ul
          class="flex flex-wrap items-center mt-3 text-sm text-gray-500 dark:text-gray-400 sm:mt-0"
        >
          <li>
            <NuxtLink to="/impressum" class="mr-4 hover:underline md:mr-6"
              >Impressum</NuxtLink
            >
          </li>
<!--          <li>-->
<!--            <NuxtLink to="/datenschutz" class="mr-4 hover:underline md:mr-6"-->
<!--              >Datenschutz</NuxtLink-->
<!--            >-->
<!--          </li>-->
        </ul>
      </footer>
    </section>
  </div>
</template>

<script setup></script>

<style scoped>
.btn {
  position: relative;
  font-size: 14px;
  text-transform: uppercase;
  text-decoration: none;
  padding: 1em 1em;
  display: inline-block;
  border-radius: 6px;
  transition: all 0.2s;
  border: none;
  font-family: inherit;
  font-weight: 500;
  color: black;
  background-color: white;
}

.btn:hover {
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
}

.btn:active {
  transform: translateY(-1px);
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}

.btn::after {
  content: '';
  display: inline-block;
  height: 100%;
  width: 100%;
  border-radius: 6px;
  position: absolute;
  top: 0;
  left: 0;
  z-index: -1;
  transition: all 0.4s;
}

.btn::after {
  background-color: #fff;
}

.btn:hover::after {
  transform: scaleX(1.4) scaleY(1.6);
  opacity: 0;
}
</style>
