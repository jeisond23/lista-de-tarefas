<script>
    // Código Javascript aqui
    export default {
        data() {
            return {
                // Propriedades aqui.
                tarefas: [],
                novaTarefa: {
                    titulo: "",
                    // texto: "",
                    concluida: false
                },
                error: "",
                editar: false,
                id_editar: undefined
            }
        },
        methods: {
            adicionarTarefa: function(){
                // Código aqui
                if(this.novaTarefa.titulo && !this.editar) {
                    if(this.novaTarefa.titulo && this.novaTarefa.texto){
                        this.tarefas.push(this.novaTarefa);
                        this.novaTarefa = {
                            concluida: false
                        };
                        this.error = "";
                        localStorage.setItem("tarefas", JSON.stringify(this.tarefas));
                    } else {
                        this.error = "Você não informou um título ou tarefa!!!";
                        // alert("Uma tarefa deve ser informada!!!");
                    }
                    
                } else {
                    if(this.novaTarefa.titulo ){
                        //this.tarefas.push(this.novaTarefa);
                        this.tarefas[this.id_editar].titulo = this.novaTarefa.titulo;
                        this.tarefas[this.id_editar].texto = this.novaTarefa.texto;
                        this.editar = false;
                        this.id_editar = undefined;
                        this.novaTarefa = {
                            concluida: false
                        };
                        this.error = "";
                        localStorage.setItem("tarefas", JSON.stringify(this.tarefas));
                    } else {
                        this.error = "Você não informou a tarefa!!!";
                        // alert("Uma tarefa deve ser informada!!!");
                    }
                }
            },
            excluirTarefa: function(id) {
                // Código aqui
                let tmp = this.tarefas[id].titulo;
                this.tarefas.splice(id, 1);
                localStorage.setItem("tarefas", JSON.stringify(this.tarefas));
                alert("tarefa " + tmp + " removida!!!");
            },
            editarTarefa: function(id) {
                // Código aqui
                 this.novaTarefa.titulo = this.tarefas[id].titulo;
                 this.novaTarefa.texto = this.tarefas[id].texto;
                 this.editar = true;
                 this.id_editar = id;
                 this.$refs.tarefa.focus();
            },
            cancelar: function () {
                this.editar = false;
                this.id_editar = undefined;
                this.novaTarefa = {
                    concluida: false
                };
                this.error = "";
            },
            removerTarefas: function() {
                // Código aqui
                localStorage.removeItem("tarefas");
                this.tarefas = [];
                if(this.error) this.error = "";
                alert("Lista de tarefas limpa!!!");
            }
        },
        created() {
            this.tarefas = localStorage.getItem("tarefas") ? JSON.parse(localStorage.getItem("tarefas")) : this.tarefas;
        },
        updated() {
            localStorage.setItem("tarefas", JSON.stringify(this.tarefas));
        }
    }
</script>
<template>
    <!-- Código HTML aqui -->
    <h2 class="subtitulo">Lista de tarefas</h2>
    <div class="row row-cols-1 row-cols-md-3 g-4 tarefas container">
        <div class="col" v-for="(tarefa, index) in tarefas">
            <div class="card h-100">
                <img src="../assets/img/paisagens/paisagem-1.jpg" class="card-img-top" alt="...">
                <div class="card-body d-flex flex-column align-items-center">
                    <h5 class="card-title" 
                        :class="{ concluida : tarefa.concluida }">
                        {{ tarefa.titulo }}
                    </h5>
                    <!-- <p class="card-text" v-show="tarefa.texto">{{ tarefa.texto }}</p> -->
                    <button 
                        @click="tarefa.concluida = !tarefa.concluida" 
                        class="btn btn-primary">
                        <span v-if="!tarefa.concluida">Concluir</span>
                        <span v-else>Refazer</span>
                    </button>
                    <button 
                        @click="editarTarefa(index)" 
                        class="btn btn-warning">
                        Editar
                    </button>
                    <button 
                        @click="excluirTarefa(index)" 
                        class="btn btn-danger">
                        Excluir
                    </button>
                </div>
            </div>
        </div>
    </div>
    <div class="d-flex flex-column container-fluid margen-b">
        <form @submit.prevent class="d-flex flex-column align-items-center container">
            <input
                type="text"
                placeholder="Adicione um título para a tarefa..."
                class="form-control m-3"
                v-model="novaTarefa.titulo"
                ref="tarefa"
            />
            <!-- <input
                type="text"
                placeholder="Adicione uma tarefa..."
                class="form-control"
                v-model="novaTarefa.texto"
            /> -->
            <span class="text-danger m-3" v-show="error">{{ error }}</span>
            <div class="d-flex flex-row justify-content-around">
                <button class="btn btn-primary" @click="adicionarTarefa()">
                    Adicionar
                </button>
                <!-- <button class="btn btn-danger" @click="cancelar()">
                    Cancelar Edição
                </button> -->
                <button class="btn btn-danger" @click="removerTarefas()">
                    Limpar lista
                </button>
            </div>
        </form>
    </div>
</template>
<style scope>
    /* Estilização CSS aqui */
    .d-flex button {
        width: 160px;
        height: 50px;
        margin: 15px;
        padding: 5px;
    }

    .subtitulo {
        font-size: 35px;
        margin-bottom: 25px;
        padding-bottom: 5px;
        text-decoration: underline;
        text-align: center;
        font-weight: bold;
    }

    .item {
        font-size: 30px;
        font-weight: bold;
        text-align: center;
        line-height: 25px;
        width: 60%;
        padding: 25px;
    }

    .item:hover {
        cursor: pointer;
    }

    .concluida {
        text-decoration: line-through;
    }
    .margen-b {
        margin-bottom: 80px;
    }

    .card-tarefa {
        width: 18rem;
    }

    .tarefas {
        margin-bottom: 30px;
    }

</style>
