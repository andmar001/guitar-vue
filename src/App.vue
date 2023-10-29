<script setup>
  import { ref, reactive, onMounted } from 'vue'
  import { db } from './data/guitarras'
  import Guitarra from './components/Guitarra.vue'
  import Header from './components/Header.vue'
  import Footer from './components/Footer.vue'


  const guitarras = ref([])
  const carrito = ref([])
  const guitarra = ref({})

  onMounted(()=>{
    guitarras.value = db
    guitarra.value = guitarras.value[2]
  })

  const agregarCarrito = (guitarra) => {
    const existeCarrito = carrito.value.findIndex(producto => producto.id === guitarra.id)
    if(existeCarrito >= 0){
      carrito.value[existeCarrito].cantidad++
    }
    else{
      guitarra.cantidad = 1
      carrito.value.push(guitarra)
    }
  }

  const decrementarCantidad = (id) =>{
    const index = carrito.value.findIndex(producto => producto.id === id)
    if (carrito.value[index].cantidad <= 1) return; //si la cantidad es 1 no se puede decrementar
    carrito.value[index].cantidad--
  }

  const incrementarCantidad = (id) =>{
    const index = carrito.value.findIndex(producto => producto.id === id)
    if (carrito.value[index].cantidad >= 5) return; //si la cantidad es 5 no se puede incrementar
    carrito.value[index].cantidad++
  }

  const eliminarProducto= (id) =>{
    carrito.value = carrito.value.filter(producto => producto.id !== id)
  }

  const vaciarCarrito = () =>{
    carrito.value = []
  }

</script>

<template>

  <Header
    :carrito="carrito"
    :guitarra="guitarra"
    @incrementar-cantidad = "incrementarCantidad"
    @decrementar-cantidad = "decrementarCantidad"
    @agregar-carrito="agregarCarrito"
    @eliminar-producto="eliminarProducto"
    @vaciar-carrito="vaciarCarrito"
  />

  <main class="container-xl mt-5">
    <h2 class="text-center">Nuestra Colección</h2>
    
    <div class="row mt-5">

      <Guitarra 
        v-for="guitarra in guitarras" 
        :key="guitarra.id" :guitarra="guitarra" 
        @agregar-carrito="agregarCarrito"    
      />
    
    </div>

  </main>

  <Footer/>
    
</template>

<style scoped></style>
