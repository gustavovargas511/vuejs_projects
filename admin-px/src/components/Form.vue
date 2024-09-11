<script setup>
import { ref, reactive } from "vue";
import Alert from "./Alert.vue";

// const px_name = ref("");

/** Vars */

const alert_mgs = reactive({
  msgType: "",
  msgText: "",
});

const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  parentName: {
    type: String,
    required: true,
  },
  parentEmail: {
    type: String,
    required: true,
  },
  date: {
    type: String,
    required: true,
  },
  comments: {
    type: String,
    required: true,
  },
});

const emits = defineEmits([
  "update:name",
  "update:parent-name",
  "update:parent-email",
  "update:date",
  "update:comments",
  "c-save-px",
]);
/**END Vars */

/** Functions */
const validateForm = () => {
  // if ([px_data.name, px_data.parentEmail].includes("")) {
  //   console.log("Empty fields...");
  // }
  // console.log(px_data)

  /**Above code its same as: */
  if (Object.values(props).includes("")) {
    // console.log("Please fill in all fields");
    alert_mgs.msgText = "All fields are mandatory";
    alert_mgs.msgType = "Error";
    return;
  }

  console.log("Adding...");

  emits("c-save-px", 123);
};
/** END Functions */
</script>

<template>
  <div class="md:w-1/2">
    <h2 class="font-black text-3xl text-center">Px Follow up</h2>
    <p class="text-lg text-center mt-5 mb-10">
      Adding and administration of Px
    </p>
    <Alert v-if="alert_mgs.msgText" :alertmsg="alert_mgs" />
    <form
      class="bg-white shadow-md rounded-lg py-10 px-5"
      v-on:submit.prevent="validateForm"
    >
      <div class="mb-5">
        <label for="px-name" class="block text-gray-700 uppercase font-bold"
          >Px Name:</label
        >
        <input
          id="px-name"
          type="text"
          placeholder="Px Name"
          class="border-2 w-full p-2 mt-2 rounded-md placeholder-gray-400"
          @input="emits('update:name', $event.target.value)"
        />
        <!--Var emits-->
      </div>
      <div class="mb-5">
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
          @input="$emit('update:parent-name', $event.target.value)"
        />
        <!--Linear $emit-->
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
          @input="$emit('update:parent-email', $event.target.value)"
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
          @input="$emit('update:date', $event.target.value)"
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
          @input="$emit('update:comments', $event.target.value)"
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
