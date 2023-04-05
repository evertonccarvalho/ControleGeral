<template>
    <div :class="{'cliente': !isPremium,'cliente-premium': isPremium}" >
        <h4>Nome: {{ cliente.nome }} </h4>
        <p>Email: {{ processarEmail }} </p>
        <p v-if="showIdade === true"> Idade: {{ cliente.idade }}</p>
        <p v-else> O Usuario Escondeu a Idade</p>
        <button @click="mudarCor($event)"> Mudar Cor </button>
        <button @click="emitirEventoDelete">Deletar</button>
        <h4>Id: especial {{ idEspecial }}</h4>
    </div>
</template>


<script>
export default {
    data(){
        return{
            isPremium: false
        }
    },
    props:{

        cliente: Object,
        showIdade: Boolean

    },
    methods:{
        mudarCor: function($event){
            console.log($event)
            this.isPremium = !this.isPremium;
            
        },
        emitirEventoDelete: function(){
            console.log("emitindo do filho");
            this.$emit("meDelete",{ idDoCliente: this.cliente.id, Formulario: "Deletado Com", Sucesso:true, component: this });
        },
        testar: function(){
            console.log("testando par VALER!")
            alert("isso é um alert!")
        }
    },
    computed:{
        processarEmail: function() {
            return this.cliente.email.toUpperCase();
        },   
        idEspecial: function() {
            return (this.cliente.email + this.cliente.nome + this.cliente.id).toUpperCase();
        }
        
    },
}   
</script>

<style scoped>
    .cliente{
        background-color: antiquewhite;
    }
    .cliente-premium{
        background-color: black;
        color: yellow;
    }
</style>