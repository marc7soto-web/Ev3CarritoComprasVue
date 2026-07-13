<script setup>

import { ref, computed } from 'vue'

/* Importación de imágenes de los productos */

import audifono from './assets/productos/audifono.png'
import mouse from './assets/productos/mouse.png'
import teclado from './assets/productos/teclado.png'
import gabinete from './assets/productos/gabinete.png'
import pantalla from './assets/productos/pantalla.png'
import silla from './assets/productos/silla.png'

/* Almacena los productos agregados por el usuario */
const carrito = ref([])

/* Agrega productos al carrito */

/*
  Agrega productos al carrito validando el stock disponible */

function agregarCarrito(producto) {

  const existe = carrito.value.find(
    item => item.id === producto.id
  )
  if (existe) {

    /* Si la cantidad agregada supera el stock disponible, se muestra un mensaje */
    if (existe.cantidad >= producto.stock) {
      alert('No hay más unidades disponibles de este producto.')
      return
    }
    existe.cantidad++
  } else {

    carrito.value.push({
      ...producto,
      cantidad: 1
    })
  }
}

/* Elimina un producto del carrito de compras */

function removerProducto(id) {

  const item = carrito.value.find(
    producto => producto.id === id
  )
  if (!item) return
  item.cantidad--
  if (item.cantidad <= 0) {
    carrito.value = carrito.value.filter(
      producto => producto.id !== id
    )
  }
}


/* Productos disponibles definidos en la pauta del ejercicio */

const productos = ref([
  {
    id: 1,
    nombre: 'Audífono',
    precio: 30000,
    stock: 3,
    imagen: audifono
  },
  {
    id: 2,
    nombre: 'Mouse',
    precio: 20000,
    stock: 5,
    imagen: mouse
  },
  {
    id: 3,
    nombre: 'Teclado',
    precio: 15000,
    stock: 10,
    imagen: teclado
  },
  {
    id: 4,
    nombre: 'Gabinete',
    precio: 35000,
    stock: 4,
    imagen: gabinete
  },
  {
    id: 5,
    nombre: 'Pantalla',
    precio: 175000,
    stock: 3,
    imagen: pantalla
  },
  {
    id: 6,
    nombre: 'Silla',
    precio: 150000,
    stock: 2,
    imagen: silla
  }
])

/* Calcula automáticamente el total a pagar según los productos que existen en el carrito */

const total = computed(() => {
  return carrito.value.reduce(
    (acumulador, item) =>
      acumulador + (item.precio * item.cantidad),
    0
  )
})

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
                <button class="btn btn-primary" @click="agregarCarrito(producto)">
                  Agregar al carrito
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Columna derecha -->
      <div class="col-md-6">

        <h3>
          Productos Agregados
        </h3>

        <!-- Mensaje cuando el carrito está vacío -->
        <div v-if="carrito.length === 0" class="alert alert-info">
          No hay productos agregados.
        </div>

        <!-- Productos agregados -->
        <div v-for="item in carrito" :key="item.id" class="card mb-3">
          <div class="card-body">
            <div class="row">
              <div class="col-4">
                <img :src="item.imagen" class="img-fluid producto-img">
              </div>
              <div class="col-8">
                <h5>
                  {{ item.nombre }}
                </h5>
                <p>
                  Cantidad:
                  {{ item.cantidad }}
                </p>
                <button class="btn btn-danger" @click="removerProducto(item.id)">
                  Remover del carrito
                </button>
              </div>
            </div>
          </div>
        </div>

        <!-- Total a pagar -->
        <div class="alert alert-success mt-3">
          <h4>
            Total a pagar:
            ${{ total.toLocaleString('es-CL') }}
          </h4>
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