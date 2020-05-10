<template>
  <div>
    <v-card flat v-for="(item, index) in followers" :key="index">
      <v-list two-line>
        <v-list-item>
          <v-list-item-avatar>
            <img :src="item.avatar_url" />
          </v-list-item-avatar>
          <v-list-item-content>
            <v-card-text>{{ item.login }}</v-card-text>
          </v-list-item-content>
          <v-list-item-action> <v-btn small depressed>Follow</v-btn></v-list-item-action>
        </v-list-item>
        <v-divider></v-divider>
      </v-list>
    </v-card>
  </div>
</template>

<script>
export default {
  name: 'Followers',
  data() {
    return {
      followers: []
    }
  },
  created() {
    this.axios.get('https://api.github.com/users/RRapids/followers').then((value) => {
      this.followers = value.data
      console.log(this.followers)
    })
  }
}
</script>

<style lang="scss" scoped></style>
