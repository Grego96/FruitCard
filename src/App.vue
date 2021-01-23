<template>
  <div id="app">
    <div class="row no-gutters">
      <div class="col-md-9 col">
        <Catalogo :items="items" />
      </div>
      <div class="col-md-3 col">
        <Carrito
        :pTotal="pTotal"
          :itemsCart="itemsCarrito"
          v-on:eliminar-carro="eliminarCarro"
          v-on:restar="restar"
          v-on:sumar="sumar"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Catalogo from "./components/Catalogo.vue";
import Carrito from "./components/Carrito.vue";
import ManzanaImg from "../public/img/manzana.jpeg";
import BananaImg from "../public/img/banana.jpg";
import PeraImg from "../public/img/pera.jpeg";
import KiwiImg from "../public/img/kiwi.jpeg";
import FrutillaImg from "../public/img/frutilla.jpeg";
import MelonImg from "../public/img/melon.jpeg";

export default {
  components: {
    Catalogo,
    Carrito
  },
  data() {
    return {
      pTotal: 0,
      items: [
        {
          titulo: "Manzana",
          img: ManzanaImg,
          peso: 150,
          precio: 15,
          count: 0,
          subTotal: 0
        },
        {
          titulo: "Banana",
          img: BananaImg,
          peso: 200,
          precio: 15,
          count: 0,
          subTotal: 0
        },
        {
          titulo: "Pera",
          img: PeraImg,
          peso: 250,
          precio: 20,
          count: 0,
          subTotal: 0
        },
        {
          titulo: "Kiwi",
          img: KiwiImg,
          peso: 100,
          precio: 45,
          count: 0,
          subTotal: 0
        },
        {
          titulo: "Frutilla",
          img: FrutillaImg,
          peso: 50,
          precio: 30,
          count: 0,
          subTotal: 0
        },
        {
          titulo: "Melon",
          img: MelonImg,
          peso: 300,
          precio: 70,
          count: 0,
          subTotal: 0
        }
      ],
      itemsCarrito: []
    };
  },
  methods: {
    agregarCarro(item) {
      if (item.count <= 0) {
        this.itemsCarrito.push(item);
        item.count = item.count + 1;
      } else {
        item.count = item.count + 1;
      }
      item.subTotal = item.count * item.precio;
      // console.log(item.subTotal);
    },
    eliminarCarro(index, item) {
      this.itemsCarrito.splice(index, 1);
      item.count = 0;
      this.subTotal()
    },
    restar(index, item) {
      if (item.count > 1) {
        item.count = item.count - 1;
      } else {
        this.itemsCarrito.splice(index, 1);
        item.count = 0;
      }
      item.subTotal = item.count * item.precio;
      this.subTotal()
    },
    sumar(item) {
      if (item.count >= 1) {
        item.count = item.count + 1;
      }
      item.subTotal = item.count * item.precio;
      this.subTotal()
    },
    subTotal() {
      let total = 0;
      for (let i = 0; i < this.itemsCarrito.length; i++) {
        total = total + this.itemsCarrito[i].subTotal;
      // console.log(this.itemsCarrito[i].subTotal);
      }
      this.pTotal = total
      // console.log("000000");
      // console.log(this.pTotal);
    }
  },
  created() {
    this.$bus.$on("agregar-carro", item => {
      this.agregarCarro(item);
      this.subTotal();
    });
    // this.$bus.$on('agregar-carro', (item) => {
    //   this.agregarCarro(item)
    // })
  }
};
</script>

<style lang="scss" scoped>
// #app {
//   font-family: Avenir, Helvetica, Arial, sans-serif;
//   -webkit-font-smoothing: antialiased;
//   -moz-osx-font-smoothing: grayscale;
//   text-align: center;
//   color: #2c3e50;
// }

// #nav {
//   padding: 30px;

//   a {
//     font-weight: bold;
//     color: #2c3e50;

//     &.router-link-exact-active {
//       color: #42b983;
//     }
//   }
// }

#app {
  border: 1px solid pink;
  background-color: rgb(240, 252, 240);
}
.col {
  border: 1px solid green;
}
</style>
