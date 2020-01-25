<template>
  <div>
    <h1>Stock Hamburguesas</h1>
    <add-burger :refreshList="this.getBurgers"></add-burger>
    <table class="table">
      <thead>
      <tr>
        <th scope="col">Nombre</th>
        <th scope="col">Calorías</th>
        <th scope="col">Detalles</th>
        <th scope="col"></th>
        <th scope="col"></th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="dato of datos">
        <td>{{dato.nombre}}</td>
        <td>{{dato.calorias}}</td>
        <td><button v-on:click="burgerDetails(dato.ingredientes, dato.nombre, dato.calorias)" type="button" class="btn btn-secondary" id="btn1" data-toggle="modal" data-target="#detailsModal">Ver</button></td>
        <td><button type="button" class="btn btn-danger verde" data-toggle="modal" data-target="#editModal">Editar</button></td>
        <td><button v-on:click="deleteDetails(dato._id, dato.nombre)" type="button" class="btn btn-danger" data-toggle="modal" data-target="#deleteModal">Eliminar</button></td>
      </tr>
      </tbody>
    </table>
    <view-burger :_ingredientes="ingredientes" :_nombre="nombre" :_calorias="calorias"></view-burger>
    <delete-burger :burgerId="id" :burgerName="nombreDelete" :refreshLista="this.getBurgers"></delete-burger>
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
      id: '',
      nombreDelete: '',
    };
  },
  methods: {
    getBurgers() {
      this.$http.get('https://prueba-hamburguesas.herokuapp.com/burguer')
        .then((response) => { this.datos = response.body; }, err => console.log(err));
    },
    burgerDetails(ing, nom, cal) {
      this.ingredientes = ing;
      this.nombre = nom;
      this.calorias = cal;
    },
    deleteDetails(_id,nom) {
      this.id = _id;
      this.nombreDelete = nom;
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
