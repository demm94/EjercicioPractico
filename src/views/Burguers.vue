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
        <td><button v-on:click="getIngredientes(dato.ingredientes)" type="button" class="btn btn-secondary" id="btn1" data-toggle="modal" data-target="#exampleModal">Ver</button></td>
        <td><delete-burger :burgerId="dato._id" :refreshLista="getBurgers"></delete-burger></td>
      </tr>
      </tbody>
    </table>
    <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Detalles de hamburguesa</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <h3>Ingredientes</h3>
            <h3>{{ingredientes}}</h3>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-dismiss="modal">Cerrar</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import AddBurger from '../components/AddBurger';
import DeleteBurger from '../components/DeleteBurger';

export default {
  name: 'Burguers',
  components: { DeleteBurger, AddBurger },
  data() {
    return {
      datos: 'Hamburguesas',
      components: {
        'Add-Burger': AddBurger,
        'Delete-Burger': DeleteBurger,
      },
      ingredientes: '',
    };
  },
  methods: {
    getBurgers() {
      this.$http.get('https://prueba-hamburguesas.herokuapp.com/burguer')
        .then((response) => { this.datos = response.body; }, err => console.log(err));
    },
    getIngredientes(data) {
      this.ingredientes = data;
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
  .btn-secondary {
    background-color: #42b983;
    border: none;
  }
  #botones {
    text-align: left;
  }
</style>
