<template>
  <div style="padding-top:10px;">
    <v-card>
      <v-card-title>
        <span class="b-btn">
          <v-btn color="Disabled" @click="expor()">导出</v-btn>
          <v-btn color="error">删除</v-btn>
        </span>
        <v-spacer></v-spacer>
        <v-text-field
          v-model="search"
          append-icon="mdi-magnify"
          label="Search"
          @keyup.enter="cha()"
          single-line
          hide-details
        ></v-text-field>
      </v-card-title>
      <v-data-table :headers="headers" :items="desserts" :search="search"></v-data-table>
    </v-card>
  </div>
</template>

<script>
export default {
  name: 'Music',
  data() {
    return {
      menuList: this.$store.state.menuList,
      search: '',
      headers: [
        {
          text: '歌曲',
          align: 'start',
          sortable: false,
          value: 'song_name'
        },
        { text: '歌手', value: 'singer' },
        { text: '喜欢数(w)', value: 'like_count' },
        { text: '评论数(w)', value: 'comment_count' },
        { text: '创建时间', value: 'create_time' },
        { text: '时长', value: 'duration' }
      ],
      desserts: []
    }
  },
  created() {
    console.log(this.$options.name)
    for (let i = 0; i < this.menuList.length; i++) {
      let parent = this.menuList[i]
      for (let j = 0; j < parent.subMenus.length; j++) {
        let child = this.menuList[i]
        if (child.subMenus[j].path === this.$options.name) {
          this.menus = child.subMenus[j].subMenus
          console.log(JSON.stringify(this.menus))
        }
      }
    }
    this.axios.get(this.GLOBAL.baseUrl + '/song/list').then((res) => {
      this.desserts = res.data.data
      console.log(this.desserts)
    })
  },
  methods: {
    //模糊查询歌曲
    cha() {
      this.axios({
        method: 'get',
        url: this.GLOBAL.baseUrl + '/songList/select',
        // 问号带参，表单提交
        params: {
          field: this.search
        }
      }).then((res) => {
        this.desserts = res.data.data
      })
    },
    expor() {
      this.axios({
        method: 'get',
        url: this.GLOBAL.baseUrl + '/song/export'
      }).then((res) => {
        if (res.data.code === 1) {
          alert('导出成功')
        }
      })
    }
  }
}
</script>

<style scoped lang="scss">
.b-btn {
  left: 30%;
}
</style>
