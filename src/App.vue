<template>
  <Header/>
  <Calendar />
</template>

<script>
import Header from './components/Header.vue';
import Calendar from './components/Calendar.vue';

export default {
  name: 'App',
  components: {
    Header,
    Calendar,
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@100;200;300;400;500;600;700;800;900&display=swap');

*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
}
</style>
