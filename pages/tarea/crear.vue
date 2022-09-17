<template>
  <v-row>
    <v-col cols="12">
      <v-form>
        {{newAssignment}}
        <v-text-field
          outlined
          v-model="newAssignment.name"
          name="name"
          label="Nombre de la tarea"
          id="id"
        ></v-text-field>
        <input type="checkbox" id="checkbox" v-model="newAssignment.completed"> Tarea completada
        <br>
        <br>
      <v-date-picker
        v-model="newAssignment.due_date"
        name="due_date"
      ></v-date-picker>

    </v-form>
    <v-btn
          @click="saveAssignment()"
          :loading="saving"
          rounded
          color="primary"
          :disabled="saved"
          >Guardar</v-btn
        >
    <v-snackbar
      :timeout="-1"
      :value="true"
      absolute
      v-model="saved"
      bottom
      color="success"
      outlined
      right
    >
      Tu tarea se registró con éxito
      <template v-slot:action="{ attrs }">
        <v-btn color="pink" text v-bind="attrs" @click="saved = false">
          Cerrar
        </v-btn>
      </template>
    </v-snackbar>

    </v-col>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      newAssignment: {},
      saving: false,
      saved: false,
      date: null,
      time: null,
    };
  },
  methods: {
    saveAssignment() {
      this.saving = true;
      delete this.newAssignment.student;
      this.$axios
        .$post("http://127.0.0.1:5000/assignment/create",this.newAssignment, {
          headers: {
            jwt: localStorage.getItem("jwt"),
          },
        })
        .then((response) => {
          console.log(response);
          this.saved = true;
          this.saving = false;
        });
    },
  },
};
</script>
