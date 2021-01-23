<template>
  <div class="itemsCart">
    <div class="item">
      <h3>{{ item.titulo }}</h3>
      <img :src="item.img" width="150" alt="">
      <p>precio: ${{ item.precio }}</p>
      <p>peso: {{ item.peso }}gr</p>
      <p>index: {{ ind }}</p>
      <button @click="agregarCarrito(item)" class="btn btn-success">Agregar carrito</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["item", "ind"],
  methods: {
      agregarCarrito(item) {
          this.$bus.$emit("agregar-carro", item)
      }
  }
};
</script>

<style>
.itemsCart {
  padding: 0;
}

.item {
  padding: 20px;
  margin: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #fff;
}

.item p {
  margin: 0;
}
</style>