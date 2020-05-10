<template>
  <div class="bg">
    <Login />
  </div>
</template>

<script>
import Login from '../../components/Login'
export default {
  components: {
    Login
  }
}
</script>

<style lang="scss" scoped>
.bg {
  background-image: url('../../assets/images/bg.jpg');
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
