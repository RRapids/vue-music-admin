<template>
  <v-container>
    <v-card>
      <v-toolbar color="cyan" dark flat>
        <v-app-bar-nav-icon></v-app-bar-nav-icon>

        <v-toolbar-title>Role Management</v-toolbar-title>

        <v-spacer></v-spacer>

        <v-btn icon>
          <v-icon>mdi-magnify</v-icon>
        </v-btn>

        <v-btn icon>
          <v-icon>mdi-dots-vertical</v-icon>
        </v-btn>

        <template v-slot:extension>
          <v-tabs v-model="model" centered slider-color="yellow">
            <!-- <v-tab v-for="i in 3" :key="i" :href="`#tab-${i}`"> Item {{ i }} </v-tab>
             -->
            <v-tab>Admin</v-tab>
            <v-tab>Editor</v-tab>
            <v-tab>Other</v-tab>
          </v-tabs>
        </template>
      </v-toolbar>

      <v-tabs-items v-model="model">
        <v-tab-item>
          <v-card flat>
            <v-card-text v-text="admin"> </v-card-text>
          </v-card>
        </v-tab-item>
        <v-tab-item>
          <v-card flat>
            <v-card-text v-text="editor"> </v-card-text>
          </v-card>
        </v-tab-item>
        <v-tab-item>
          <v-card flat>
            <v-card-text v-text="other"> </v-card-text>
          </v-card>
        </v-tab-item>
      </v-tabs-items>
    </v-card>
  </v-container>
</template>

<script>
export default {
  name: 'Role',
  data() {
    return {
      // permissions: this.$store.state.menuList[1].subMenus[0].permissions,
      model: 'tab-2',
      admin: '管理员，音乐管理，类型管理，歌单管理，歌曲，权限管理，角色管理，菜单管理，授权管理，系统说明',
      editor: '小编，拥有音乐管理的新增、编辑权限，Dashboard、About等常规模块权限',
      other: 'other'
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
