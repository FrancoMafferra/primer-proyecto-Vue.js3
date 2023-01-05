<script setup>
import {ref, computed} from "vue"

const name ="Franco 1er Vue Dinámico"

const counter = ref(0)

const favoritos = ref([])

const increment = ()=>counter.value++;

const decrement =()=> counter.value--;

const reset =()=> (counter.value = 0)

const add =()=> {
  favoritos.value.push(counter.value)
}

const classCounter = computed(()=>{
  if(counter.value == 0) return "cero"
  if(counter.value < 0) return "negative"
  if(counter.value > 0) return "positive"
})

const bloquearBtnAdd = computed(()=>{
  const searchNum = favoritos.value.find(num => num === counter.value)
  if(searchNum === 0) return true
  return searchNum ? true : false
})

</script>

<template>

    <h1>{{ name.toUpperCase() }}</h1> <br/>
    <h2 :class = "classCounter">{{ counter }}</h2> <br/>
    <div class="btn-toolbar">

      <button @click="increment" class="btn btn-success">Aumentar</button> 
      <button @click="reset" class="btn btn-info">Reset</button> 
      <button @click="decrement" class="btn btn-danger">Decrementar</button> 
      <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-warning">Add</button> 
    </div> <br/>
    <ul> <br/>
      Números guardados
      <li
      v-for="(num, index) in favoritos"
      :key="index"
      >
      {{ num }}
      </li>
    </ul>

</template>

<style>
h1{
  color:rgb(0, 162, 255)
}
.positive{
  color:rgb(33, 158, 13)
}
.negative{
  color:rgb(255, 0, 0)
}
.cero{
  color:rgb(0, 162, 255)
}
</style>