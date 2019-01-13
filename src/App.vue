<template>
  <div id="app">
    <input type="text" v-model="person" @keyup.enter="agregar_persona(person)">
    

    <div>{{person}}</div>
    <ul>
     <li v-for=" persona in lista_personas"> 
      {{persona.name}}
      <input type="	text" v-model="form.parent_id[persona.id]"@keyup.enter="actualizar_persona(persona.id,form.parent_id[persona.id])">
      <button @click="eliminar_persona (persona.id)">eliminar </button>

     </li>
    </ul> 
  </div>
</template>

<script>
export default {
  name: 'app',
  data : function() {
    return {
      LAST : 'last',
      person: 'example',
      form: {
        parent_id:[]
      },
      lista_personas: [
        {name:'josse',id:0},
        {name:'byron',id:2},
        {name:'moises',id:3},

      ]
    }
  },
  methods :{
    obtener_persona : function(params){
      if (params === this.LAST){
        return this.lista_personas[this.lista_personas.length-1].id+1
      }
       return this.lista_personas = this.lista_personas.filter(function(value, index, array){
          return value.id !=params
      })[0]
    },  
    agregar_persona: function(params){
      this.lista_personas.push({id: this.obtener_persona(this.LAST), name: params});

    },
    eliminar_persona: function(params){
      this.lista_personas = this.lista_personas.filter(function(value, index, array){
          return value.id !=params
      })
    },
    actualizar_persona: function(id,params){
      for (var i = 0; i< this.lista_personas.length; i++){
        if (this.lista_personas[i].id ==id){
          this.lista_personas[i].name =  params;
        }
      }
    }
    

  }
}
</script>

<style>
#app {
  
}
</style>
