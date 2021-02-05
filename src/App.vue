<template>
  <v-app>
    <v-app-bar
      app
      color="#041948"
      dark
    >
    <h3>Password Generator</h3>
    </v-app-bar>

    <v-main class="wrapper">
      <PasswordForm/>
    </v-main>
  </v-app>
</template>

<script>
import PasswordForm from './components/PasswordForm';

export default {
  name: 'App',

  components: {
    PasswordForm,
  },

  data: () => ({
  }),
};
</script>

<style lang="scss">
    .wrapper {
     background-color: #8BC6EC;
     background-image: linear-gradient(135deg, #8BC6EC 0%, #9599E2 100%)
    }
</style>
