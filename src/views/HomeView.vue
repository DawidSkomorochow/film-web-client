<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld :msg="msg" />
    <div v-if="items.length">
      <h2>Items from Backend:</h2>
      <ul>
        <li v-for="(item, index) in items" :key="index">
          {{ item.title }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted, toRaw } from "vue";
import HelloWorld from "@/components/HelloWorld.vue";
import axios from "axios";

interface Item {
  title: string;

  // other properties if needed
}

export default defineComponent({
  components: {
    HelloWorld,
  },
  setup() {
    const msg = ref("Welcome to Your Vue.js + TypeScript App");
    const items = ref<Item[]>([]); // Define a reactive property for the items

    onMounted(async () => {
      try {
        const response = await axios.get("http://localhost:3000/movies");
        items.value = response.data.results;

        console.log("response: ", response);
        console.log("Items:", toRaw(items.value)); // Logging the items after fetching
      } catch (error) {
        console.error("There was an error fetching the items: ", error);
      }
    });

    // console.log("items: ", items);

    return {
      msg,
      items,
    };
  },
});
</script>
