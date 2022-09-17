<template>
    <v-container>
        <v-row>
            <v-col cols="12">
                <v-list dense nav>
                    <v-list-item v-for="item in items" :key="item.name">
                        <v-list-item-title>
                            <div style="border-style: solid; border-color: black;">
                                <p>id de la tarea:{{item.id}}</p>
                                <p>Nombre: {{item.name}}</p>
                                <p>Fecha de entrega: {{item.due_date}}</p>
                                <p>usuario: {{item.user}}</p>
                                <p>Completada: {{item.completed}}</p>
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
        getAssignments() {
            console.log("getting tasks");
            const headers = { 
                "jwt": localStorage.getItem("jwt"),
            };
            this.$axios
                .$get("http://127.0.0.1:5000/assignment/list", { headers })
                .then((response) => {
                    console.log(response);
                    for (let i = 0; i < response.length; i++) {
                        this.items.push({ id: i+1 ,name: response[i].name, due_date: response[i].due_date, user: response[i].user, completed: response[i].completed});
                    }
                });
        }
    },
    beforeMount() {
        this.getAssignments();
    }
};
</script>
