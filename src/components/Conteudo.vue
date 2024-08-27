<script>
    // Código Javascript aqui
    export default {
        data() {
            return {
                // Propriedades aqui.
                tarefas: [],
                novaTarefa: {
                    texto: "",
                    concluida: false
                },
                error: ""
            }
        },
        methods: {
            adicionarTarefa: function(){
                // Código aqui
                if(this.novaTarefa.texto) {
                    this.tarefas.push(this.novaTarefa);
                    this.novaTarefa = {
                        concluida: false
                    };
                    this.error = "";
                    localStorage.setItem("tarefas", JSON.stringify(this.tarefas));
                } else {
                    this.error = "Você não informou a tarefa!!!";
                    // alert("Uma tarefa deve ser informada!!!");
                }
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
    <div class="d-flex flex-column align-items-center container-fluid">
        <p class="card item text-bg-secondary" v-for="tarefa in tarefas">
                {{ tarefa.texto }}
        </p>
    </div>
    <div class="d-flex flex-column container-fluid margen-b">
        <form @submit.prevent class="d-flex flex-column align-items-center container">
            <input
                type="text"
                placeholder="Adicione uma tarefa..."
                class="form-control"
                v-model="novaTarefa.texto"
            />
            <span class="text-danger m-3" v-show="error">{{ error }}</span>
            <div class="d-flex flex-row justify-content-around">
                <button class="btn btn-primary" @click="adicionarTarefa()">
                    Adicionar
                </button>
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

</style>
