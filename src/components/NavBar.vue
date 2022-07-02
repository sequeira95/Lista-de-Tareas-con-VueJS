<template>
    <div>
        <v-toolbar
            dark
            dense
            src="https://cdn.vuetifyjs.com/images/backgrounds/vbanner.jpg"
        >
        <v-app-bar-nav-icon @click="cerrarNavBar = !cerrarNavBar"></v-app-bar-nav-icon>
        <v-toolbar-title>Tareas <v-icon>assignment</v-icon></v-toolbar-title>
        <v-spacer></v-spacer>
        </v-toolbar>
        <div>
        <v-navigation-drawer v-model="cerrarNavBar"
            absolute
            temporary
            color="rgb(0, 29, 153,0.41)">
            <v-container>
            <v-btn icon
                absolute
                right
                @click="cerrarNavBar = false">
            <v-icon>close</v-icon>
            </v-btn>
            </v-container>
            <v-container >
                <v-list-item class="d-flex justify-center mt-5">
                    <v-avatar>
                        <v-img src="https://randomuser.me/api/portraits/men/78.jpg"></v-img>
                    </v-avatar>
                </v-list-item>
                <v-container column>
                    <v-row>
                        <v-btn text
                        color="white">
                            Inicio
                        </v-btn>
                    </v-row>
                    <v-row>
                        <v-btn text
                        color="white"
                        :to="{ name: 'listasTareas' }">
                        Listas de Tareas
                        </v-btn>
                    </v-row>
                </v-container>
            </v-container>
        </v-navigation-drawer>
        </div>
    </div>
</template>
<script>

export default ({
    name: 'NavBar',
    data  () {
        return {
            cerrarNavBar: false
        }
    }
})
</script>
>