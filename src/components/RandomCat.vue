<template>
  <div>
    <h1>{{ msg }}</h1>
    <form @submit.prevent="getcat">
      <div class="form__input-container py-3 mb-4">
       
        <div class="row form-group">
          <div class="col-6 d-flex flex-column align-items-end">
            <label  class="mb-4" for="text">Titulo: </label>
            <label class="mb-4" for="text">Filtro: </label>
            <label class="mb-4" for="text">Color: </label>
            <label for="text">Tamaño</label>
          </div>
          
          <div class="col-6 d-flex flex-column align-items-start">
            <input v-model="titulo" class="mb-3" type="text" placeholder="Ingrese un Mensaje">
            <select v-model="filtro"  class="mb-3" name="" id="">
                <option value="" selected disabled>-- Seleccione--</option>
                <option value="blur">blur</option>
                <option value="mono">mono</option>
                <option value="sepia">sepia</option>
                <option value="negative">negative</option>
                <option value="paint">paint</option>
                <option value="pixel">pixel</option>
            </select>
            <div class="d-flex justify-content-center align-items-center mb-3">
                <select  v-model="color" class=" mr-3"  name="" id="">
                    <option value="" selected disabled>-- Seleccione--</option>
                    <option value="red">rojo</option>
                    <option value="blue">azul</option>
                    <option value="green">verde</option>
                    <option value="yellow">amarillo</option>
                    <option value="white">blanco</option>
                </select>
               <div class="color" :style="{'background-color':color}"></div>
            </div>
            <input v-model.number="tamaño" type="text" placeholder="Tamaño del titulo">
          </div>
        </div>
      </div>
      <button type="submit">Obtener mi gatito</button>
    </form>
    <div class="spinner-border mt-5" :class="{'d-none': !loading}" role="status">
      <span class="sr-only">Loading...</span>
    </div>
    <div class="mt-5 pb-5" >
        <img :src="imagen" alt="">
    </div>
  </div>
</template>

<script>
export default {
  name: 'RandomCat',
  props: {
    msg: String,
  },
  data()
  {
      return{
      filtro: "",
      color:  "",
      titulo: "",
      tamaño:0,
      imagen: "",
      loading: false
      }

  },
  methods: {
      async getcat(){
          this.loading = true;
          this.imagen = ""
          try {

                let BaseUrl = `https://cataas.com/cat/gif/says/${this.titulo}?`;

                let response = await fetch(`${BaseUrl}filter=${this.filtro}&color=${this.color}&size=${this.tamaño}`)

                this.imagen = response.url;
                this.loading = false;
        
          } catch (error) {
              console.log(error)
          }
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  font-size: 2 em;
  font-weight: 700;
  text-align: center;
  padding: 2em 0 1em;
}
.form__input-container {
  background-color: lightcoral;
}

.color{
    border-radius: 50%;
    width: 30px;
    height: 30px;
}


</style>
