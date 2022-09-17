<template>
  <v-container>
    <v-card
      :loading="loadingLogin"
      elevation="18"
      outlined
      tile
      style="padding: 35px"
    >
      <v-card-title primary-title>
        <div>
          <h3 class="headline mb-0">Iniciar sesión</h3>
        </div>
      </v-card-title>
      <div style="padding: 35">
        <v-text-field
          name="name"
          label="Correo"
          id="id"
          v-model="email"
          outlined
        ></v-text-field>
        <v-text-field
          v-model="password"
          :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
          :rules="[rules.required]"
          :type="showPassword ? 'text' : 'password'"
          label="Password"
          counter
          outlined
          @click:append="showPassword = !showPassword"
        ></v-text-field>
      </div>
      <v-card-actions>
        <v-btn :loading="loadingLogin" @click="login()" color="primary"
          >Iniciar sesión</v-btn
        >
      </v-card-actions>
    </v-card>
    <v-snackbar
      :timeout="-1"
      :value="true"
      absolute
      v-model="logged_error"
      bottom
      color="error"
      outlined
      right
    >
      No se inició sesión
      <template v-slot:action="{ attrs }">
        <v-btn color="pink" text v-bind="attrs" @click="logged_error = false">
          Cerrar
        </v-btn>
      </template>
    </v-snackbar>
  </v-container>
</template>

<script>
export default {
    layout: 'login',
  data() {
    return {
      loadingLogin: false,
      password: '',
      email: '',
      showPassword: false,
      rules: {
        required: (value) => !!value || "Campo obligatorio.",
      },
      logged_error: false,
    };
  },
  methods: {
    login() {
      this.loadingLogin = true;
      this.$axios
        .$post("http://127.0.0.1:5000/login", {
          email: this.email,
          password: this.password,
        })
        .then((response) => {
          console.log(response);
          this.loadingLogin = true;
          if(response.status_code == 200){
            console.log("logged");
            localStorage.setItem("jwt", response.jwt);
            this.$router.push('/tarea/crear')
          }else{
            this.loadingLogin = false;
            this.logged_error = true;
          }
        }).catch(e => {
          console.log(e);
          this.loadingLogin = false;
          this.logged_error = true;
      });
    },
  },
};
</script>
