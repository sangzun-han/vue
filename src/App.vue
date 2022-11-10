<template>
  <div id="app">
    <div class="menu">
      <a v-for="(menu, index) in menus" :key="index">{{ menu }}</a>
    </div>
    <transition name="fade">
      <ModalView
        v-bind:products="products"
        v-bind:click="click"
        v-bind:isModal="isModal"
        v-on:closeModal="isModal = false"
      />
    </transition>
    <DisCount v-if="isShowDisCount" />
    <button v-on:click="priceSort">가격순 정렬</button>
    <button v-on:click="reversePriceSort">가격역순정렬</button>
    <button v-on:click="sortBack">원래대로</button>
    <CardView
      v-for="(product, index) in products"
      v-on:openModal="
        isModal = true;
        click = $event;
      "
      v-bind:product="products[index]"
      v-bind:key="index"
    />
  </div>
</template>

<script>
import data from "./assets/data.js";
import DisCount from "./DisCount.vue";
import ModalView from "./ModalView.vue";
import CardView from "./CardView.vue";

export default {
  name: "App",
  data() {
    return {
      origin: [...data],
      click: 0,
      menus: ["Home", "Shop", "About"],
      products: data,
      isModal: false,
      isShowDisCount: true,
    };
  },
  methods: {
    priceSort() {
      this.products.sort((a, b) => {
        return a.price - b.price;
      });
    },
    reversePriceSort() {
      this.products.sort((a, b) => {
        return b.price - a.price;
      });
    },

    sortBack() {
      this.products = [...this.origin];
    },
  },

  components: {
    DisCount: DisCount,
    ModalView: ModalView,
    CardView: CardView,
  },
};
</script>

<style>
.fade-enter {
  transform: translateY(-1000px);
}

.fade-enter-active {
  transition: all 1s;
}

.fade-enter-to {
  transform: translateY(0px);
}

body {
  margin: 0;
}

div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}

.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}
</style>
