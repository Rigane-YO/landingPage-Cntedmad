<template>
  <div>
    <h4 class="mb-4">Informations personnelles</h4>

    <div class="mb-3">
      <label class="form-label">Nom</label>
      <input 
        type="text" 
        class="form-control" 
        v-model="formData.lastName"
        :class="{ 'is-invalid': validationErrors.lastName }"
        @input="checkValidation"
      >
      <div v-if="validationErrors.lastName" class="invalid-feedback active">
        Veuillez entrer votre nom.
      </div>
    </div>

    <div class="mb-3">
      <label class="form-label">Prénom</label>
      <input 
        type="text" 
        class="form-control" 
        v-model="formData.firstName"
        :class="{ 'is-invalid': validationErrors.firstName }"
        @input="checkValidation"
      >
      <div v-if="validationErrors.firstName" class="invalid-feedback active">
        Veuillez entrer votre prénom.
      </div>
    </div>

    <div class="mb-3">
      <label class="form-label">Date de naissance</label>
      <input 
        type="date" 
        class="form-control" 
        v-model="formData.birthDate"
        :class="{ 'is-invalid': validationErrors.birthDate }"
        @input="checkValidation"
      >
      <div v-if="validationErrors.birthDate" class="invalid-feedback active">
        Veuillez entrer votre date de naissance.
      </div>
    </div>

    <div class="mb-3">
      <label class="form-label">Adresse</label>
      <textarea 
        class="form-control" 
        v-model="formData.address"
        :class="{ 'is-invalid': validationErrors.address }"
        @input="checkValidation"
      ></textarea>
      <div v-if="validationErrors.address" class="invalid-feedback active">
        Veuillez entrer votre adresse.
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps, toRefs, watch } from 'vue';

const props = defineProps({
  formData: Object,
  validationErrors: Object
});

const { formData, validationErrors } = toRefs(props);

// Vérifier les erreurs lors de la saisie
const checkValidation = () => {
  validationErrors.value.lastName = !formData.value.lastName;
  validationErrors.value.firstName = !formData.value.firstName;
  validationErrors.value.birthDate = !formData.value.birthDate;
  validationErrors.value.address = !formData.value.address;
};

// Surveille les changements pour retirer les erreurs dynamiquement
watch(formData, () => {
  checkValidation();
}, { deep: true });
</script>

<style scoped>
.is-invalid {
  animation: shake 0.4s ease-in-out;
  border-color: var(--danger-color);
}

.invalid-feedback {
  opacity: 0;
  transform: translateY(-5px);
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.invalid-feedback.active {
  opacity: 1;
  transform: translateY(0);
}

@keyframes shake {
  0%, 100% { transform: translateX(0); }
  25% { transform: translateX(-5px); }
  75% { transform: translateX(5px); }
}
</style>
