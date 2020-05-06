<template>
  <div>
    <span>
      <mu-button class="gutter" @click="expor()">导出</mu-button>
    </span>
    <span>
      <mu-text-field v-model="keywords" placeholder="输入关键词搜索"></mu-text-field>
      <mu-button color="success" @click="search()">搜索</mu-button>
    </span>

    <v-row justify="space-around">
      <v-col cols="12" sm="18" md="15" lg="30">
        <v-sheet elevation="10" class="pa-4" style="padding:15px">
          <h2 class="title mb-2">All Types</h2>
          <v-btn text color="primary" v-for="(type, index) in types" :key="index" :value="index" @click="showList(index)">
            {{ type.type }}
          </v-btn>
        </v-sheet>
      </v-col>
    </v-row>

    <mu-row v-if="show">
      <mu-col span="4" v-for="(child, index) in types[typeId].child" :key="index">
        <div class="grid-cell">
          <v-card class="mx-auto" max-width="344" outlined>
            <v-list-item three-line>
              <v-list-item-content>
                <v-list-item-title class="headline mb-1">{{ child.song_list_name }}</v-list-item-title>
                <v-list-item-subtitle>歌曲数：{{ child.song_count }}</v-list-item-subtitle>
                <v-list-item-subtitle>收藏数：{{ child.like_count }}</v-list-item-subtitle>
                <v-list-item-subtitle>创建时间：{{ child.create_time }}</v-list-item-subtitle>
              </v-list-item-content>
              <v-list-item-avatar tile size="80" color="grey"><img :src="child.thumbnail" alt=""/></v-list-item-avatar>
              <!-- <v-img :src="child.thumbnail" size="80"></v-img> -->
            </v-list-item>

            <v-card-actions>
              <v-btn text>Explore</v-btn>
              <v-btn text>Delete</v-btn>
            </v-card-actions>
          </v-card>
        </div>
      </mu-col>
    </mu-row>
  </div>
</template>

<script>
export default {
  name: 'MusicList',
  data() {
    return {
      selected: [],
      menuList: this.$store.state.menuList,
      menus: [],
      types: [],
      typeId: 0,
      songList: [],
      keywords: '',
      show: true
    }
  },
  created() {
    for (let i = 0; i < this.menuList.length; i++) {
      let parent = this.menuList[i]
      for (let j = 0; j < parent.subMenus.length; j++) {
        let child = this.menuList[i]
        if (child.subMenus[j].path === this.$options.name) {
          this.menus = child.subMenus[j].subMenus
        }
      }
    }
    //获取所有歌曲
    this.axios.get(this.GLOBAL.baseUrl + '/songList/type').then((res) => {
      this.types = res.data.data
      console.log(this.types)
    })
  },
  methods: {
    showList(Id) {
      this.show = !this.show
      this.typeId = Id
    },
    // 模糊查询歌单
    search() {
      this.axios({
        method: 'get',
        url: this.GLOBAL.baseUrl + '/songList/select',
        // 问号带参，表单提交
        params: {
          field: this.keywords
        }
      }).then((res) => {
        this.songList = res.data.data
      })
      this.show = !this.show
    }
  }
}
</script>

<style scoped lang="scss">
.tui {
  color: #1a1a1a;
  font-size: 18px;
  line-height: 28px;
  max-height: 56px;
  font-weight: 600;
  margin-left: 5px;
}
.gutter {
  margin-right: 10px;
  margin-top: 13px;
}
</style>
