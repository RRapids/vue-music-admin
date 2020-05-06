<template>
  <v-container>
    <h3>角色管理</h3>
    <span class="gutter">
      <mu-button color="teal">添加角色</mu-button>
      <mu-button color="success">编辑角色</mu-button>
      <mu-button color="error">删除角色</mu-button>
    </span>
  </v-container>
</template>

<script>
export default {
  name: 'Role',
  data() {
    return {
      permissions: this.$store.state.menuList[1].subMenus[0].permissions
    }
  },
  components: {},
  created() {},
  mounted() {},
  methods: {},
  computed: {}
}
</script>

<style scoped lang="scss"></style>
