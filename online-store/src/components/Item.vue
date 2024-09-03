<script setup>

const props = defineProps({
  item: {
    type: Object,
    required: true,
  },
});

defineEmits(["c-add-to-cart"]);

// const incrementar = () => {
//   numero.value++;
// };
</script>

<template>
  <div class="col-md-6 col-lg-4 my-4 row align-items-center">
    <div class="col-4">
      <img
        class="img-fluid"
        v-bind:src="'/img/' + item.imagen + '.jpg'"
        alt="imagen item"
      />
    </div>
    <div class="col-8">
      <h3 class="text-black fs-4 fw-bold text-uppercase">{{ item.nombre }}</h3>
      <p>
        {{ item.descripcion }}
      </p>
      <p class="fw-black text-primary fs-3">${{ item.precio }}</p>
      <button
        type="button"
        class="btn btn-dark w-100"
        v-on:click="$emit('c-add-to-cart', item)"
      >
        Agregar al Carrito
      </button>
    </div>
  </div>
  <!-- FIN item -->
</template>
