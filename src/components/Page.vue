<template>
  <nav class="page">
    <button class="btn" :class="{ 'js-btn': currentIndex === index ? true : false }"
      type="button" @click="changePage(index)"
      v-for="(item, index) in dataLen" :key="index">{{ index + 1 }}</button>
  </nav>
</template>

<script>
export default {
  name: 'Page',
  props: {
    dataLen: Number,
  },
  data() {
    return {
      currentIndex: 0,
    };
  },
  methods: {
    changePage(index) {
      this.currentIndex = index;
      this.$emit('changePage', index);
    },
  },
};
</script>

<style scoped>
.page {
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
  width: 7%;
  padding-left: 15px;
}

.btn {
  width: 40px;
  margin: 8px;
  font-size: 16px;
  color: #888;
  border: none;
  background-color: #fff;
  cursor: pointer;
}

.js-btn {
  font-weight: 600;
  color: #666;
  border-right: 3px solid #0077b5;
}
</style>
