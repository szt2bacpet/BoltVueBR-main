<template>
  <h1>Kosár tartalma</h1>
  <div class="container">
    <table>
      <tr v-for="n in names" :key="n.id">
        <td>Terméknév: {{ n.name }}</td>
        <td>Ár: {{ n.price }}</td>
        <td>
          <button class="quantity-button" @click="decrementQuantity(n.id)">-</button>
          Mennyiség: {{ n.quantity }}
          <button class="quantity-button" @click="incrementQuantity(n.id)">+</button>
        </td>
        <td><span class="spanclass" @click="del(n.id)">❌</span></td>
      </tr>
    </table>
    <button class="button" @click="rendeles()">Rendelés</button>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';

const names = ref([]);

const letolt = () => {
  fetch('http://localhost:3000/cart')
    .then(resp => resp.json())
    .then(json => {
      names.value = json;
    })
}

onMounted(() => {
  letolt();
})

const del = (id) => {
  fetch("http://localhost:3000/cart/" + id, {
    method: "delete",
  })
    .then(() => letolt())
}

const incrementQuantity = (id) => {
  const productIndex = names.value.findIndex(item => item.id === id);
  if (productIndex !== -1) {
    names.value[productIndex].quantity++;
    updateQuantity(id, names.value[productIndex].quantity);
  }
}

const decrementQuantity = (id) => {
  const productIndex = names.value.findIndex(item => item.id === id);
  if (productIndex !== -1) {
    names.value[productIndex].quantity = Math.max(names.value[productIndex].quantity - 1, 0);
    updateQuantity(id, names.value[productIndex].quantity);
  }
}

const rendeles = () => {
  alert("Sikeres rendelés!");
  fetch("http://localhost:3000/cart", {
    method: "DELETE",
  })
}

const updateQuantity = (id, quantity) => {
  fetch(`http://localhost:3000/cart/${id}`, {
    method: 'put',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({ quantity })
  }).then(() => {
    console.log('Mennyiség frissítésre került.');
  }).catch(error => {
    console.error('Hiba történt frissítés közben', error);
  });
}
</script>

<style scoped>
.spanclass {
  cursor: pointer;
}

.container {
  text-align: center;
  padding: 20px;
  margin: 50px;
  border-radius: 10px;
}

table {
  margin: 0 auto; 
  border-collapse: collapse;
  text-align: center;
  width: 100%;
}

td, th {
  padding: 8px;
}

button {
  margin-top: 20px;
  display: inline-block;
  padding: 8px 16px;
  background-color: white;
  color: black;
  text-decoration: none;
  border-radius: 8px;
}

.quantity-button {
  margin: 0 5px;
}
h1 {
  text-align: center;
  padding: 20px;
  font-family: fantasy;
}
</style>
