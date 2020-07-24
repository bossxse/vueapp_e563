<template>
  <v-card color="pink lighten-1">
    <center>
      <v-icon size="120" color="rainbow">
        looks
      </v-icon>
      <h1>SIGN IN</h1>
    </center>

    <v-card-text>
      <v-form>
        <v-text-field prepend-icon="mdi-account-circle" label="Username" />
        <v-text-field
          :type="showPassword ? 'text' : 'password'"
          label="Password"
          prepend-icon="mdi-lock"
          :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
          @click:append="showPassword = !showPassword"
        />
      </v-form>
    </v-card-text>
    <v-card-actions>
      <nuxt-link to="register">
        <v-btn color="primary">
          <v-icon>loupe</v-icon>
          REGISTER
        </v-btn>
      </nuxt-link>
      <v-spacer />
      <nuxt-link to="menu">
        <v-btn color="success">
          <v-icon>forward</v-icon>
          LOGIN
        </v-btn>
      </nuxt-link>
    </v-card-actions>
  </v-card>
</template>
<script>
export default {
  name: 'App',
  data () {
    return {
      showPassword: false,
    }
  },
}
</script>
