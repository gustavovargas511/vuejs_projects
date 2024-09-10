<script setup>
import { ref } from "vue";

const px_name = ref("Anna"); //v-model
const px_pn = ref("Marina"); // @input and :value

// const readPxParentName = (ev) => {
//   px_pn.value = ev.target.value;
// };
</script>

<template>
  <div class="md:w-1/2">
    <h2 class="font-black text-3xl text-center">Px Follow up</h2>
    <p class="text-lg text-center mt-5 mb-10">
      Adding and administration of Px
    </p>

    <form action="" class="bg-white shadow-md rounded-lg py-10 px-5">
      <div class="mb-5">
        {{ px_name }}
        <label for="px-name" class="block text-gray-700 uppercase font-bold"
          >Px Name:</label
        >
        <input
          id="px-name"
          type="text"
          placeholder="Px Name"
          class="border-2 w-full p-2 mt-2 rounded-md placeholder-gray-400"
          v-model="px_name"
        />
      </div>
      <div class="mb-5">
        {{ px_pn }}
        <label
          for="px-parent-name"
          class="block text-gray-700 uppercase font-bold"
          >Px Parent Name:</label
        >
        <input
          id="px-parent-name"
          type="text"
          placeholder="Px Parent Name"
          class="border-2 w-full p-2 mt-2 rounded-md placeholder-gray-400"
          :value="px_pn"
          @input="(e) => (px_pn = e.target.value)"
        />
      </div>
      <div class="mb-5">
        <label
          for="px-parent-email"
          class="block text-gray-700 uppercase font-bold"
          >Px Parent Email:</label
        >
        <input
          id="px-parent-email"
          type="email"
          placeholder="Px Parent Email"
          class="border-2 w-full p-2 mt-2 rounded-md placeholder-gray-400"
        />
      </div>
      <div class="mb-5">
        <label
          for="register-date"
          class="block text-gray-700 uppercase font-bold"
          >Date:</label
        >
        <input
          id="register-date"
          type="date"
          class="border-2 w-full p-2 mt-2 rounded-md placeholder-gray-400"
        />
      </div>
      <div class="mb-5">
        <label for="comments" class="block text-gray-700 uppercase font-bold"
          >Comments:</label
        >
        <textarea
          id="comments"
          placeholder="Important extra information"
          class="border-2 w-full p-2 mt-2 rounded-md placeholder-gray-400 h-28"
        />
      </div>
      <input
        type="submit"
        value="Add Px"
        class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors rounded-md"
      />
    </form>
  </div>
</template>
