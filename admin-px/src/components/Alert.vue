<script setup>
import { computed } from "vue";

const alertProps = defineProps({
  alertmsg: {
    type: Object,
    required: true,
  },
});

const isError = computed(() => {
  return alertProps.alertmsg.msgType === "Error";
});
</script>

<template>
  <div
    :class="[isError ? 'bg-red-500' : 'bg-green-500']"
    class="text-white p-3 text-center uppercase rounded-md mb-2 font-bold"
  >
    {{ alertmsg.msgText }}
  </div>
</template>
