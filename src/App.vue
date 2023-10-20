<script setup>
import {cloneVNode, computed, ref } from 'vue'
var script = document.createElement('script');
script.src = 'https://code.jquery.com/jquery-3.6.3.min.js'; // Check https://jquery.com/ for the current version
document.getElementsByTagName('head')[0].appendChild(script);
const titulo = ref('Meu título dinâmico')
const quantidadeLetras = ref()
const isTextoInvertido = ref(false)
const nomes = ref(['Malu','Bia','Thom'])
let carros = ref([
  {nome: "Fusca", valor: 1000, cor: "Azul"},
  {nome: "Variante", valor: 2000, cor:"Amarela"},
  {nome: "Brasilia", valor: 3000, cor:"Branca"},
])
let nomeParaAdicionar = ref()
let nomeCarro = ref()
let corCarro = ref()
let valorCarro = ref()
let index = ref(-1)
let filtroCarro = ref('')
const filtroNome = ref('')
const nomesFiltrados = computed(() => {
  if (filtroNome.value == '') {
    return nomes.value
  }
  return nomes.value.filter(n => {
    return n.toLowerCase().startsWith(filtroNome.value.toLowerCase())
  })
})
const carrosFiltrados = computed(() => {
  if (filtroCarro.value == '') {
    return carros.value
  }
  return carros.value.filter(n => {
    return n.nome.toLowerCase().startsWith(filtroCarro.value.toLowerCase())
  })
})

function sortNomeCarroInverter()
  {
  let sortCarro = carrosFiltrados
  for (var i = 0; i < sortCarro.value.length; i++) { 
 
  for (var j = 0; j < (sortCarro.value.length - i - 1); j++) { 

      if (sortCarro.value[j].nome < sortCarro.value[j + 1].nome) { 

        var temp = sortCarro.value[j]
          sortCarro.value[j] = sortCarro.value[j + 1]
          sortCarro.value[j + 1] = temp 
      } 
  } 
} 
  carrosFiltrados = sortCarro
}
function sortNomeCarro(){
  let sortCarro = carrosFiltrados
  for (var i = 0; i < sortCarro.value.length; i++) { 
 
  for (var j = 0; j < (sortCarro.value.length - i - 1); j++) { 

      if (sortCarro.value[j].nome > sortCarro.value[j + 1].nome) { 

        var temp = sortCarro.value[j]
          sortCarro.value[j] = sortCarro.value[j + 1]
          sortCarro.value[j + 1] = temp 
      } 
  } 
} 
  carrosFiltrados = sortCarro
}

function sortCorCarro(){
  let sortCarro = carrosFiltrados
  for (var i = 0; i < sortCarro.value.length; i++) { 
 
  for (var j = 0; j < (sortCarro.value.length - i - 1); j++) { 

      if (sortCarro.value[j].cor > sortCarro.value[j + 1].cor) { 

        var temp = sortCarro.value[j]
          sortCarro.value[j] = sortCarro.value[j + 1]
          sortCarro.value[j + 1] = temp 
      } 
  } 
} 
  carrosFiltrados = sortCarro
}

function sortCorCarroInverter(){
  let sortCarro = carrosFiltrados
  for (var i = 0; i < sortCarro.value.length; i++) { 
 
  for (var j = 0; j < (sortCarro.value.length - i - 1); j++) { 

      if (sortCarro.value[j].cor < sortCarro.value[j + 1].cor) { 

        var temp = sortCarro.value[j]
          sortCarro.value[j] = sortCarro.value[j + 1]
          sortCarro.value[j + 1] = temp 
      } 
  } 
} 
  carrosFiltrados = sortCarro
}

function sortValorCarro(){
  let sortCarro = carrosFiltrados
  for (var i = 0; i < sortCarro.value.length; i++) { 
 
  for (var j = 0; j < (sortCarro.value.length - i - 1); j++) { 

      if (sortCarro.value[j].valor > sortCarro.value[j + 1].valor) { 

        var temp = sortCarro.value[j]
          sortCarro.value[j] = sortCarro.value[j + 1]
          sortCarro.value[j + 1] = temp 
      } 
  } 
} 
  carrosFiltrados = sortCarro
}
function sortValorCarroInverter(){
  let sortCarro = carrosFiltrados
  for (var i = 0; i < sortCarro.value.length; i++) { 
  for (var j = 0; j < (sortCarro.value.length - i - 1); j++) { 
      if (sortCarro.value[j].valor < sortCarro.value[j + 1].valor) { 
        var temp = sortCarro.value[j]
          sortCarro.value[j] = sortCarro.value[j + 1]
          sortCarro.value[j + 1] = temp 
      } 
  } 
} 
  carrosFiltrados = sortCarro
}
function upper() {
  titulo.value = titulo.value.toUpperCase()
}

function lower() {
  titulo.value = titulo.value.toLowerCase()
}

