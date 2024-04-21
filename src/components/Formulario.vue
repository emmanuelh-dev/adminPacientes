<template>
  <div class="w-full bg-black rounded-md p-4 shadow-md text-white border border-gray-400 max-w-2xl">
    <h2 class="text-2xl font-bold py-2">Seguimiento Pacientes</h2>

    <form class="space-y-4" @submit.prevent="validar">
      <Alert v-if="alert.message" :alert="alert" />
      <label for="nombre" class="block text-gray-300 text-sm mt-2">Nombre de la mascota
        <input type="text" id="nombre" class="w-full p-2 border border-gray-400 bg-neutral-950 rounded mt-1"
          placeholder="Nombre del paciente" :value="nombre" @input="$emit('update:nombre', $event.target.value)" />
      </label>
      <label for="propietario" class="block text-gray-300 text-sm mt-2">Propietario
        <input type="text" id="propietario" class="w-full p-2 border border-gray-400 bg-neutral-950 rounded mt-1"
          placeholder="Nombre del propietario" :value="propietario"
          @input="$emit('update:propietario', $event.target.value)" />
      </label>
      <label for="email" class="block text-gray-300 text-sm mt-2">Email
        <input type="email" id="email" class="w-full p-2 border border-gray-400 bg-neutral-950 rounded mt-1"
          placeholder="Email del propietario" :value="email" @input="$emit('update:email', $event.target.value)" />
      </label>
      <label for="alta" class="block text-gray-300 text-sm mt-2">Alta
        <input type="date" id="alta" class="w-full p-2 border border-gray-400 bg-neutral-950 rounded mt-1"
          placeholder="Alta" :value="alta" @input="$emit('update:alta', $event.target.value)" />
      </label>
      <label for="sintomas" class="block text-gray-300 text-sm mt-2">Síntomas
        <textarea id="sintomas" class="w-full p-2 border border-gray-400 bg-neutral-950 rounded mt-1"
          placeholder="Síntomas" :value="sintomas" @input="$emit('update:sintomas', $event.target.value)"></textarea>
      </label>
      <input type="submit" value="Registrar paciente"
        class="bg-white py-2 px-2 rounded-md w-full text-black cursor-pointer" />
    </form>
  </div>
</template>

<script setup>

import { reactive } from 'vue';
import Alert from './Alert.vue';

const props = defineProps({
  nombre: {
    type: String,
    required: true
  },
  propietario: {
    type: String,
    required: true
  },
  email: {
    type: String,
    required: true
  },
  alta: {
    type: String,
    required: true
  },
  sintomas: {
    type: String,
    required: true
  },
})

const alert = reactive({
  type: '',
  message: ''
});


defineEmits(['update:nombre', 'update:propietario', 'update:email', 'update:alta', 'update:sintomas']);

const validar = () => {
  if (Object.values(props).includes('')) {
    alert.message = 'Todos los campos son obligatorios'
    alert.type = 'error'
    return
  }

  alert.message = 'Paciente registrado correctamente'
  alert.type = 'success'
}

</script>
