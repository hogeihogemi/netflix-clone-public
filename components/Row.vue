<template>
  <div class="Row">
    <h2>{{ title }}</h2>
    <div class="Row-posters">
      <img
        class="Row-poster"
        :class="{ 'Row-poster-large': isLargeRow }"
        v-for="movie in response.results"
        :src="`${baseUrl}${
          isLargeRow ? movie.poster_path : movie.backdrop_path
        }`"
        :key="movie.id"
        :alt="movie.name"
      />
    </div>
  </div>
</template>

<script>
import { defineComponent, onMounted } from '@nuxtjs/composition-api'
import useFetch from '@/composables/useFetch'

export default defineComponent({
  name: 'Row',
  props: {
    title: { type: String },
    fetchUrl: { type: String },
    isLargeRow: { type: Boolean },
  },
  setup(props) {
    const { response, fetchData } = useFetch(props.fetchUrl, {})
    const baseUrl = 'https://image.tmdb.org/t/p/original'

    onMounted(() => {
      fetchData()
    })

    return { props, response, baseUrl }
  },
})
</script>

<style lang="scss" scoped>
h2 {
  font-size: 1.5em;
  font-weight: bold;
}
.Row {
  margin-left: 20px;
  color: #fff;

  &-posters {
    display: flex;
    overflow-y: hidden;
    overflow-x: scroll;
    padding: 20px;

    &::-webkit-scrollbar {
      display: none;
    }
  }

  &-poster {
    object-fit: contain;
    width: 100%;
    max-height: 100px;
    margin: 10px;
    transition: transform 450ms;

    &-large {
      max-height: 250px;

      &:hover {
        transform: scale(1.09);
      }
    }

    &:hover {
      transform: scale(1.08);
    }
  }
}
</style>
