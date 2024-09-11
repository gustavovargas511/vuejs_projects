<script setup>
import { ref, reactive } from "vue";
import Header from "./components/Header.vue";
import Form from "./components/Form.vue";

const px_data = reactive({
  name: "",
  parentName: "",
  parentEmail: "",
  date: "",
  comments: "",
});

const px_list = ref([]);

const savePx = () => {
  px_list.value.push(px_data);
  // px_list.value.forEach((px) => console.table(px));
};

// const savePx = (num) => {
//   console.log("Saved!", num);
// };
</script>

<template>
  <div class="container mx-auto mt-10">
    <Header />
    <div class="mt-12 md:flex">
      <!--v-bind + v-on === v-model -->
      <Form
        v-bind:name="px_data.name"
        v-on:update:name="(newName) => (px_data.name = newName)"
        v-model:parentName="px_data.parentName"
        v-model:parentEmail="px_data.parentEmail"
        v-model:date="px_data.date"
        v-model:comments="px_data.comments"
        @c-save-px="savePx"
      />
      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Px Control</h3>

        <div v-if="px_list.length > 0">
          <div v-for="px in px_list">
            <p>{{ px.name }}</p>
          </div>
        </div>
        <p v-else class="mt-10 text-2xl text-center">No Px to edit</p>
      </div>
    </div>
  </div>
</template>
