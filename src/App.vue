<template>
  <div id="app" class="py-3">
    <header>
      <h1 class="text-center">Galeria de productos</h1>
    </header>

    <main class="container">
      <section class="row justify-content-center g-3">
        <div
          class="col-12 col-md-6 col-lg-4"
          v-for="producto in productos"
          :key="producto.id"
        >
          <div class="card">
            <img
              :src="producto.path"
              class="card-img-top"
              :alt="producto.nombre"
            />
            <div class="card-body">
              <h5 class="card-title">{{ producto.nombre }}</h5>
              <p class="card-text">
                {{ producto.descripcionCorta }}
              </p>

              <div>
                <button
                  class="btn btn-primary"
                  data-bs-toggle="modal"
                  data-bs-target="#miModal"
                  :data-producto-id="producto.id"
                  @click="mostrar"
                >
                  Ver detalles
                </button>
              </div>
            </div>
          </div>
        </div>
      </section>
    </main>

    <!-- Modal -->
    <div
      class="modal fade"
      id="miModal"
      tabindex="-1"
      aria-labelledby="miModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="miModalLabel">
              {{ currentProducto.nombre }}
            </h1>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            <img class="imgModal" :src="currentProducto.path" :alt="currentProducto.nombre">
            <p class="p-3" >
              <span>Descripción: </span>{{ currentProducto.descripcionLarga }}
            </p>
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              data-bs-dismiss="modal"
            >
              Close
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      productos: [
        {
          id: 1,
          nombre: "Producto 1",
          descripcionCorta: "Zapatillas 1",
          descripcionLarga: "Zapatillas marca x, color x, talla x.",
          path: "./img/zapatilla1.webp",
        },
        {
          id: 2,
          nombre: "Producto 2",
          descripcionCorta: "Zapatillas 2",
          descripcionLarga: "Zapatillas marca x, color x, talla x.",
          path: "./img/zapatilla2.webp",
        },
        {
          id: 3,
          nombre: "Producto 3",
          descripcionCorta: "Zapatillas 3",
          descripcionLarga: "Zapatillas marca x, color x, talla x.",
          path: "./img/zapatilla3.webp",
        },
      ],
      currentProducto: {},
    };
  },
  methods: {
    mostrar: function (event) {
      let element = event.target;
      let productoId = element.dataset.productoId;

      //buscar elemento dentro del array de productos
      let foundProducto = this.productos.find(
        (producto) => producto.id == productoId
      );

      if (foundProducto) {
        this.currentProducto = foundProducto;
      } else {
        alert("Producto no encontrado.");
      }
    },
  },
};
</script>

<style>
.card-img-top{
  width: 18rem;
  height: 18rem;
}
.modal-body{
  display: flex;
  flex-direction: column;
  align-items: center;
}
.imgModal{
  width: 20rem;
  height: 18rem;
}
</style>
