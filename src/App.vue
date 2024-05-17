<script setup>
import { ref } from 'vue'
let name = ref('')
let price = ref('')
let cost = ref('')
let proveedor = ref('')
let array = ref([])
function costoTotal () {
  return array.value.reduce((total, item) => total + (item.costo * item.cantidad), 0)
}
function precioTotal () {
  return array.value.reduce((total, item) => total + (item.precio * item.cantidad), 0)
}
function gananciaTotal () {
  return precioTotal() - costoTotal()
}

function guardar() {
  let cantidad = 1
  let todo = {
    nombre: name.value,
    precio: price.value,
    costo: cost.value,
    cantidad: cantidad,
    proveedor: proveedor.value
  }
  array.value.push(todo)
  name.value = ''
  price.value = ''
  cost.value = ''
  proveedor.value = ''
}
function sumar(item){
  item.cantidad += 1
}
function restar(item){
  if(item.cantidad >= 1){
    item.cantidad -= 1
  }
  if (item.cantidad === 0) {
    const index = array.value.indexOf(item);
    if (index > -1) {
      array.value.splice(index, 1);
    }
  }
}
</script>
<template>
  <div id="all">
    <div id="peticion">
      <label for="name">Dígite nombre del producto</label><br>
      <input type="text" name="" id="name" placeholder="Nombre..." v-model="name"><br><br>

      <label for="price">Dígite el precio</label><br>
      <input type="number" name="" id="price" placeholder="Precio..." v-model="price"><br><br>

      <label for="cost">Dígite el costo</label><br>
      <input type="number" name="" id="cost" placeholder="Costo..." v-model="cost"><br><br>

      <label for="proveedor">Dígite nombre del proveedor</label><br>
      <input type="text" name="" id="proveedor" placeholder="Proveedor..." v-model="proveedor"><br><br>

      <button @click="guardar()">Guardar</button>
    </div>
    <hr>
    <div id="total">
      <fieldset id="field">
        <legend><h2>Costo Total</h2></legend>
        <h3>{{ costoTotal() }}</h3>
      </fieldset>
      <fieldset id="field">
        <legend><h2>Precio Total</h2></legend>
        <h3>{{ precioTotal() }}</h3>
      </fieldset>
      <fieldset id="field">
        <legend><h2>Ganancia Total</h2></legend>
        <h3>{{ gananciaTotal() }}</h3>
      </fieldset>
    </div>
    <hr>
    <div id="tabla">
      <table>
        <thead>
          <tr>
            <th>Nombre</th>
            <th>Precio</th>
            <th>Costo</th>
            <th>Cantidad</th>
            <th>Proveedor</th>
            <th>Opciones</th>
            <th>Ganancia</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, i) in array" :key="i">
            <td>{{ item.nombre }}</td>
            <td>{{ item.precio }}</td>
            <td>{{ item.costo }}</td>
            <td>{{ item.cantidad }}</td>
            <td>{{ item.proveedor }}</td>
            <td>
              <button @click="sumar(item)">➕</button>
              <button @click="restar(item)">❌</button>
            </td>
            <td>{{ item.ganancia }}</td>
          </tr>
        </tbody>
      </table>
    </div>

  </div>
</template>
<style>
#peticion{
  margin-left: 1%;
}
#total{
  margin-left: 1%;
}
#tabla{
  margin-left: 1%;
}
table {
  border: 1px solid black;
  border-collapse: collapse;
}
td {
  border: 1px solid black;
}
th {
  border: 1px solid black;
  /* background-color: aqua; */
}
#field{
  /* padding: 0%; */
  width: 10%;
}
h2{
  margin: 0%;
}
h3{
  margin: 1%;
  /* display: flex; */
  text-align: center;
}
</style>