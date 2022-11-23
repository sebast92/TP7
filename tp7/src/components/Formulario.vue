<template>
  <section class="src-components-ingreso">
    <div class="jumbotron">
      <h2>Registro</h2>

      <hr>
      <br>

      <vue-form :state="formState" @submit.prevent="enviar()">

        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input type="text" id="nombre" class="form-control" autocomplete="off" v-model.trim="formData.nombre"
            name="nombre" required entre-3-15-caracteres>

          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-2 mr-1">Campo requerido.</div>
            <div slot="entre-3-15-caracteres" class="alert alert-danger mt-2 mr-1">
              Este campo debe poseer entre {{ MinLengthNombre }} y {{ MaxLengthNombre }} caracteres para una correta
              representacion del nombre.
            </div>
          </field-messages>
        </validate>

        <br>

        <validate tag="div">
          <label for="edad">Edad</label>
          <input type="number" id="edad" class="form-control" autocomplete="off" v-model.number="formData.importe"
            name="importe" required entre-18-120-anios>

          <field-messages name="pagar" show="$dirty">
            <div slot="required" class="alert alert-danger mt-2 mr-1">Campo requerido.</div>
            <div slot="entre-18-120-anios" class="alert alert-danger mt-2 mr-1">
              Este campo debe poseer entre {{ MinEdad }} y {{ MaxEdad }} caracteres para una correta
              representacion del nombre.</div>
          </field-messages>
        </validate>

        <br>

        <validate tag="div">
          <label for="email">Email</label>
          <input 
            type="email" 
            id="email" 
            class="form-control" 
            autocomplete="off"
            v-model.trim="formData.email" 
            name="email"
            required
          >
          <!-- mensajes de validación -->
          <field-messages name="email" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="email" class="alert alert-danger mt-1">Email no válido</div>
          </field-messages>
        </validate>
        <br>

        <button class="btn btn-success my-3 mx-3" :disabled="formState.$invalid">Enviar</button>

      </vue-form>


    </div>

  </section>
</template>


<script>

  export default  {
    name: 'src-components-formulario',
    props: [],
    mounted () {

    },
    data () {
      return {
        formState : {},
        formData: this.getInitialData(),
        nombreMinLength: 3,
        nombreMinLength: 15,
        edadMin: 16,
        edadMax: 110
      }
    },
    methods: {
      getInitialData() {
        return {
          nombre: null,
          edad: null,
          email: null
        }
    },
    enviar() {
      this.formData = this.getInitialData()
      this.formState._reset()
    }
    },
    computed: {

    }
}


</script>

<style scoped lang="scss">
  .src-components-formulario {

  }
</style>
