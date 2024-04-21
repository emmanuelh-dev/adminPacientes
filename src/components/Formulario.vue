<template>
  <div class="max-w-2xl w-full bg-black rounded-md p-4 shadow-md text-white border border-gray-400">
    <h2 class="text-2xl font-bold py-2">Seguimiento Pacientes</h2>

    <form class="space-y-4" @submit.prevent="validar">
      <Alert v-if="alert.message" :alert="alert" />
      <label for="pet" class="block text-gray-300 text-sm mt-2">Nombre de la mascota
        <input type="text" id="pet" class="w-full p-2 border border-gray-400 bg-neutral-950 rounded mt-1"
          placeholder="Nombre del paciente" :value="pet" @input="$emit('update:pet', $event.target.value)" />
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
      <input type="submit" :value="[editign ? 'Editar Paciente' : 'Registrar Paciente']"
        class="bg-white py-2 px-2 rounded-md w-full text-black cursor-pointer" />
    </form>
  </div>
</template>

<script setup>

import { computed, reactive } from 'vue';
import Alert from './Alert.vue';

const props = defineProps({
  id: {
    type: [String, null],
    required: false
  },
  pet: {
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


const emit = defineEmits(['update:pet', 'update:propietario', 'update:email', 'update:alta', 'update:sintomas', 'save-patient']);

const validar = () => {
  if (Object.values(props).includes('')) {
    alert.message = 'Todos los campos son obligatorios'
    alert.type = 'error'
    return
  }
  emit('save-patient')
  alert.message = 'Paciente registrado correctamente'
  alert.type = 'success'
}

const editign = computed(() => {
  return props.id
})

</script>
