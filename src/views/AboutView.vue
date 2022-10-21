<template>
  <div class="container mt-5">
    <div class="box1">
      <h1>Mis gastos!</h1>
      <button @click="btn1()" id="bt1" class="btn">
        <i class="bx bx-plus-medical"></i>
      </button>
    </div>
    <div v-if="status" class="box2 mt-2">
      <form @submit.prevent="add()" class="row">
        <div class="mb-3 col-6">
          <label for="exampleFormControlInput1" class="form-label"
            ><h5>Gasto</h5></label
          >
          <input
            required
            type="text"
            class="form-control"
            id="exampleFormControlInput1"
            placeholder="gasto"
            v-model="titulo"
          />
        </div>
        <div class="mb-3 col-6">
          <label for="exampleFormControlInput1" class="form-label"
            ><h5>Cantidad</h5></label
          >
          <input
            required
            type="number"
            class="form-control"
            id="exampleFormControlInput1"
            placeholder="Cantidad"
            v-model.number="cantidad"
          />
        </div>
        <div>
          <button class="btn col-12">
            Agregar <i class="bx bxs-send"></i>
          </button>
        </div>
      </form>
    </div>
    <div class="box3 mt-3 row card">
      <div class="row" v-for="ingreso in gastos" :key="ingreso">
        <div class="col-3 mt-3">
          <h6>{{ ingreso.titulo }}</h6>
        </div>
        <div class="col-4 mt-3">
          <h6>${{ ingreso.cantidad }}</h6>
        </div>
        <div class="col-4 mt-3">
          <h6>{{ ingreso.fecha }}</h6>
        </div>
        <div class="col-1">
          <button @click="() => delet(ingreso)" class="bg-danger btn">
            <h6><i class="bx bxs-trash mt-2"></i></h6>
          </button>
        </div>
      </div>
    </div>
    <div class="box6 border mt-3">
      <h5 class="mt-2">Ingreso total: ${{ total }}</h5>
      <button @click="print()" class="btn border"><h5>print</h5></button>
    </div>
  </div>
</template>

<script>
import Form from "../components/Form.vue";
export default {
  components: { Form },

  data() {
    return {
      status: true,
      titulo: "",
      cantidad: "",
      gastos: [],
      date: 0,
      total: 0,
    };
  },

  methods: {
    btn1() {
      this.status = !this.status;
    },
    add() {
      let date = new Date();
      let dia = date.getDate();
      let mes = date.getMonth();
      let year = date.getFullYear();

      const ingreso = {
        titulo: this.titulo,
        cantidad: this.cantidad,
        fecha: `${dia}/${mes + 1}/${year}`,
      };
      this.gastos.push(ingreso);

      let counter = 0;
      this.gastos.forEach((i) => {
        counter = counter + i.cantidad;
      });
      this.total = counter;
      (this.titulo = ""), (this.cantidad = ""), (this.status = false);
      localStorage.setItem("gastos", JSON.stringify(this.gastos));
    },

    delet(i) {
      let filtro = this.gastos.filter((value) => value !== i);

      this.gastos = filtro;
      let counter = 0;
      this.gastos.forEach((i) => {
        counter = counter + i.cantidad;
      });
      this.total = counter;
      localStorage.setItem("gastos", JSON.stringify(this.gastos));
    },

    print() {
      print();
    },
  },

  mounted() {
    this.gastos = JSON.parse(localStorage.getItem("gastos")) || [];
  },
};
</script>

<style scoped>
.box1 {
  display: flex;
}
.btn {
  background-color: rgb(255, 148, 41);
}
#bt1 {
  margin-left: 7rem;
}

.box3 {
  background-color: #f48ed9;
}

.box6 {
  display: flex;
  justify-content: space-between;
}
</style>
