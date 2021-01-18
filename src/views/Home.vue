<template>
  <div class="home">
    <Coments msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import Coments from '@/components/Comments.vue'

export default {
  name: 'Home',
  components: {
    Coments
  }
}
</script>
