<script setup>
  import { onMounted, ref  } from 'vue';
  const names = ref();
  const name = ref("");
  const ara = ref("");

  const save = () => {
    console.log(name.value);
    let tombMerete = names.value.length;
    let id = Number(names.value[tombMerete - 1].id);
    let d = {id: name.id, name : name.value, price: ara.value};
    console.log(d);    
    fetch("http://localhost:3000/products",
    {
      method : 'post',
      body : JSON.stringify(d),
      headers : {
        "Content-type" : "application/json"
      }
    })
    .then(() => letolt())
    alert("Sikeres mentés!")
  }
  const letolt = () => {
    fetch('http://localhost:3000/products')
    .then(resp => resp.json())
    .then(json => {
      names.value = json;
    })
  }

  onMounted(() => {
    letolt();
  }) 
</script>

<template>
    <h1>Termék hozzáadás</h1>
    <div class="form-container">
      <div class="input-container">
        <label for="productName">Terméknév</label>
        <input type="text" id="productName" v-model="name" >
      </div>
      <div class="input-container">
        <label for="productPrice">Ár</label>
        <input type="text" id="productPrice" v-model="ara" >
      </div>
      <button class="save-button" @click="save()">Mentés</button>
    </div>
  </template>

<style scoped>
.form-container {
  max-width: 400px;
  margin: 0 auto;
}

.input-container {
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input[type="text"] {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  padding: 10px 20px;
  background-color: white;
  color: black;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: grey; 
}
  h1{
    text-align: center;
    padding: 20px;
    font-family: fantasy ;

  }


</style>
