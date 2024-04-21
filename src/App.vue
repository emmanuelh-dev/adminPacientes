<template>
  <div class="container mx-auto mt-16">

    <Header />

    <div class="md:flex mt-12 gap-4 justify-around">
      <Formulario
        v-model:nombre="paciente.nombre"
        v-model:propietario="paciente.propietario"
        v-model:email="paciente.email"
        v-model:alta="paciente.alta"
        v-model:sintomas="paciente.sintomas"
      />
      <div class="max-w-2xl w-full overflow-y-scroll bg-black rounded-md p-4 shadow-md text-white border border-gray-400">
        <h2 class="text-2xl font-bold py-2">{{ pacientes.length > 0 ? 'Lista Pacientes' : 'Comienza agregando uno.' }}</h2>
      </div>
    </div>
  </div>
</template>

<script setup>
import Header from './components/Header.vue'
import Formulario from './components/Formulario.vue'
import ListaPaciente from './components/ListaPaciente.vue'
import { ref, reactive } from 'vue';

const pacientes = ref([]);

const paciente = reactive({
  nombre: '',
  propietario: '',
  email: '',
  alta: '',
  sintomas: ''
});

</script>
