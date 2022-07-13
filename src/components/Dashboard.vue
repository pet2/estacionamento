<template>
  <div id="carro-table">
      <Mensagem :msg="msg" v-show="msg" />
      <div>
          <div id="carro-table-heading">

                <div class="order-id"></div>
                <div>Proprietario: </div>
                <div>Modelo: </div>
                <div>Placa do carro: </div>
                <div>Horário de entrada: </div>
                <div>Horário de saída: </div>
                
            
          </div>
      </div>

      <div id="carro-table-rows">

          <div class="carro-table-row" v-for="carro in carros" :key="carro.id" >


              <div class="order-number"> {{ carro.id }}</div>
              <div> {{ carro.nome }} </div>
              <div> {{ carro.nomeCarro }} </div>
              <div> {{ carro.placaCarro }} </div>
              <div> {{ carro.horaEntrada }} </div>
              <div> {{ carro.horaSaida }} </div>
            

                  <select name="status" class="status"  @change="updateCarro($event, carro.id)">
                      <option value="">Status Carro </option>
                       <option :value="statu.tipo" v-for="statu in status" :key="statu.id" :selected="carro.status == statu.tipo"> {{ statu.tipo }} </option>
                  </select>

                  <button class="delete-btn" @click="deletarCarro(carro.id)"> Remover</button>

              
          </div>
      </div>
  </div>

</template>
    
<script>

    import Mensagem from './Mensagem.vue';
    export default {
        name: "Dashboard",

        data() {
            return {
                carros: null,
                carros_id: null,
                status: [],
                msg : null
            }
        },

        components : {
            Mensagem
        },
        methods: {

            async getCadastros() {
                const req = await fetch("http://localhost:4000/carros");
                const data = await req.json();
                this.carros = data;
                this.getStatus();
            },

            async getStatus() {
                const req = await fetch("http://localhost:4000/status");
                const data = await req.json();
                this.status = data;
            },

            async deletarCarro(id) {
                const req  = await fetch(`http://localhost:4000/carros/${id}`, {
                    method: "DELETE"
                });

                const data = await req.json();
                this.msg = `Veiculo removido com sucesso. obrigado volte sempre`;
                setTimeout(() => this.msg = "", 4000)
                this.getCadastros();
            },


            async updateCarro(event, id){
                const opcoes = event.target.value;
                const dataJson = JSON.stringify({ status: opcoes }); 
                const req =  await fetch(`http://localhost:4000/carros/${id}`, {
                    method: "PATCH",
                    headers: { "Content-Type" : "application/json" },
                    body: dataJson
                });

                const res = await req.json();
                this.msg = `O veiculo do ${res.nome} foi atualizado para ${res.status} . Obrigado `;
                setTimeout(() => this.msg = "", 3000)
                console.log(res);
            }     
        },

        mounted() {
            this.getCadastros();
        }
    }


</script>
<style scoped>

    #carro-table {

        max-width: 1200px;
        margin: 0 auto;
    }

    #carro-table-heading,
    #carro-table-rows
    .carro-table-row {

        display: flex;
        flex-wrap: wrap;
    }

    #carro-table-heading{

        font-weight: bold;
        padding: 12px;
        border-bottom: 2px solid blue;
    }

    #carro-table-heading div,
    .carro-table-row div {
        width: 19%;
    }
   .carro-table-row {
       width: 100%;
       padding: 12px;
       border-bottom: 2px solid blue;

   }

   #carro-table-heading .order-id,
   .carro-table-row .order-number {
       width: 5%;
   }

    select {
        padding:  10px 6px;
        margin-right:  12px;
    }
    .delete-btn {
        background-color: #3F7FBF;
        color: white;
        font-weight:  bold;
        padding: 10px;
        font-size: 16px;
        border: 1px solid white;
        cursor: pointer;
        transition:  .5s;
    }
    .delete-btn:hover {
        background-color: rgb(72, 200, 72);
        font-size: 18px;
    }

</style>
