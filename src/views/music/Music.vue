<template>
  <div style="padding-top:10px;">
    <v-card>
      <v-card-title>
        <span class="b-btn">
          <v-btn color="Disabled" @click="expor()">导出</v-btn>
        </span>
        <v-spacer></v-spacer>
        <v-text-field
          v-model="search"
          append-icon="mdi-magnify"
          label="Search"
          @keyup.enter="_search()"
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
      search: '',
      headers: [
        { text: '', value: 'song_id' },
        {
          text: '歌曲',
          align: 'start',
          sortable: false,
          value: 'song_name'
        },
        { text: '歌手', value: 'singer' },
        // { text: '喜欢数', value: 'like_count' },
        { text: '评论数', value: 'comment_count' },
        { text: '时长', value: 'duration' },
        { text: '创建时间', value: 'create_time' }
      ],
      desserts: []
    }
  },
  created() {
    console.log(this.$options.name)
    this.axios.get(this.GLOBAL.baseUrl + '/song/list').then((res) => {
      this.desserts = res.data.data
      console.log(this.desserts)
    })
  },
  methods: {
    //模糊查询歌曲
    _search() {
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
      this.axios.get(this.GLOBAL.baseUrl + '/song/export').then((res) => {
        if (res.data.code === 1) {
          alert('导出成功')
        }
      })
      console.log('export')
    }
  }
}
</script>

<style scoped lang="scss">
.b-btn {
  left: 30%;
}
</style>
