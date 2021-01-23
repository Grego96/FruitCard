<template>
  <div class="catalogo">
    <div class="row no-gutters">
      <ItemCart
        class="col-md-6"
        v-for="(item, index) in items"
        :key="index"
        :item="item"
        :ind="index"
      />
    </div>
  </div>
</template>

<script>
import ItemCart from "./ItemCart";

export default {
  components: {
    ItemCart
  },
  props: ["items"]
};
</script>

<style lang="scss">

</style>