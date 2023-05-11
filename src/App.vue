<script setup>
import { ref } from 'vue';

let valortotal = ref(0)

const produtos = ref([
  {
    id: 1,
    nome: 'CAMISA',
    preco: 99.90,
    quantidade: 1
  },
  {
    id: 2,
    nome: 'CAMISA',
    preco: 99.90,
    quantidade: 1
  },
  {
    id: 3,
    nome: 'CAMISA',
    preco: 129.99,
    quantidade: 1
  },
  {
    id: 4,
    nome: 'CALÇA',
    preco: 239.99,
    quantidade: 1
  },
  {
    id: 5,
    nome: 'CALÇA',
    preco: 279.99,
    quantidade: 1
  },
  {
    id: 6,
    nome: 'MOLETOM',
    preco: 359.90,
    quantidade: 1
  },
  {
    id: 7,
    nome: 'MOLETOM',
    preco: 399.90,
    quantidade: 1
  },
  {
    id: 8,
    nome: 'BONÉ',
    preco: 119.90,
    quantidade: 1
  },
  {
    id: 9,
    nome: 'BONÉ',
    preco: 139.90,
    quantidade: 1
  },
  {
    id: 10,
    nome: 'CORTA VENTO',
    preco: 379.90,
    quantidade: 1
  }
])
let carrinho = ref([])
function addcarrinho(item) {
  carrinho.value.push({
    codigo: item.id,
    nome: item.nome,
    preco: item.preco,
    quantidade: item.quantidade,
    totalitem: item.preco * item.quantidade
  })
  totalvalor()
  item.quantidade = 1
}
function totalvalor(){
  for (let contador = 0; contador < carrinho.value.length; contador++) {
    valortotal.value = valortotal.value + carrinho.value[contador].totalitem  
  }
}
function limpacarrinho() {
  carrinho.value = []
}
function remover(index) {
  carrinho.value.splice(index, 1)
}
const avf = (value) => "R$ " + value.toFixed(2).replace('.', ',')
</script>

<template>
  <div class="carrinho">
    <h1>carrinho {{ avf(valortotal) }}</h1> 
    <ul>
      <li v-for="(item, index) in carrinho" :key="index">{{ item.nome }} {{avf(item.preco) }} {{
        item.quantidade
      }} valor total {{ (item.totalitem) }}
        <button @click="remover(index)">remover item</button>
      </li>
    </ul>
    <button @click="limpacarrinho()">limpar carrinho</button>
  </div>
  <ul>
    <li v-for="(item, index) in produtos" :key="index">Item: {{ item.nome }} Valor: {{ avf(item.preco) }}
      Quantidade: {{ item.quantidade }}
      <button @click="addcarrinho(item)">adicionar</button>
      <button @click="item.quantidade++">+</button>
      <button @click="item.quantidade--" v-if="item.quantidade > 1">-</button>
    </li>
  </ul>
</template>


<style scoped>
template {
  font-family: Arial, sans-serif;
  background-color: #f5f5f5;
}

h1 {
  font-size: 2rem;
  font-weight: bold;
  text-align: center;
  margin-top: 2rem;
  margin-bottom: 1rem;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1rem;
  background-color: #fff;
  border-radius: 0.5rem;
  box-shadow: 0 0.2rem 0.5rem rgba(0, 0, 0, 0.2);
  margin-bottom: 1rem;
}

li button {
  background-color: #4caf50;
  color: #fff;
  border: none;
  border-radius: 0.5rem;
  padding: 0.5rem 1rem;
  cursor: pointer;
  transition: background-color 0.2s;
}

li button:hover {
  background-color: #3e8e41;
}

.carrinho {
  max-width: 600px;
  margin: 0 auto;
  padding: 2rem;
  background-color: #fff;
  border-radius: 0.5rem;
  box-shadow: 0 0.2rem 0.5rem rgba(0, 0, 0, 0.2);
  margin-top: 2rem;
  margin-bottom: 2rem;
}

button {
  background-color: #4caf50;
  color: #fff;
  border: none;
  border-radius: 0.5rem;
  padding: 0.5rem 1rem;
  cursor: pointer;
  transition: background-color 0.2s;
}

button:hover {
  background-color: #3e8e41;
}

button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

button + button {
  margin-left: 0.5rem;
}

input[type="number"] {
  padding: 0.5rem;
  border-radius: 0.5rem;
  border: none;
  background-color: #f5f5f5;
  font-size: 1rem;
  text-align: center;
  width: 4rem;
  margin-right: 0.5rem;
}

input[type="number"]:focus {
  outline: none;
  box-shadow: 0 0 0.2rem rgba(0, 0, 0, 0.5);
}

</style>
