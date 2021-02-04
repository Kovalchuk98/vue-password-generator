<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
    <h3>Password Generator</h3>
    </v-app-bar>

    <v-main>
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
