<template>
    <v-container>
        <v-row>
            <v-col cols="12">
                <v-list dense nav>
                    <v-list-item v-for="item in items" :key="item.name">
                        <v-list-item-title>
                            <div style="border-style: solid; border-color: black;">
                                <b>id de la materia:{{item.id+1}}</b>
                                <p>Materia: {{item.name}}</p>
                                <p>Profesor: {{item.professor}}</p>
                                <br>
                            </div>
                        </v-list-item-title>
                    </v-list-item>
                </v-list>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
export default {
    data() {
        return {
            saving: false,
            saved: false,
            newClass: {},
            items: []
        };
    },
    methods: {
        getClasses() {
            console.log("getting classes");
            const headers = { 
                "jwt": localStorage.getItem("jwt"),
            };
            this.$axios
                .$get("http://127.0.0.1:5000/class/list", { headers })
                .then((response) => {
                    console.log(response);
                    for (let i = 0; i < response.length; i++) {
                        this.items.push({ id: i, name: response[i].name, professor: response[i].professor});
                    }
                });
        }
    },
    beforeMount() {
        this.getClasses();
    }
};
</script>
