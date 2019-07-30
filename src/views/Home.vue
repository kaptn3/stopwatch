<template>
  <div class="home">
    <moment/>
  </div>
</template>

<script>
import Moment from '@/components/Moment';

export default {
  name: 'home',
  components: { Moment }
};
</script>

<style scoped>
  .home {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
