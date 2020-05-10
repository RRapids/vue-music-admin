<template>
  <div>
    <v-card flat v-for="(item, index) in following" :key="index">
      <v-list two-line>
        <v-list-item>
          <v-list-item-avatar>
            <img :src="item.avatar_url" />
          </v-list-item-avatar>
          <v-list-item-content>
            <v-card-text>
              {{ item.login }}
            </v-card-text>
          </v-list-item-content>
          <!-- <v-list-item-action> <v-btn small depressed>UnFollow</v-btn></v-list-item-action> -->
          <v-list-item-action>
            <Btn @cancel-click="clickEvent($event, index)">UnFollow</Btn>
          </v-list-item-action>
        </v-list-item>
        <v-divider></v-divider>
      </v-list>
    </v-card>
  </div>
</template>

<script>
import Btn from '../components/Button'
export default {
  name: 'Following',
  data() {
    return {
      following: []
    }
  },
  components: {
    Btn
  },
  created() {
    this.axios.get('https://api.github.com/users/RRapids/following').then((value) => {
      this.following = value.data
      console.log(this.following)
    })
  },
  methods: {
    clickEvent(event, index) {
      console.log(index)
      this.following.splice(index, 1)
      // this.$emit('cancel-click', event)
    }
  }
}
</script>

<style lang="scss" scoped></style>
