<template>
  <div>
    <v-date-picker v-model="date" full-width :landscape="$vuetify.breakpoint.smAndUp" class="mt-4"></v-date-picker>
    <v-parallax src="https://cdn.vuetifyjs.com/images/parallax/material.jpg"></v-parallax>
  </div>
</template>

<script>
export default {
  name: 'Dashboard',
  data: () => ({
    date: new Date().toISOString().substr(0, 10),
    show: false,
    items: [
      {
        color: '#1F7087',
        src: 'https://cdn.vuetifyjs.com/images/cards/foster.jpg',
        title: 'Supermodel',
        artist: 'Foster the People'
      },
      {
        color: '#952175',
        src: 'https://cdn.vuetifyjs.com/images/cards/halcyon.png',
        title: 'Halcyon Days',
        artist: 'Ellie Goulding'
      }
    ]
  })
}
</script>

<style scoped lang="scss"></style>
