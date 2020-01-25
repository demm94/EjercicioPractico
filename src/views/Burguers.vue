<template>
  <div>
    <h1>Hamburguesas</h1>
    <h2>Stock</h2>
    <add-burger :refreshList="this.getBurgers"></add-burger>
    <table class="table">
      <thead>
      <tr>
        <th scope="col">Nombre</th>
        <th scope="col">Calorías</th>
        <th scope="col">Detalles</th>
        <th scope="col"></th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="dato of datos">
        <td>{{dato.nombre}}</td>
        <td>{{dato.calorias}}</td>
        <td><button v-on:click="getDetails(dato.ingredientes, dato.nombre, dato.calorias)" type="button" class="btn btn-secondary verde" id="btn1" data-toggle="modal" data-target="#detailsModal">Ver</button></td>
        <td><delete-burger :burgerId="dato._id" :refreshLista="getBurgers"></delete-burger></td>
      </tr>
      </tbody>
    </table>
    <view-burger :_ingredientes="ingredientes" :_nombre="nombre" :_calorias="calorias"></view-burger>
  </div>
</template>

<script>

import AddBurger from '../components/AddBurger';
import DeleteBurger from '../components/DeleteBurger';
import ViewBurger from '../components/ViewBurger';

export default {
  name: 'Burguers',
  components: { DeleteBurger, AddBurger, ViewBurger },
  data() {
    return {
      datos: 'Hamburguesas',
      ingredientes: '',
      nombre: '',
      calorias: '',
    };
  },
  methods: {
    getBurgers() {
      this.$http.get('https://prueba-hamburguesas.herokuapp.com/burguer')
        .then((response) => { this.datos = response.body; }, err => console.log(err));
    },
    getDetails(ing, nom, cal) {
      this.ingredientes = ing;
      this.nombre = nom;
      this.calorias = cal;
    },
  },
  created() {
    this.getBurgers();
  },
};
</script>

<style lang="scss">
  table {
    margin: 10px;
  }
  .btn.verde {
    background-color: #42b983;
    border: none;
  }
  #botones {
    text-align: left;
  }
</style>
