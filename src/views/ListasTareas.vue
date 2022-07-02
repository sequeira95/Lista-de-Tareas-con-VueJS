<template>
    <v-container class="ma-0">
        <v-row>
            <v-col cols="12" sm="6" class="mt-3 scrollContenedor " order-sm="first" order="last">
                <v-card class="mb-3 scroll" max-width="500"
                v-for="(item, index) in listasTareas" :key="index">
                    <v-card-title>
                        {{item.titulo}}
                    </v-card-title>
                    <v-card-text>
                        {{item.contenido}}
                    </v-card-text>
                    <v-card-actions>
                        <v-btn color="warning" outlined @click="editar(index)">
                            Modificar
                        </v-btn>
                        <v-btn color="error" outlined @click="eliminarTarea(index)">
                            Eliminar
                        </v-btn>
                    </v-card-actions>
                </v-card>
            </v-col>
            <v-col cols="12" sm="6" class="mt-3 pa-3" order-sm="last" order="first"
            v-if="formAgregar">
                <v-card>
                    <v-form @submit.prevent="agregarTarea">
                        <v-text-field class="pa-3" label="Titulo de la tarea" v-model="titulo"></v-text-field>
                        <v-textarea class="pa-3" label="Descripcion" v-model="descripcion"></v-textarea>
                        <v-btn color="success" block type="submit">Agregar tarea</v-btn>
                    </v-form>
                </v-card>
            </v-col>
            <v-col cols="12" sm="6" class="mt-3 pa-3" 
            v-if="!formAgregar">
                <v-card>
                    <v-form @submit.prevent="editarTarea">
                        <v-text-field class="pa-3" label="Titulo de la tarea" v-model="titulo"></v-text-field>
                        <v-textarea class="pa-3" label="Descripcion" v-model="descripcion"></v-textarea>
                        <v-btn color="warning" block type="submit" >Editar tarea</v-btn>
                    </v-form>
                </v-card>
            </v-col>
        </v-row>
        <v-snackbar
            v-model="snackbar"
            min-width="100px">
                {{ mensaje }}
                <v-btn
                    color="pink"
                    text
                    @click="snackbar = false"
                    >
                    <v-icon>close</v-icon>
                </v-btn>
    </v-snackbar>
    </v-container>
</template>

<script>
export default {
    data (){
        return {
            listasTareas: [{
                id:1,
                titulo: 'Tarea #1',
                contenido: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Veritatis voluptatum laboriosam debitis. Sunt vitae minus maiores quasi, tempore, ad et veniam beatae corrupti voluptatem odio obcaecati ducimus quos vero quod!'
            },
            {
                id:2,
                titulo: 'Tarea #2',
                contenido: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Veritatis voluptatum laboriosam debitis. Sunt vitae minus maiores quasi, tempore, ad et veniam beatae corrupti voluptatem odio obcaecati ducimus quos vero quod!'
            }
            ],
            titulo: '',
            descripcion: '',
            snackbar: false,
            mensaje: '',
            formAgregar: true,
            indexTarea: ''
        }
    },
    methods: {
        agregarTarea (){
            if(this.titulo === '' || this.descripcion === ''){
                this.snackbar = true
                this.mensaje = '⚠️Por favor llenar el formulario correctamente'
            } else {
                this.listasTareas.push({
                    id: Date.now(),
                    titulo: this.titulo,
                    contenido: this.descripcion
                })
                this.titulo = ''
                this.descripcion = ''
                this.snackbar = true
                this.mensaje = 'Tarea agregada ✔️' 
            }
        },
        eliminarTarea (index){
            this.listasTareas.splice(index,1)
        },
        editar (index) {
            this.formAgregar = false
            this.titulo = this.listasTareas[index].titulo
            this.descripcion = this.listasTareas[index].contenido
            this.indexTarea = index
        },
        editarTarea (){
            this.listasTareas[this.indexTarea].titulo = this.titulo
            this.listasTareas[this.indexTarea].contenido = this.descripcion
            this.titulo = ''
            this.descripcion = ''
            this.formAgregar = true
            this.mensaje = 'Tarea editada'

        }
    }
}
</script>

<style scoped>
.scrollContenedor{
    display: flex;
    flex-direction: column;
    scroll-snap-type: y mandatory;
    overflow: hidden auto;
    max-height: 80vh;

}
.scroll{
    scroll-snap-align: initial;
}
</style>

