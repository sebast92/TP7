<template>

  <section>
    <div class="jumbotron">
      <h2>Usuarios</h2>
      <hr>
      <hr>
      <br>



      <button class="btn btn-success my-3 mr-2" @click="getUsuariosAsyncAwait()">GET Async Await</button>
      <button class="btn btn-success my-3 mr-2" @click="getUsuariosThenCatch()">GET Then Catch</button>

      
      <div v-if="requestResolved == true && usuarios.length == 0">No se encontraron usuarios</div>
      <div v-else>
      <div class="media alert alert-info" v-for="(usuario,index) in usuarios" :key="index">
          <img :src="usuario.foto" class="mr-3" width="400" :alt="usuario.nombre" :style="{ 'border-radius' : '10px' }">
          <div class="media-body">
              <h4 class="mt-0"><u>Usuario {{ index + 1 }} - ID: {{ usuario.id }}</u></h4>
              <br>
              <p>Nombre: <b>{{ usuario.name }}</b></p>
              <p>Email: <i>{{ usuario.email }}</i></p>
              <p>Edad: {{ usuario.age }}</p>

          </div>
      </div>      
    </div>
    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-components-usuarios',
    props: [],
    mounted () {

    },
    data () {
      return {

        url: 'https://635e8a8303d2d4d47af10cea.mockapi.io//users/',
        usuarios : [],
        requestResolved : false
      }
    },
    methods: {


      async getUsuariosAsyncAwait() {
        try {

          let { data : usuarios } = await this.axios(this.url)
          console.log(usuarios)
          this.usuarios = usuarios
          this.requestResolved = true
        }
        catch(error) {
          console.error('Error en getUsuarios', error.message)
        }
      },


      getUsuariosThenCatch() {
        fetch(this.url)
        .then(response => {
            console.log(response)
            return response.json()
          })
          .then(respuesta => 
          { this.usuarios = respuesta 
            console.log(this.usuarios)
            this.requestResolved = true}
          )
          .catch( error => console.error(error) ) 

          
},      
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .jumbotron {
    background-color: navy;
    color: white;
  }

  hr {
    background-color: #bbb;
  }

  pre {
    color: white;
  }
  
  </style>
