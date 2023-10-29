# Levantar server de vue
npm run serve

# API styles 
los componentes de vue se escribir en 2 apis diferentes: Options API y Composition API.
# Options API
define la instancia de vue como un objeto y se le pasan las propiedades y metodos que se necesiten
# Composition API - forma mas moderna 
se define composition API añadiendo setup al <script>
<script setup> // setup es una palabra reservada para usar composition API
  // variables
  // funciones
  // lifecycle hooks
</script>

# State en VUE
El state determina la situacion actual de la aplicacion, es decir, el estado de los datos en un momento dado.
El state o estado no es siempre igual, tiende a cambiar en base a las acciones que se realicen en la aplicacion.(clicks, formularios, navegacion, etc)
Vue nos permite crear un state global que se puede acceder desde cualquier componente de la aplicacion.
Las funciones usadas son reactive y ref. ambas se importan de vue. Estan disponibles con composition API.
Una vez que el state cambie el DOM el DOM se actualiza automaticamente.
Reactive siempre es un objeto, ref puede ser un objeto o un valor primitivo, ejemplo.
- import { reactive } from 'vue'
const libro = reactive({
  disponible: true,
  titulo: 'El señor de los anillos',
  autor: 'J.R.R. Tolkien',
  genero: 'Fantasia',
  paginas: 1200
})

# acceder a las propiedades del reactive
- import { reactive } from 'vue'
console.log(libro.disponible) // true
console.log(libro.titulo) // El señor de los anillos
console.log(libro.autor) // J.R.R. Tolkien
# modificar las propiedades del reactive
- import { reactive } from 'vue'
libro.disponible = false
libro.titulo = 'El hobbit'
console.log(libro.disponible) // false

# State con ref 
import { ref } from 'vue'
const clientes = ref([])
const libro = ref({})
const auth = ref(false)
const edad = ref(0)
const mensaje = ref('hola')

# acceder a las propiedades del ref
const clientes = ref([])
const libro = ref({})
const auth = ref(false)
const mensaje = ref('hola')

console.log(clientes.value) // proxy
console.log(libro.value) // {}
console.log(auth.value) // false
console.log(mensaje.value) // hola

# reescribir un ref
clientes.value.push(nuevoCliente)
auth.value = true
mensaje.value = 'hola mundo'

# Props
vue.js usa props para pasar informacion de un componente padre a un componente hijo.
estos pueden ser datos estaticos o reactivos.

# Eventos 
v:on:click="nombreFuncion"
- ejemplo
-- inline handlers
<button 
  type="button" 
  class="btn btn-dark w-100 "
  v-on:click="numero++"
>
Agregar al Carrito
</button>
-- methods handlers
son utiles cuando se hacen muchas cosas en el evento
- ejemplo
-- validaciones en formularios
<script setup>
  const numero = ref(0)
  const incrementar = () => {
    numero.value++
  }
</script>
<button 
  type="button" 
  class="btn btn-dark w-100 "
  v-on:click="incrementar"
>Agregar al Carrito</button>
</div>

-- con otra sintaxis
<button 
  type="button" 
  class="btn btn-dark w-100 "
  @click="incrementar"
>Agregar al Carrito</button>

# componente event 
- ejemplo
@click="incrementar($event)"
@submit.prevent="enviarFormulario($event)"
-- para comunicar un componente hijo con un componente padre

ejemplo
# Componente padre
  const incrementar = () => {
    alert('click en el boton')  
  }
  <Guitarra 
    v-for="guitarra in guitarras" 
    :key="guitarra.id" :guitarra="guitarra" 
    @incrementar="incrementar"    
  />

# Componente hijo
  //declarar emit del componente padre
  defineEmits(['incrementar'])
  <button 
    type="button" 
    class="btn btn-dark w-100 "
    @click="$emit('incrementar')"
  >Agregar al Carrito</button>

-- eventos definirlos con dos palabras cuando son descriptivos
agregar-carrito - emit

# compute properties
son funciones que se ejecutan cuando una propiedad cambia.

# build
npm run build
- crea una carpeta dist con los archivos para produccion