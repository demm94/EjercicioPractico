<template>
    <div class="modal fade" id="editModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <h4 class="modal-title" id="exampleModalLabel">Editar Hamburguesa</h4>
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                        <span aria-hidden="true">&times;</span>
                    </button>
                </div>
                <div class="modal-body">
                    <p>
                        <input v-model="arr.editNombre" class="form-control" :placeholder="data.nombre" type="text" id="editNombre">
                    </p>
                    <p>
                        <input v-model="arr.editCalorias" class="form-control" :placeholder="data.calorias" type="text" id="editCalorias">
                    </p>
                    <p>
                    <h5>Seleccione ingredientes:</h5>
                    <input type="checkbox" id="palta" value="Palta" v-model="arr.editIngredientes">
                    <label class="radio-btn" for="palta">Palta</label>
                    <input type="checkbox" id="tomate" value="Tomáte" v-model="arr.editIngredientes">
                    <label class="radio-btn" for="tomate">Tomáte</label>
                    <input type="checkbox" id="mayonesa" value="Mayonesa" v-model="arr.editIngredientes">
                    <label class="radio-btn" for="mayonesa">Mayonesa</label>
                    <input type="checkbox" id="queso" value="Queso" v-model="arr.editIngredientes">
                    <label class="radio-btn" for="queso">Queso</label><br>
                    <input type="checkbox" id="HamburguesaV" value="Hamburguesa de Vacuno" v-model="arr.editIngredientes">
                    <label class="radio-btn" for="HamburguesaV">Hamburguesa de Vacuno</label>
                    <input type="checkbox" id="HamburguesaP" value="Hamburguesa de Pollo" v-model="arr.editIngredientes">
                    <label class="radio-btn" for="HamburguesaP">Hamburguesa de Pollo</label>
                    </p>
                </div>
                <div class="modal-footer">
                    <button v-on:click="editBurger(data._id, arr)" type="button" class="btn btn-primary verde" data-dismiss="modal">Guardar cambios</button>
                    <button type="button" class="btn btn-secondary" data-dismiss="modal">Cerrar</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'EditBurger',
  props: {
    data: Object,
    refreshLista: Function,
  },
  data() {
    return {
      arr: {
        editNombre: '',
        editCalorias: '',
        editIngredientes: [],
      },
    };
  },
  methods: {
    editBurger(id, arr) {
      this.$http.put(`https://prueba-hamburguesas.herokuapp.com/burguer/${id}`, {
        nombre: arr.editNombre,
        calorias: arr.editCalorias,
        ingredientes: arr.editIngredientes,
      })
        .then((response) => { this.refreshLista(); }, err => console.log(err));
    },
  },
};
</script>

<style scoped>
    label.radio-btn {
        margin: 3px;
        padding: 3px;
    }
</style>
