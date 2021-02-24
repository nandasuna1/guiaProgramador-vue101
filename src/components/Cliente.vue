<template>

    <div :class="{'cliente': !isPremium, 'cliente-premium': isPremium}">
        <h4 id="cliente-nome">nome: {{cliente.nome}}</h4>
        <p>email: {{cliente.email | processarEmail}}</p>
        <p v-if="!showIdade">idade: {{cliente.idade}}</p>
        <p v-else><b>o usuario escondeu a idade</b></p>
        <p>{{cliente.id}}</p>
        <h4>IdEspecial: {{idEspecial}}</h4>
        <button @click="mudarCor($event)">Mudar cor</button>
        <button @click="emitirEventoDelete">Deletar</button>
    </div>
</template>

<script>

export default {
    data(){
        return{
            isPremium: true,
        }
    },

    props: {
        cliente: Object,
        showIdade: Boolean,
    },
    methods:{
        mudarCor: function($event){
            this.isPremium = !this.isPremium
            console.log($event)
        },
        emitirEventoDelete: function(){
            console.log("deletando")
            this.$emit("meDelete", {idDoCliente: this.cliente.id, component: this});
        },
        teste: function(){
            console.log('tetetetete')
        }
    },
    filters:{
        processarEmail: function(value){
            return value.toUpperCase()
        }
    },
    //computed properties são variaveis que são funções que retornam valores
    //da pra fazer ordenação de lista e buscas com o computed proprietiess
    computed:{
        idEspecial: function(){
            return(this.cliente.email + this.cliente.nome + this.cliente.id).toUpperCase();
        }
    }
}
</script>

<style scoped>
.cliente{
    background: rgb(235, 91, 91);
    margin-top: 15px;
}

.cliente-premium{
    padding: 5px;
    margin-top: 10px;
}

button{
    margin: 5px;
}
</style>