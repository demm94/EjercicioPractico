<template>
    <div id="add-btn">
        <button  v-on:click="addBurger" type="button" class="btn btn-primary barra">Agregar Hamburguesa</button>
    </div>
</template>

<script>
export default {
  name: 'AddBurger',
  props: {
    refreshList: Function,
  },
  methods: {
    addBurger() {
      this.$http.post('https://prueba-hamburguesas.herokuapp.com/burguer', {
        nombre: 'Cangreburger',
        ingredientes: ['Pan frica', 'Palta', 'Tomate', 'Queso', 'Hamburguesa de vacuno'],
        calorias: 600,
      }).then((response) => { this.refreshList(); }, err => console.log(err));
    },
  },
};
</script>

<style scoped>
    #add-btn {
        padding: 10px;;
    }

</style>
