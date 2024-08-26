<script>
    // Código Javascript aqui
    export default {
        data() {
            return {
                // Propriedades aqui.
            }
        },
    }
</script>
<template>
    <!-- Código HTML aqui -->
    <h2 class="subtitulo">Lista de tarefas</h2>
    <div class="d-flex flex-column align-items-center container-fluid">
        <p class="card item text-bg-secondary">
                Tarefa 1
        </p>
        <p class="card item text-bg-secondary">
                Tarefa 2
        </p>
        <p class="card item text-bg-secondary">
                Tarefa 3
        </p>
    </div>
    <div class="d-flex flex-column container-fluid">
        <form @submit.prevent class="d-flex flex-column align-items-center container">
            <input
                type="text"
                placeholder="Adicione uma tarefa..."
                class="form-control"
            />
            <span class="text-danger m-3">MENSAGEM DE ERRO!!!</span>
            <div class="d-flex flex-row justify-content-around">
                <button class="btn btn-primary">
                    Adicionar
                </button>
                <button class="btn btn-danger">
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

</style>
