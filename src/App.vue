<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
  <!-- <HelloWorld msg="Hello Vue 3.0 + Vite" /> -->
  <SelectDrag />
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import SelectDrag from './components/SelectDrag.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld
    SelectDrag
  }
}
</script>
