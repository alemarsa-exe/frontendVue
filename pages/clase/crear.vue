<template>
    <v-container>
        <v-row>
            <v-col cols="12">
                <h2>Crear una clase</h2>
                <v-form>
                    <v-text-field name="name" v-model="newClass.name" outlined label="Nombre" id="id"></v-text-field>
                    <v-text-field name="professor" v-model="newClass.professor" outlined label="Profesor" id="id"></v-text-field>
                </v-form>
                <v-btn @click="saveClass()" :loading="saving" rounded color="primary" :disabled="saved">Guardar</v-btn>
            </v-col>
        </v-row>
        <v-snackbar :timeout="-1" :value="true" absolute v-model="saved" bottom color="success" outlined right>
            Tu clase se creó con éxito
            <template v-slot:action="{ attrs }">
                <v-btn color="pink" text v-bind="attrs" @click="saved = false">
                    Cerrar
                </v-btn>
            </template>
        </v-snackbar>
    </v-container>
</template>

<script>
export default {
    data() {
        return {
            saving: false,
            saved: false,
            newClass: {},
        };
    },
    methods: {
        saveClass() {
            this.saving = true;
            this.$axios
                .$post("http://127.0.0.1:5000/class/create", this.newClass, {
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
