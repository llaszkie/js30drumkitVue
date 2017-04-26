<template>
  <div class="keys">
    <keyelem v-for="singleKey in keys" :key="singleKey.id" :singleKey="singleKey">
    </keyelem>
  </div>
</template>

<script>
  import keyData from '../keysData.js'
  import keyelem from './Key.vue'

  export default {
    data () {
      return {
        keys: keyData
      }
    },
    components: {
      keyelem: keyelem
    }
  }
</script>

<style scoped>
  .keys {
    display: flex;
    flex: 1;
    min-height: 100vh;
    align-items: center;
    justify-content: center;
  }
</style>