function inverter() {
  let texto_invertido = ''
  for (let i = titulo.value.length - 1; i >= 0; i--) { 
    texto_invertido += titulo.value[i] 
  }
  titulo.value = texto_invertido
  isTextoInvertido.value = !isTextoInvertido.value
}

function contarLetras() {
   quantidadeLetras.value = 
      titulo.value.split('')
       .filter(letra => 
          letra.toLowerCase() == 'â' || 
          letra.toLowerCase() == 'a' || 
          letra.toLowerCase() == 'á' || 
          letra.toLowerCase() == 'à' ).length
}

function adicionarNome() {
  nomes.value.push(nomeParaAdicionar.value)
  nomeParaAdicionar.value = ''
}
function adicionarCarro() {
  if(nomeCarro.value !== '' || corCarro.value !== '' || valorCarro <0){
  carros.value.push({nome: nomeCarro.value, valor:valorCarro.value,cor:corCarro.value })
  nomeCarro.value = ''
  corCarro.value = ''
  index= -1
  }
  
}

function excluir(nomeParaExcluir) {
  let idx = nomes.value.indexOf(nomeParaExcluir)
  if (idx > -1) {
    nomes.value.splice(idx, 1)
  }
}
function excluirCarro(nomeParaExcluir) {
  let idx = -1
  for(let i = 0; i<carros.value.length;i++){
   if(carros.value[i].nome === nomeParaExcluir){
    idx = i;   
    break;
   }
  }
  if (idx > -1) 
  {
    carros.value.splice(idx, 1)
    index = -1
  }
  nomeParaExcluir=''
}
function alterarCarro(nomeAlterar) {
  let idx = -1
  for(let i = 0; i<carros.value.length;i++){
   if(carros.value[i].nome === nomeAlterar){
    idx = i;  
    index = i;
    break;
   }
  }
  if (idx > -1) 
  {
    nomeCarro.value = carros.value[idx].nome;
    corCarro.value = carros.value[idx].cor;
    valorCarro.value = carros.value[idx].valor;
    index = idx;
  }
  nomeAlterar=''
}

function salvarCarro() {
  carros.value[index] = ({nome: nomeCarro.value, valor:valorCarro.value,cor:corCarro.value })
  nomeCarro.value = ''
  corCarro.value = ''
  index= -1
}

</script>

<template>
  <div>

    <h3>{{ titulo }}</h3>
    <button @click="upper()" >To Upper Case</button>
    <button @click="lower()" >To Lower Case</button>

    <button @click="inverter()">Inverter o título</button>

    <button @click="contarLetras()">Contar quantas letras "a", o título possui</button>

    <div v-if="quantidadeLetras">
      Quantidade de letras a : {{  quantidadeLetras }}
    </div>
    <div v-show="isTextoInvertido">
      O texto está invertido
    </div>
    <br>
    <hr>
      <div :class="{ destaque : filtroNome != '' }">
        <label for="filtroNome">Filtro</label>  
        <input type="text" id="filtroNome" v-model="filtroNome"/>
      </div>
    <hr>
    <br>
    <input type="text" v-model="nomeParaAdicionar"/>
    <button @click="adicionarNome()">Adicionar</button><br>

    <ol>
      <li v-for="(n) in nomesFiltrados">{{ n }}  
      <a href="#" @click="excluir(n)">Excluir</a>  </li>
    </ol>
    <br>
    <hr>
      <div :class="{ destaque : filtroCarro != '' }">
        <label for="filtroCarro">Filtro</label>  
        <input type="text" id="filtroCarro" v-model="filtroCarro"/>
      </div>
    <hr>
    <br>
    <div>Nome</div>
    <input type="text" v-model="nomeCarro"/>
    <div>Cor</div>
    <input type="text" v-model="corCarro"/>
    <div>Valor</div>
    <input type="number" v-model="valorCarro"/>
    <br>
    <button @click="adicionarCarro()">Adicionar</button>
    <button @click="salvarCarro()">Salvar</button>
    <br>
    <table>
      <tr>
        <td>Nome<button @click="sortNomeCarro()">↑</button><button @click="sortNomeCarroInverter()">↓</button></td>
        <td>Cor<button @click="sortCorCarro()">↑</button><button @click="sortCorCarroInverter()">↓</button></td>
        <td>Valor<button @click="sortValorCarro()">↑</button><button @click="sortValorCarroInverter()">↓</button></td>
        <td>Avaliação</td> 
      </tr>
      <tr v-for="c in carrosFiltrados">
        <td>{{ c.nome }}</td>
        <td>{{ c.cor }}</td>
        <td>{{ c.valor }}</td>
        <td v-if="c.valor > 1500">
            Preço alto
        </td>
        <td v-else>
            Preço baixo
        </td>
        <button @click="alterarCarro(c.nome)">Alterar</button>
        <button @click="excluirCarro(c.nome)">Deletar</button>
      </tr>
    </table>
   
  </div> 
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>