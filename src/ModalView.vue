<template>
  <div class="black-bg" v-if="isModal">
    <div class="white-bg">
      <img v-bind:src="products[click].image" alt="image" />
      <h4>{{ products[click].title }}</h4>
      <p>{{ month }}개월 선택함 : {{ products[click].price * month }}</p>
      <p>{{ products[click].content }}</p>
      <input v-model="month" />
      <button v-on:click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ModalView",
  data() {
    return {
      month: 1,
    };
  },
  beforeUpdate() {
    if (this.month == 2) {
      alert("2개월은 좀 .. 3개월부터해봐");
      this.month = 3;
    }
  },
  watch: {
    month(data) {
      // 사용자가 month를 문자로 입력하면 경고문 띄워주셈
      if (isNaN(data) == true || data > 12) {
        alert("입력 똑바로");
        this.month = 1;
      }
    },
  },
  props: {
    products: Array,
    click: Number,
    isModal: Boolean,
  },
};
</script>

<style></style>
