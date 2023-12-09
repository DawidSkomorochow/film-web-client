<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld :msg="msg" />
    <div v-if="items.length">
      <h2>Items from Backend:</h2>
      <ul>
        <li v-for="item in items" :key="item.id">{{ item.name }}</li>
      </ul>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from "vue";
import HelloWorld from "@/components/HelloWorld.vue";
import axios from "axios";

export default defineComponent({
  components: {
    HelloWorld,
  },
  setup() {
    const msg = ref("Welcome to Your Vue.js + TypeScript App");
    const items = ref([]); // Define a reactive property for the items

    onMounted(async () => {
      try {
        const response = await axios.get("http://localhost:3000/movies"); // Replace with your backend URL
        items.value = response.data;
      } catch (error) {
        console.error("There was an error fetching the items: ", error);
      }
    });

    return {
      msg,
      items,
    };
  },
});
</script>
