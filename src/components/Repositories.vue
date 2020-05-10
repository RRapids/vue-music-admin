<template>
  <div>
    <v-card flat v-for="(item, index) in repos" :key="index">
      <v-card-text>
        <p class="title text--primary">
          {{ item.name }}
        </p>
        <p>{{ item.description }}</p>
        <div class="text--primary">
          <v-icon small color="green darken-2">mdi-checkbox-blank-circle</v-icon>
          {{ item.language }}
        </div>
      </v-card-text>
      <v-card-actions>
        <v-btn text color="deep-purple accent-4">
          Learn More
        </v-btn>
      </v-card-actions>
      <v-divider></v-divider>
    </v-card>
  </div>
</template>

<script>
export default {
  name: 'Repositories',
  data() {
    return {
      repos: []
    }
  },
  created() {
    this.axios.get('https://api.github.com/users/RRapids/repos').then((res) => {
      this.repos = res.data
      console.log(this.repos)
    })
  }
}
</script>

<style lang="scss" scoped></style>
