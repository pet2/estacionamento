<template>
        <div>
            <Mensagem :msg="msg" v-show="msg" />
            <form id="carro-form" @submit="createCarro">
                <div class="input-container">

                    <label for="nome">Proprietario: </label>
                    <input type="text" id="nome" v-model="nome" placeholder="Digite o nome do proprietario : ">

                </div>
                <div class="input-container">

                    <label for="nomeCarro">Modelo: </label>
                    <input type="text" id="nomeCarro" v-model="nomeCarro" placeholder="Digite o modelo do carro ">
                    
                </div>
                <div class="input-container">

                    <label for="placaCarro">Placa do veículo: </label>
                    <input type="text" id="placaCarro" v-model="placaCarro" placeholder="Informe a placa do Carro: ">
                    
                </div>
                <div class="input-container">

                    <label for="horaEntrada">Horário de entrada: </label>
                    <input type="text" id="horaEntrada" v-model="horaEntrada" placeholder="Informe o Horário de Entrada: ">
                    
                </div>
                <div class="input-container">

                    <label for="horaSaida">Horário de saída: </label>
                    <input type="text" id="horaSaida" v-model="horaSaida" placeholder="Informe o Horário de Saída: ">
                <div>
                </div>
                    <input type="submit" class="submit-btn" value="Cadastrar o Carro">
            
                </div>
            </form>
        </div>
</template>
<script>

    import Mensagem from './Mensagem.vue';
    export default {
        name: "CarroForm",

        data() {
            return {

                nome: null,
                nomeCarro: null,
                placaCarro: null,
                horaEntrada: null,
                horaSaida: null,
                msg: null
            }
        },

        methods: {
            async createCarro(e){
                e.preventDefault();

                const data = {
                    nome: this.nome,
                    nomeCarro: this.nomeCarro,
                    placaCarro: this.placaCarro,
                    horaEntrada: this.horaEntrada,
                    horaSaida: this.horaSaida,
                    status: "Solicitado",
                }

                const dataJson = JSON.stringify(data);
                const req = await fetch("http://localhost:4000/carros",

                {
                    method: "POST",
                    headers: { "Content-Type" : "application/json"},
                    body: dataJson
                });

                const res = await req.json();
                console.log(res);
                this.msg = `Veículo cadastrado.`;
                setTimeout(() => this.msg = "", 4000)

                this.nome = "";
                this.nomeCarro = "";
                this.placaCarro = "";
                this.horaEntrada = "";
                this.horaSaida = "";
            }
        },

        components: {
            Mensagem
        }
    }

</script>
<style scoped>

    #carro-form {

        max-width: 300px;
        margin: 0 auto;;
    }
    .input-container {

        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }

    label {

        font-weight: bold;
        margin-bottom: 15px;
        color: #222;
        padding: 5px 10px;
    }

    input {

        padding: 5px 10px;
        widows: 300px;
    }
    .submit-btn {

        background-color: #3F7FBF;
        color: white;
        font-weight:  bold;
        padding: 15px;
        font-size: 16px;
        border: 5px solid ;
        cursor: pointer;
        transition:  .5s;
    }
    .submit-btn:hover {
        background-color:rgb(72, 200, 72);
        font-size: 18px;
    }
</style>