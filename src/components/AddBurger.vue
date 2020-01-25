<template>
    <div id="add-btn">
        <button type="button" class="btn btn-primary barra mb-3 mt-2" data-toggle="modal" data-target="#addModal">Agregar Hamburguesa</button>
        <div class="modal fade" id="addModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
            <div class="modal-dialog" role="document">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="exampleModalLabel">Agregar Hamburguesa</h5>
                        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                            <span aria-hidden="true">&times;</span>
                        </button>
                    </div>
                    <div class="modal-body">
                        <p>
                            <input v-model="nombre" class="form-control" placeholder="Ingrese un nombre" type="text" id="nombre">
                        </p>
                        <p>
                            <input v-model="calorias" class="form-control" placeholder="Ingrese calorias" type="number" min="0" id="calorias">
                        </p>
                        <p>
                            <h5>Seleccione ingredientes:</h5>
                            <input type="checkbox" id="palta" value="Palta" v-model="ingredientes">
                            <label class="radio-btn" for="palta">Palta</label>
                            <input type="checkbox" id="tomate" value="Tomáte" v-model="ingredientes">
                            <label class="radio-btn" for="tomate">Tomáte</label>
                            <input type="checkbox" id="mayonesa" value="Mayonesa" v-model="ingredientes">
                            <label class="radio-btn" for="mayonesa">Mayonesa</label>
                            <input type="checkbox" id="queso" value="Queso" v-model="ingredientes">
                            <label class="radio-btn" for="queso">Queso</label><br>
                            <input type="checkbox" id="HamburguesaV" value="Hamburguesa de Vacuno" v-model="ingredientes">
                            <label class="radio-btn" for="HamburguesaV">Hamburguesa de Vacuno</label>
                            <input type="checkbox" id="HamburguesaP" value="Hamburguesa de Pollo" v-model="ingredientes">
                            <label class="radio-btn" for="HamburguesaP">Hamburguesa de Pollo</label>
                        </p>
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" data-dismiss="modal">Cerrar</button>
                        <button v-on:click="addBurger(nombre,calorias,ingredientes)" type="button" class="btn btn-primary verde" data-dismiss="modal">Agregar</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'AddBurger',
  props: {
    refreshList: Function,
  },
  data() {
    return {
      nombre: '',
      calorias: '',
      ingredientes: [],
    };
  },
  methods: {
    addBurger(n, c, i) {
      this.$http.post('https://prueba-hamburguesas.herokuapp.com/burguer', {
        nombre: n,
        ingredientes: i,
        calorias: c,
      }).then((response) => { this.refreshList(); }, err => console.log(err));
    },
  },
};
</script>

<style scoped>
    .barra {
        padding: 10px;
    }
    label.radio-btn {
        margin: 3px;
        padding: 3px;
    }

</style>
