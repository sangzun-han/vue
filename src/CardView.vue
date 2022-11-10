<template>
  <div>
    <img v-bind:src="product.image" alt="image" class="room-img" />
    <h4 v-on:click="$emit('openModal', product.id)">{{ product.title }}</h4>
    <p>{{ product.price }}원</p>
    <p>{{ product.content }}</p>
  </div>
</template>

<script>
export default {
  name: "CardView",
  props: {
    product: Object,
  },
};
</script>

<style></style>
