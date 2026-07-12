<script setup>
import { ref } from 'vue'

const productos = ref([
  {
    id: 1,
    nombre: 'Audífono',
    precio: 30000,
    stock: 3,
    imagen: '/img/audifono.png'
  },
  {
    id: 2,
    nombre: 'Mouse',
    precio: 20000,
    stock: 5,
    imagen: '/img/mouse.png'
  },
  {
    id: 3,
    nombre: 'Teclado',
    precio: 15000,
    stock: 10,
    imagen: '/img/teclado.png'
  },
  {
    id: 4,
    nombre: 'Gabinete',
    precio: 35000,
    stock: 4,
    imagen: '/img/gabinete.png'
  },
  {
    id: 5,
    nombre: 'Pantalla',
    precio: 175000,
    stock: 3,
    imagen: '/img/pantalla.png'
  },
  {
    id: 6,
    nombre: 'Silla',
    precio: 150000,
    stock: 2,
    imagen: '/img/silla.png'
  }
])
</script>

<template>

  <div class="container mt-4">

    <h1 class="text-center mb-4">
      Carrito de Compras
    </h1>

    <div class="row">

      <!-- Columna izquierda -->
      <div class="col-md-6">

        <h3 class="mb-3">
          Productos Disponibles
        </h3>

        <!-- Recorre todos los productos en el arreglo productos -->

        <div v-for="producto in productos" :key="producto.id" class="card mb-3">
          <div class="card-body">
            <div class="row">
              <div class="col-4">
                <img :src="producto.imagen" class="img-fluid producto-img" :alt="producto.nombre">
              </div>
              <div class="col-8">
                <h5>
                  {{ producto.nombre }}
                </h5>
                <p>
                  Precio:
                  ${{ producto.precio.toLocaleString('es-CL') }}
                </p>
                <p>
                  Stock:
                  {{ producto.stock }}
                </p>
                <button class="btn btn-primary">
                  Agregar al carrito
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Columna derecha -->
      <div class="col-md-6">
        <h3>Productos agregados</h3>
        <div class="alert alert-info">
          No hay productos agregados
        </div>
      </div>
    </div>
  </div>

</template>

<style>
/* Ajuste de las imágenes de cada producto */
.producto-img {
  width: 100px;
  height: 100px;
  object-fit: contain;
}

/* Sombra para las tarjetas */
.card {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
}
</style>