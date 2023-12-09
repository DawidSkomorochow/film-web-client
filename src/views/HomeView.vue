<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue"; // Import necessary functions
import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src

export default defineComponent({
  components: {
    HelloWorld,
  },
  setup() {
    const msg = ref("Welcome to Your Vue.js + TypeScript App");

    return {
      msg,
    };
  },
});
</script>
