<template>
  <div>
    <v-card max-width="1000" class="mx-auto">
      <v-toolbar color="teal" dark>
        <v-app-bar-nav-icon></v-app-bar-nav-icon>

        <v-toolbar-title>Settings</v-toolbar-title>
      </v-toolbar>

      <v-list subheader two-line flat>
        <v-subheader>type management</v-subheader>

        <v-list-item-group v-model="settings" multiple>
          <v-list-item v-for="(item, index) in types" :key="index">
            <v-list-item-action>
              <v-checkbox color="primary"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title>{{ item.type }}</v-list-item-title>
              <v-list-item-subtitle>Allow notifications</v-list-item-subtitle>
            </v-list-item-content>

            <v-list-item-action>
              <v-btn class="mx-2" fab dark small color="teal">
                <v-icon dark>mdi-minus</v-icon>
              </v-btn>
            </v-list-item-action>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-card>
  </div>
</template>

<script>
export default {
  name: 'MusicType',
  data() {
    return {
      keywords: '',
      menus: [],
      types: [],
      settings: []
    }
  },
  mounted() {},
  created() {
    console.log(this.$options.name)
    //获取所有歌曲
    this.axios.get(this.GLOBAL.baseUrl + '/songList/type').then((res) => {
      this.types = res.data.data
      console.log(this.types)
    })
  },
  methods: {}
}
</script>

<style scoped lang="scss"></style>
