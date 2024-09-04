<script setup>
import { computed } from 'vue';

const cartProps = defineProps({
  cart: {
    type: Array,
    required: true,
  },
  headerItem: {
    type: Object,
    required: true,
  },
});

/**    Functions */
/*************** */
const total = computed(()=>{
    return cartProps.cart.reduce((acc, item) =>  acc + (item.qty * item.precio), 0 )
})


/*************** */
/**END Functions */

defineEmits([ "c-add-to-cart", "c-increase-qty", "c-decrease-qty", "c-delete-item", "c-empty-cart"]);
</script>

<template>
  <header class="py-5 header">
    <div class="container-xl">
      <div class="row justify-content-center justify-content-md-between">
        <div class="col-8 col-md-3">
          <a href="index.html">
            <img class="img-fluid" src="../../img/logo.svg" alt="imagen logo" />
          </a>
        </div>
        <nav
          class="col-md-6 a mt-5 d-flex align-items-start justify-content-end"
        >
          <div class="carrito">
            <img
              class="img-fluid"
              src="../../img/carrito.png"
              alt="imagen carrito"
            />

            <div id="carrito" class="bg-white p-3">
              <p class="text-center" v-if="cart.length === 0">
                El carrito esta vacio
              </p>
              <div v-else>
                <table class="w-100 table">
                  <thead>
                    <tr>
                      <th>Imagen</th>
                      <th>Nombre</th>
                      <th>Precio</th>
                      <th>Cantidad</th>
                      <th></th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="item in cart">
                      <td>
                        <img
                          class="img-fluid"
                          :src="'/img/' + item.imagen + '.jpg'"
                          alt="imagen item"
                        />
                      </td>
                      <td>{{ item.nombre }}</td>
                      <td class="fw-bold">${{ item.precio }}</td>
                      <td class="flex align-items-start gap-4">
                        <button
                          type="button"
                          class="btn btn-dark"
                          @click="$emit('c-decrease-qty', item.id)"
                        >
                          -
                        </button>
                        {{ item.qty }}
                        <button
                          type="button"
                          class="btn btn-dark"
                          @click="$emit('c-increase-qty', item.id)"
                        >
                          +
                        </button>
                      </td>
                      <td>
                        <button class="btn btn-danger" 
                                type="button"
                                v-on:click="$emit('c-delete-item', item.id)" >X</button>
                      </td>
                    </tr>
                  </tbody>
                </table>
                <p class="text-end">
                  Total pagar: <span class="fw-bold">${{ total }}</span>
                </p>
                <button class="btn btn-dark w-100 mt-3 p-2"
                        @click="$emit('c-empty-cart')">
                  Vaciar Carrito
                </button>
              </div>
            </div>
          </div>
        </nav>
      </div>
      <!--.row-->

      <div class="row mt-5">
        <div class="col-md-6 text-center text-md-start pt-5">
          <h1 class="display-2 fw-bold">Model {{ headerItem.nombre }}</h1>
          <p class="mt-5 fs-5 text-white">
            {{ headerItem.descripcion}}
          </p>
          <p class="text-primary fs-1 fw-black">${{headerItem.precio}}</p>
          <button
            type="button"
            class="btn fs-4 bg-primary text-white py-2 px-5"
            v-on:click="$emit('c-add-to-cart', headerItem)"
          >
            Agregar al Carrito
          </button>
        </div>
      </div>
    </div>

    <img
      class="header-item"
      src="../../img/header_item.png"
      alt="imagen header"
    />
  </header>
</template>
