<template>
    <div :class="{'cliente': !isPremium,'cliente-premium': isPremium}" >
        <h3>Responsavel: {{ cliente.nome }} </h3>
        <p>Crianças Menor de 6 Meses: {{ cliente.criancas6meses }} </p>
        <p>Crianças em AME: {{ cliente.criancaAme }} </p>
        <p>Criancas Menor de 2 Anos: {{ cliente.criancas2Anos }} </p>
        <p>Gestantes: {{ cliente.gestantes }} </p>
        <p>Gestantes Menor de 20 Anos: {{ cliente.gestantesAte20Anos }} </p>
        <p>Familias: {{ cliente.familias }} </p>
        <p>Familias Acompanhadas: {{ cliente.familiasAcompanhada }} </p>
     
        <button class="btn btn-primary" @click="emitirEventoDelete">Deletar</button>

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
            return this.cliente.criancaAme.toUpperCase();
        },   
        idEspecial: function() {
            return (this.cliente.criancaAme + this.cliente.nome + this.cliente.id).toUpperCase();
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