<template>
  <v-navigation-drawer dark color="primary" left app>
    <v-list-item>
      <v-list-item-content>
        <v-list-item-title class="text-h6"> Menú </v-list-item-title>
      </v-list-item-content>
    </v-list-item>

    <v-divider></v-divider>

    <v-list dense nav>
      <v-list-item v-for="item in items" :key="item.title" link>
        <v-list-item-icon>
        </v-list-item-icon>

        <v-list-item-content>
          <v-list-item-title>
            <NuxtLink :to="item.url">{{ item.title }}</NuxtLink>
            
          </v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list>
  </v-navigation-drawer>
</template>
<script>
export default {
  data(){
    return{
      items:[
        {
          title:"Crear Clase",
          url:"/clase/crear"
        },
        {
          title:"Crear tarea",
          url:"/tarea/crear"
        },
        {
          title:"Mostrar Clases",
          url:"/clase/clases/"
        },
        {
          title:"Mostrar Tareas",
          url:"/tarea/tareas"
        },
      ]
    }
  }
};
</script>
<style>
.v-application a{
  color:white!important;
}
</style>
