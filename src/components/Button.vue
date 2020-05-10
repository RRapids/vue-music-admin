<template>
  <button class="my-btn" @click="handleClick($event)">
    <slot></slot>
  </button>
</template>

<script>
export default {
  props: {
    type: {
      type: String,
      default: ''
    }
  },
  methods: {
    handleClick(event) {
      alert('UnFollow')
      this.$emit('cancel-click', event)
    }
  }
}
</script>

<style lang="scss" scoped>
.my-btn {
  background-color: #fff;
  border-radius: 3px;
  cursor: pointer;
  border: 1px solid #ccc;
  outline: none;
  color: #000;
  width: 80px;
  height: 20px;
  // padding: 5px;
}
</style>
