<template>
    <div>
      <h4 class="mb-4">Contact</h4>
      <div class="mb-3">
        <label class="form-label">Téléphone</label>
        <input 
          type="tel" 
          class="form-control" 
          v-model="formData.phone"
          :class="{ 'is-invalid': validationErrors.phone }"
        >
      </div>
      <div class="mb-3">
        <label class="form-label">Facebook</label>
        <input 
          type="text" 
          class="form-control" 
          v-model="formData.facebook"
          :class="{ 'is-invalid': validationErrors.facebook }"
        >
      </div>
      <div class="mb-3">
        <label class="form-label">Gmail</label>
        <input 
          type="email" 
          class="form-control" 
          v-model="formData.email"
          :class="{ 'is-invalid': validationErrors.email }"
        >
      </div>
    </div>
  </template>
  
  <script setup>
  import { defineProps, toRefs } from 'vue';
  
  const props = defineProps({
    formData: Object,
    validationErrors: Object
  });
  
  const { formData, validationErrors } = toRefs(props);
  </script>
  