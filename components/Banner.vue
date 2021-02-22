<template>
  <header
    class="bg-cover Banner"
    :style="{
      backgroundImage: 'url(' + bannerMovieImageUrl + ')',
      backgroundPosition: 'center center',
    }"
  >
    <div class="Banner-contents">
      <h1 class="Banner-title">
        {{ bannerMovieTitle }}
      </h1>
      <div class="Banner-buttons">
        <button class="Banner-button">Play</button>
        <button class="Banner-button">My List</button>
      </div>
      <h1 class="Banner-Description">
        {{ bannerMovieOverview }}
      </h1>
    </div>
    <div class="Banner-fadeButtom" />
  </header>
</template>

<script>
import {
  computed,
  defineComponent,
  onMounted,
  ref,
} from '@nuxtjs/composition-api'
import useFetch from '@/composables/useFetch'
import { requests } from '@/composables/useTmdb'

export default defineComponent({
  name: 'Banner',
  props: {},
  setup() {
    const { response, fetchData } = useFetch(requests.feachNetflixOriginals, {})
    const bannerMovie = ref()
    const bannerMovieTitle = computed(() => {
      return (
        bannerMovie.value?.title ||
        bannerMovie.value?.name ||
        bannerMovie.value?.original_name
      )
    })
    const bannerMovieOverview = computed(() => bannerMovie.value?.overview)
    const bannerMovieImageUrl = computed(
      () =>
        `https://image.tmdb.org/t/p/original${bannerMovie.value?.backdrop_path}`
    )
    onMounted(async () => {
      await fetchData()
      bannerMovie.value =
        response.value.results[
          Math.floor(Math.random() * response.value.results.length - 1)
        ]
    })

    return {
      bannerMovie,
      bannerMovieTitle,
      bannerMovieOverview,
      bannerMovieImageUrl,
    }
  },
})
</script>

<style lang="scss" scoped>
.Banner {
  color: #fff;
  object-fit: contain;
  height: 448px;

  &-contents {
    margin-left: 30px;
    padding-top: 140px;
    height: 190px;
  }

  &-title {
    font-size: 3rem;
    font-weight: 800;
    padding-bottom: 0.3rem;
  }

  &-description {
    width: 45rem;
    line-height: 1.3;
    padding-top: 1rem;
    font-size: 0.8rem;
    max-width: 360px;
    height: 80px;
  }

  &-button {
    cursor: pointer;
    color: #fff;
    outline: none;
    border: none;
    font-weight: 700;
    border-radius: 0.2vw;
    padding-left: 2rem;
    padding-right: 2rem;
    margin-right: 1rem;
    padding-top: 0.5rem;
    background-color: rgba(51, 51, 51, 0.5);
    padding-bottom: 0.5rem;

    &:hover {
      color: #000;
      background-color: #e6e6e6;
      transition: all 0.2s;
    }
  }

  &-fadeBottom {
    height: 7.4rem;
    background-image: linear-gradient(
      180deg,
      transparent,
      rgba(37, 37, 37, 0.61),
      #111
    );
  }
}
</style>
