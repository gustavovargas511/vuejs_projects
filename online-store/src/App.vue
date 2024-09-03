<script setup>
import { ref, reactive, onMounted } from "vue";
import { db } from "./data/items";
import Item from "./components/Item.vue";
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";

const items = ref([]);

const cart = ref([]);

const headerItem = ref({});

onMounted(() => {
  items.value = db;
  headerItem.value = db[3];
});

/**   FUNCTIONS */

const addToCart = (item) => {
  const alreadyAdded = cart.value.findIndex(
    (product) => product.id === item.id
  );
  // console.log(alreadyAdded)
  if (alreadyAdded >= 0) {
    cart.value[alreadyAdded].qty++;
    // console.table(cart.value);
  } else {
    item.qty = 1;
    cart.value.push(item);
    // console.table(cart.value);
  }
};

const decreaseQty = (id) => {
  // console.log('Minus one', id)
  const index = cart.value.findIndex((product) => product.id === id);
  if (cart.value[index].qty <= 1) return;
  cart.value[index].qty--;
};

const increaseQty = (id) => {
  // console.log('Plus one', id)
  const index = cart.value.findIndex((product) => product.id === id);
  cart.value[index].qty++;
};

const deleteItem = (id) => {
  //alternative method
  // const index = cart.value.findIndex((product) => product.id === id);
  // cart.value.splice(index, 1);

  cart.value = cart.value.filter(item => item.id !== id)

};

const emptyCart = () => {
  cart.value.length = 0;
}

/**END FUNCTIONS */
</script>

<template>
  <Header
    :cart="cart"
    :headerItem="headerItem"
    @c-add-to-cart="addToCart"
    @c-decrease-qty="decreaseQty"
    @c-increase-qty="increaseQty"
    @c-delete-item="deleteItem"
    @c-empty-cart="emptyCart"
  />

  <main class="container-xl mt-5">
    <h2 class="text-center">Nuestra Colección</h2>

    <div class="row mt-5">
      <Item
        v-for="item in items"
        v-bind:item="item"
        @c-add-to-cart="addToCart"
      />
    </div>
  </main>

  <Footer />
</template>
