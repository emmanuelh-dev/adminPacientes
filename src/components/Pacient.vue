<template>
  <div class="p-4 border border-gray-400 px-5 py-10 rounded-xl text-white space-y-2">
    <p class="font-bold uppercase">Nombre:
      <span class="font-normal normal-case">
        {{ pacient.pet }}
      </span>
    </p>
    <p class="font-bold uppercase">Propietario:
      <span class="font-normal normal-case">
        {{ pacient.propietario }}
      </span>
    </p>
    <p class="font-bold uppercase">Email:
      <span class="font-normal normal-case">
        {{ pacient.email }}
      </span>
    </p>
    <p class="font-bold uppercase">Fecha Alta:
      <span class="font-normal normal-case">
        {{ pacient.alta }}
      </span>
    </p>
    <p class="font-bold uppercase">Síntomas:
      <span class="font-normal normal-case">
        {{ pacient.sintomas }}
      </span>
    </p>
    <div class="grid md:grid-cols-2  gap-5 mt-10">
      <button type="button" @click="$emit('edit', pacient.id)"
        class="block w-full py-2 px-10 bg-indigo-600 hover:bg-indigo-700 text-white font-bold uppercase rounded-lg">Editar</button>

      <button type="button"
        class="block w-full py-2 px-10 bg-red-600 hover:bg-red-700 text-white font-bold uppercase rounded-lg"
        @click="$emit('delete', pacient.id)">Eliminar</button>
    </div>
  </div>
</template>
<script setup>

defineEmits(['edit', 'delete'])

const props = defineProps({
  pacient: {
    type: Object,
    required: true
  }
})
</script>
