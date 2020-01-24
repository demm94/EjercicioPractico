<template>
    <button v-on:click="deleteBurger(burgerId)" type="button" class="btn btn-danger">Eliminar</button>
</template>

<script>
export default {
  name: 'DeleteBurger',
  props: {
    refreshLista: Function,
    burgerId: String,
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
