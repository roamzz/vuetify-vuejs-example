<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-card width="400" class="mx-auto mt-5">
          <v-card-title>
            <h1>Login</h1>
          </v-card-title>
          <v-card-text>
            <v-form>
              <v-text-field
                label="Username"
                prepend-icon="mdi-account-circle"
              />
              <v-text-field
                :type="showPassword ? 'text' : 'password'"
                prepend-icon="mdi-lock"
                label="Password"
                @click:append="showPassword = !showPassword"
                :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
              />
            </v-form>
          </v-card-text>
          <v-card-actions>
            <v-btn color="success">Register</v-btn>
            <v-spacer></v-spacer>
            <v-btn color="info">Login</v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "Login",

  data() {
    return {
      showPassword: false
    };
  }
};
</script>
