<script setup>

</script>

<template>
  <div class="logo-container">
    <img 
      src="/cntemad_logo.jpg"
      alt="CNTEMAD Logo"
      class="logo-image"
    />
  </div>
</template>

<style scoped>
.logo-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 2rem;
}

.logo-image {
  width: 200px;
  height: auto;
  transition: all 0.3s ease;
  border-radius: 50%;
}

@media (max-width: 768px) {
  .logo-image {
    width: 150px;
  }
}

@media (max-width: 480px) {
  .logo-image {
    width: 120px;
  }
}
</style>
