<template>
  <v-app>
    <!-- 顶部导航 -->
    <v-app-bar dense dark height="80" app>
      <!-- <v-app-bar-nav-icon @click="$router.push('/')"></v-app-bar-nav-icon> -->
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
      <v-toolbar-title>{{ user.login }}</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>

      <v-menu left bottom>
        <template v-slot:activator="{ on }">
          <v-btn icon v-on="on">
            <v-icon>mdi-dots-vertical</v-icon>
          </v-btn>
        </template>

        <v-list>
          <v-list-item link>
            <v-list-item-title>设置</v-list-item-title>
          </v-list-item>
          <v-list-item link>
            <v-list-item-title @click="logout">退出</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>
    <!-- 内容 -->
    <v-content>
      <v-container>
        <v-row>
          <!-- 头像 -->
          <v-col cols="12" md="3">
            <v-card>
              <v-img :src="user.avatar_url"></v-img>
            </v-card>
          </v-col>
          <!-- 右上 -->
          <v-card width="800px">
            <v-tabs v-model="tab">
              <v-tab>
                Repositories
                <div class="my-2">
                  <v-btn depressed small>{{ user.public_repos }}</v-btn>
                </div>
              </v-tab>

              <v-tab>
                Stars
                <div class="my-2">
                  <v-btn depressed small>13</v-btn>
                </div>
              </v-tab>

              <v-tab>
                Following
                <div class="my-2">
                  <v-btn depressed small>{{ user.following }}</v-btn>
                </div>
              </v-tab>
            </v-tabs>
            <!-- 组件 -->
            <v-tabs-items v-model="tab">
              <!-- Repositories -->
              <v-tab-item>
                <Repositories />
              </v-tab-item>
              <!-- Stars -->
              <v-tab-item>
                <Stars />
              </v-tab-item>
              <!--following  -->
              <v-tab-item>
                <Following />
              </v-tab-item>
              <!-- 按钮封装 -->
              <!-- <v-tab-item>
                <Btn>默认按钮</Btn>
                <Btn type="error">红色按钮</Btn>
                <Btn type="success">绿色按钮</Btn>
                <Btn type="primary">蓝色按钮</Btn>
              </v-tab-item> -->
            </v-tabs-items>
          </v-card>
        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import Repositories from '../../components/Repositories'
import Stars from '../../components/Stars'
// import Followers from '../../components/Followers'
import Following from '../../components/Following'
// import Btn from '../../components/Button'
export default {
  name: 'Auth',
  data() {
    return {
      user: null,
      tab: null,
      following: []
    }
  },
  components: {
    Repositories,
    Stars,
    // Followers,
    Following
  },
  created() {
    console.log('回调')
    let user = this.$route.query.user
    if (user) {
      console.log(user)
      this.user = JSON.parse(user)
      localStorage.setItem('token', this.user.id)
      localStorage.setItem('user', user)
    }
  },
  mounted() {},
  methods: {
    logout() {
      localStorage.removeItem('token')
      localStorage.removeItem('user')
      this.$router.push('/login')
    },
    confirm() {
      if (!this.companyName) {
        this.$refs.btn.cancel()
      }
    }
  },
  computed: {}
}
</script>

<style scoped lang="scss"></style>
