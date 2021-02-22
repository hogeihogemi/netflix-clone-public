<template>
  <div class="App">
    <Nav />
    <Banner />
    <Row
      :title="'NETFLIX ORIGINALS'"
      :fetchUrl="requests.feachNetflixOriginals"
      :isLargeRow="true"
    />
    <Row title="Trending Now" :fetchUrl="requests.feachTrending" />
    <Row title="Top Rated" :fetchUrl="requests.feactTopRated" />
    <Row title="Action Movies" :fetchUrl="requests.feactActionMovies" />
    <Row title="Comedy Movies" :fetchUrl="requests.feactComedyMovies" />
    <Row title="Horror Movies" :fetchUrl="requests.feactHorrorMovies" />
    <Row title="Romance Movies" :fetchUrl="requests.feactRomanceMovies" />
    <Row title="Documentaries" :fetchUrl="requests.feactDocumentMovies" />
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from '@nuxtjs/composition-api'
import Row from '@/components/Row.vue'
import Banner from '@/components/Banner.vue'
import Nav from '@/components/Nav.vue'
import { requests } from '@/composables/useTmdb'

export default defineComponent({
  head: {},
  props: {},
  components: {
    Row,
    Banner,
    Nav,
  },
  setup() {
    const state = reactive({
      cards: ['1', '2'],
      isLoading: true,
    })

    return { state, requests }
  },
})
</script>

<style lang="scss" scoped>
.App {
  background-color: #111;
}
</style>
