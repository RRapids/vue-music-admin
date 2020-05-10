<template>
  <div>
    <v-card flat v-for="(item, index) in stars" :key="index">
      <v-card-text>
        <p class="title text--primary">
          {{ item.full_name }}
        </p>
        <p>{{ item.description }}</p>
        <div class="text--primary">
          <v-icon small color="green darken-2">mdi-checkbox-blank-circle</v-icon>
          {{ item.language }}
          <v-icon small color="blue darken-2">mdi-star</v-icon>
          {{ item.stargazers_count }}
          <v-icon small color="purple darken-2">mdi-source-branch</v-icon>
          {{ item.forks_count }}
        </div>
      </v-card-text>
      <v-divider></v-divider>
    </v-card>
  </div>
</template>

<script>
export default {
  name: 'Stars',
  data() {
    return {
      stars: []
    }
  },
  created() {
    this.axios.get('https://api.github.com/users/RRapids/starred').then((res) => {
      this.stars = res.data
      console.log(this.stars)
    })
  }
}
</script>

<style lang="scss" scoped></style>
