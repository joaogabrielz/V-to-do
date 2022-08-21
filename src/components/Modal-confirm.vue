<template>
<div class="modal" @click="$emit('cancel')">
  <div class="modal-background"></div>
  <div class="modal-card">
    <header class="modal-card-head">
      <p class="modal-card-title">Remover <strong>Tarefa</strong>? </p>
      <button @click="$emit('cancel')" class="delete" aria-label="close"></button>
    </header>
    <footer class="modal-card-foot is-flex is-justify-content-center">
      <button @click="$emit('confirm')" class="button is-danger">Confirmar</button>
      <button @click="$emit('cancel')" class="button">Cancelar</button>
    </footer>
  </div>
</div>
</template>

<script>
export default{
    name: "ModalConfirm",
    props:['cancel', 'confirm']
}
</script>