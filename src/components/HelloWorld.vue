<template>
  <div class="hello">
    <input type="text" v-model="query" placeholder="Ingrese lo que deseea buscar"> <br>
    <button @click="search()" class="ImgButton">Buscar imagen</button>
    
      <div class="imgResults">
          <div v-for="item in items" :key="item.title" class="imgResults">
            <h1>Producto: {{item.title}}</h1>
            <h2>Precio: {{item.price}}</h2>
            <button variant="dark" href="#" @click="SeeProduct(item.id)" >Mostrar</button>
          </div>
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
    }
  },
  methods : {
     async search(){
       let data = await axios.get('https://api.mercadolibre.com/sites/MCO/search?q='+this.query)
        .then( res=>{
          return res.data.results;
        })
        this.items=null;
        this.items=data;
        console.log(data);
     },
      SeeProduct(id){
       let data = axios.get('https://api.mercadolibre.com/items/'+id)
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
