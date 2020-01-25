<template>
    <div class="modal fade" id="detailsModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <h4 class="modal-title" id="exampleModalLabel">Hamburguesa {{_nombre}}</h4>
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                        <span aria-hidden="true">&times;</span>
                    </button>
                </div>
                <div class="modal-body">
                    <h5>Ingredientes:</h5>
                    <span v-for="ing of _ingredientes">
                        <h6>{{ing}}</h6>
                    </span>
                    <h6><strong>Calorías: {{_calorias}}</strong></h6>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-dismiss="modal">Cerrar</button>
                </div>
            </div>
        </div>
    </div>

</template>

<script>
export default {
  name: 'ViewBurger',
  props: ['_ingredientes','_nombre','_calorias'],
};
</script>

<style scoped>

</style>
