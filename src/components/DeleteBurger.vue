<template>
    <div class="modal fade" id="deleteModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <h4 class="modal-title" id="exampleModalLabel">Confirmar eliminación</h4>
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                        <span aria-hidden="true">&times;</span>
                    </button>
                </div>
                <div class="modal-body">
                    <h5>Seguro que desea eliminar {{burgerName}}?</h5>
                </div>
                <div class="modal-footer">
                    <button v-on:click="deleteBurger(burgerId)" type="button" class="btn btn-primary verde" data-dismiss="modal">Aceptar</button>
                    <button type="button" class="btn btn-secondary" data-dismiss="modal">Cancelar</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'DeleteBurger',
  props: {
    refreshLista: Function,
    burgerId: String,
    burgerName: String,
  },
  methods: {
    deleteBurger(id) {
      this.$http.delete(`https://prueba-hamburguesas.herokuapp.com/burguer/${id}`)
        .then((response) => { this.refreshLista(); }, err => console.log(err));
    },
  },
};
</script>

<style scoped>

</style>
