<template>
  <div>
    <h1>Hamburguesas</h1>
    <h2>Stock</h2>
    <table class="table">
      <thead>
      <tr>
        <th scope="col">Nombre</th>
        <th scope="col">Calorías</th>
        <th scope="col">Detalles</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="dato of datos">
        <td>{{dato.nombre}}</td>
        <td>{{dato.calorias}}</td>
        <td><button type="button" class="btn btn-secondary" data-toggle="modal" data-target="#exampleModal">Ver</button></td>
      </tr>
      </tbody>
    </table>
    <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">

          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
            <button type="button" class="btn btn-primary">Save changes</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Burguers',
  data() {
    return {
      datos: 'Hamburguesas',
    };
  },
  methods: {
    getBurgers() {
      this.$http.get('https://prueba-hamburguesas.herokuapp.com/burguer')
        .then((response) => { this.datos = response.body; }, err => console.log(err));
    },
  },
  created() {
    this.getBurgers();
  },
};
</script>

<style lang="scss">
  li {
    padding: 4px;
    text-align: left;
  }
  table {
    margin: 10px;
  }
  .btn-secondary {
    background-color: #42b983;
    border: none;
  }
</style>
