<script >
import AppTitle from './components/AppTitle.vue';
import AppHero from './components/AppHero.vue';


export default {
  components: {
    AppTitle,
    AppHero
  }
}

</script>

<template>
  <div>
    <AppTitle/>
    <AppHero/>
  </div>
</template>

<style scoped>
  div{
    text-align: center;
    margin-top: 2.5rem;
  }
</style>
