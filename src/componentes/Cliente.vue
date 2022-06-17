<template >

  <section class="src-componentes-cliente">
     <div class="jumbotron">
      <h1>Pedir datos</h1>
      
      <br>


      <button class="btn btn-success my-3 mr-3" @click="getPostsXHRcb()">PEDIR XHR</button>
      <button class="btn btn-success my-3 mr-3" @click="conFetch()">Con Fetch</button>
      <button class="btn btn-success my-3 mr-3" @click="getAxios()">Axios</button>
      <button class="btn btn-danger my-3 mr-3" @click="clientes=[]">Borrar </button>

      <div v-if="clientes.length" class="table-responsive" >
        <table class="table table-dark">
          <tr>
            <th>Nombre</th>
            <th>Email</th>
            <th>Telefono</th>
          </tr>

          <tr v-for="(cliente, index) in clientes" :key="index">
              <td>{{cliente.name}}</td>
              <td>{{cliente.email}}</td>
              <td>{{cliente.telefono}}</td>

          </tr>

        </table>
         <h4 class="alert alert-primary">se encontraron {{clientes.length}}</h4>
      </div>

     </div>
  </section>

</template>

<script >

  export default  {
    name: 'src-componentes-cliente',
    props: [],
    mounted () {

    },
    data () {
      return {
         url:'https://62aa470c3b31438554453166.mockapi.io/usuarios',
        clientes:[]
      }
    },
    methods: {
       getPostsXHRcb(){
          const xhr = new XMLHttpRequest();
          xhr.open('get', this.url)
          xhr.addEventListener('load', () =>{
            if(xhr.status == 200){
              let respuesta = JSON.parse(xhr.response)
              console.log(respuesta)
              this.clientes = respuesta
            }
            else{
              console.error('ERROR XHR CB (STATUS) ', xhr.status)
            }
          })
              xhr.send()

        },

        async conFetch(){
          
            try{
                let response = await fetch(this.url)
                let respuesta = await response.json()
                this.clientes = respuesta
              }
              catch(error){ 
                console.error('Error Fetch', error)
              }

         },

          async getAxios(){
           console.log('hola')
              try{
                let {data} = await this.axios(this.url)
                this.clientes = data
                console.log(this.clientes)
              }
              catch(error){
                console.error('Error Axios', error)
              }
        }
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-componentes-cliente {

  } .jumbotron {
    background-color: green;
    color:white;
  }
  hr{
    background-color: #bbb;
  }
</style>
