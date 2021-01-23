<template>
  <div class="carrot">
    <div class="carro">
      <div v-for="(item, index) in itemsCart" :key="index" class="itemCarro">
        <h4>{{ item.titulo }} x {{ item.count }}</h4>
        <p>sub total: ${{ item.count*item.precio }}</p>
        <button @click="restar(index, item)" class="btn btn-info resta">-</button>
        <button @click="sumar(item)" class="btn btn-info resta">+</button>
        <br />
        <button @click="eliminarCarro(index, item)" class="btn btn-danger">eliminar</button>
      </div>
      <div class="total">
        <h2>Total: ${{ pTotal }}</h2>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["itemsCart", "pTotal"],
  data() {
    return {
      total: Number
    };
  },
  methods: {
    eliminarCarro(index, item) {
      this.$emit("eliminar-carro", index, item);
    },
    restar(index, item) {
      this.$emit("restar", index, item);
    },
    sumar(item) {
      this.$emit("sumar", item);
    }
  }
};
</script>

<style>
.carrot {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.carro {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}
.itemCarro {
  padding: 10px;
    border: 1px solid green;
    border-radius: 5px;
    margin: 10px;
    width: 80%;
}

.resta {
  padding: 5px;
  margin: 5px;
  border-radius: 3px;
  margin-bottom: 2px;
}
</style>