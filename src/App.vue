<template>
  <div class="container mx-auto mt-16">

    <Header />

    <div class="md:flex mt-12 gap-4 justify-around">
      <Formulario v-model:pet="pacient.pet" v-model:propietario="pacient.propietario" v-model:email="pacient.email"
        v-model:alta="pacient.alta" v-model:sintomas="pacient.sintomas" @save-patient="savePatient" :id="pacient.id" />
      <div
        class="max-w-2xl w-full overflow-y-auto max-h-[40rem] bg-black rounded-md p-4 shadow-md text-white border border-gray-400">
        <h2 class="text-2xl font-bold py-2">{{ pacients.length > 0 ? 'Lista Pacientes' : 'Comienza agregando uno.' }}</h2>
        <div v-if="pacients.length > 0" class=" space-y-4">
          <div v-for="pacient in pacients" :key="pacient.id">
            <Pacient :pacient="pacient" @edit="editPatient" @delete="deletePatient" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import Header from './components/Header.vue'
import Formulario from './components/Formulario.vue'
import { ref, reactive, onMounted, watch } from 'vue';
import Pacient from './components/Pacient.vue';

const pacients = ref([]);

const pacient = reactive({
  id: null,
  pet: '',
  propietario: '',
  email: '',
  alta: new Date().toISOString().split('T')[0],
  sintomas: ''
});


onMounted(() => {
  const pacientsLocal = localStorage.getItem('pacients');
  if (pacientsLocal) {
    pacients.value = JSON.parse(pacientsLocal);
  }
})

watch(pacients, (newPacients, oldPacients) => {
  localStorage.setItem('pacients', JSON.stringify(newPacients));
})

const saveToLocalstorage = () => {
  localStorage.setItem('pacients', JSON.stringify(pacients.value));
}

function resetForm() {
  pacient.id = '';
  pacient.pet = '';
  pacient.propietario = '';
  pacient.email = '';
  pacient.sintomas = '';
}

const editPatient = (id) => {

  const foundPacient = pacients.value.find(p => p.id === id);

  pacient.id = foundPacient.id;
  pacient.pet = foundPacient.pet;
  pacient.propietario = foundPacient.propietario;
  pacient.email = foundPacient.email;
  pacient.alta = foundPacient.alta;
  pacient.sintomas = foundPacient.sintomas;
}

const deletePatient = (id) => {
  pacients.value = pacients.value.filter(p => p.id !== id);
}

const savePatient = () => {

  if (!pacient.id) {
    pacients.value.push({
      ...pacient,
      id: Date.now()
    }
    );
  } else {
    const index = pacients.value.findIndex(p => p.id === pacient.id);
    pacients.value[index] = { ...pacient };
  }
  saveToLocalstorage();
  resetForm();
}


</script>
