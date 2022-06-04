<template>
<div>
  <div class="list" v-if="bool">
  <h1> Cristian Castaño </h1>
    <input type="text" v-model="query" v-on:keyup.enter="search()" placeholder="Ingrese lo que deseea buscar"> <br>
    <button @click="search()" class="ImgButton">Buscar</button>
    
      <div class="imgResults">
          <div v-for="item in items" :key="item.title" class="imgResults">
            <h1>Producto: {{item.title}}</h1>
            <img :src="item.thumbnail">
            <h2>Precio: {{item.price}}</h2>
            <button variant="dark" href="#" @click="SeeProduct(item.id)" >Mostrar</button>
          </div>
      </div>
  </div>
  <div class="product" v-if="bool==false">
    <h1>{{item.title}}</h1>
    <img :src="item.pictures[0].secure_url">
    <h2>Precio: {{item.price}}  {{item.currency_id}}</h2>
    <h3>{{item.warranty}}</h3>
     <h3>Estado: {{item.condition}}</h3>
    <h3> </h3>
    <button variant="dark" href="#" @click="search()" >Volver</button>
    <h3> </h3>
  </div>
</div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data(){
    return{
      query:'',
      item: null,
      items : null,
      bool: true,
    }
  },
  methods : {
     async search(){
       this.bool=true
       let data = await axios.get('https://api.mercadolibre.com/sites/MCO/search?q='+this.query)
        .then( res=>{
          return res.data.results;
        })
        this.items=null;
        this.items=data;
        console.log(data);
     },

      async SeeProduct(id){
        this.bool=false;
       let data = await axios.get('https://api.mercadolibre.com/items/'+id)
        .then( res=>{
          return res.data;
        })
        this.item=null;
        this.item=data;
        console.log(this.item);
     },

  },
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
