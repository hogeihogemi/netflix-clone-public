<template>
  <div class="Nav" :class="{ 'Nav-black': isShow }">
    <img
      class="Nav-logo"
      src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/08/Netflix_2015_logo.svg/1920px-Netflix_2015_logo.svg.png"
      alt="Netflix Logo"
    />
    <img
      class="Nav-avater"
      src="https://i.pinimg.com/originals/0d/dc/ca/0ddccae723d85a703b798a5e682c23c1.png"
      alt="Avatar"
    />
  </div>
</template>

<script>
import { defineComponent, onMounted, ref } from '@nuxtjs/composition-api'

export default defineComponent({
  name: 'Nav',
  setup() {
    const isShow = ref(false)
    const handleShow = () => {
      if (window.scrollY > 100) {
        isShow.value = true
      } else {
        isShow.value = false
      }
    }
    onMounted(() => window.addEventListener('scroll', handleShow))

    return { isShow }
  },
})
</script>

<style lang="scss" scoped>
.Nav {
  position: fixed;
  top: 0;
  width: 100%;
  padding: 20px;
  height: 70px;
  z-index: 1;
  display: flex;
  justify-content: space-between;

  /* Animations */
  transition-timing-function: ease-in;
  transition: all 0.5s;

  &-black {
    background-color: #111;
  }

  &-logo {
    position: fixed;
    left: 20px;
    width: 80px;
    object-fit: contain;
  }

  &-avater {
    position: fixed;
    right: 20px;
    width: 30px;
    object-fit: contain;
  }
}
</style>
