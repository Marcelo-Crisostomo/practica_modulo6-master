<template>
  <div class="home">
    
   
    
    <Juegos></Juegos>
  </div>
</template>

<script>
// @ is an alias to /src

import Juegos from '@/components/Juegos.vue';

export default {
  name: 'HomeView',
  components: {
    Juegos
  }
}
</script>