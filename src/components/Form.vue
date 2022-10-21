<template>
  <form class="row">
    <div class="mb-3 col-6">
      <label for="exampleFormControlInput1" class="form-label"
        ><h5>Ingreso</h5></label
      >
      <input
        type="email"
        class="form-control"
        id="exampleFormControlInput1"
        placeholder="ingreso"
      />
    </div>
    <div class="mb-3 col-6">
      <label for="exampleFormControlInput1" class="form-label"
        ><h5>Cantidad</h5></label
      >
      <input
        type="number"
        class="form-control"
        id="exampleFormControlInput1"
        placeholder="Cantidad"
      />
    </div>
    <div>
      <button class="btn col-12">Agregar</button>
    </div>
  </form>
</template>

<script>
export default {};
</script>

<style scoped>
.btn {
  background-color: gold;
}
</style>
