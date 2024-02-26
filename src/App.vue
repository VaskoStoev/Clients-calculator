<template>
  <div class="container">
    <HeaderComponent msg="Clients Calculator" />
    <InputComponent />
  </div>
</template>

<script>
import InputComponent from './components/InputComponent.vue';
import './assets/app.css';
import HeaderComponent from './components/HeaderComponent.vue';
export default {
  name: 'App',
  components: {
    InputComponent,
    HeaderComponent,
  },
};
</script>
