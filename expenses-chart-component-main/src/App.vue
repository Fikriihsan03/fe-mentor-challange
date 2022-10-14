<template>
  <div class="flex flex-col justify-center items-center min-h-screen">
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
  },
};
</script>

<style>
@tailwind base;
@tailwind components;
@tailwind utilities;
@import url("https://fonts.googleapis.com/css2?family=DM+Sans&display=swap");
body {
  font-family: "DM Sans", sans-serif;
  background-color: hsl(27, 66%, 92%);
}
.bg-softred {
  background-color: hsl(10, 79%, 65%);
}
</style>
