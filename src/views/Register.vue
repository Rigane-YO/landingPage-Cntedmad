<template>
    <div class="container-fluid min-vh-100 d-flex align-items-center justify-content-center bg-light py-5">
        <div class="card shadow-lg" style="max-width: 600px; width: 100%;">
            <div class="card-body p-5">
                <div class="text-center mb-4">
                    <Logo />
                    <h2 class="fw-bold">Inscription</h2>

                    <!-- Progress bar -->
                    <div class="progress mb-4" style="height: 4px">
                        <div class="progress-bar" role="progressbar"
                            :style="{ width: `${(currentStep / totalSteps) * 100}%` }"></div>
                    </div>

                    <!-- Step indicator -->
                    <div class="d-flex justify-content-between mb-4">
                        <span v-for="step in totalSteps" :key="step"
                            :class="['badge', currentStep >= step ? 'bg-primary' : 'bg-secondary']">
                            {{ step }}
                        </span>
                    </div>
                </div>

                <transition name="fade" mode="out-in">
                    <component :is="currentComponent" :formData="formData" :validationErrors="validationErrors" />
                </transition>

                <!-- Navigation buttons -->
                <div class="d-flex justify-content-between mt-4">
                    <button class="btn btn-secondary" @click="prevStep" v-if="currentStep > 1">
                        Précédent
                    </button>
                    <button class="btn btn-primary ms-auto"
                        @click="currentStep === totalSteps ? submitForm() : nextStep()">
                        {{ currentStep === totalSteps ? 'Envoyer' : 'Suivant' }}
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, defineAsyncComponent } from 'vue';
import Logo from '../components/Logo.vue';

// Importation dynamique des composants des étapes
const StepStudy = defineAsyncComponent(() => import('../components/step3/StepLevel.vue'));
const StepMajor = defineAsyncComponent(() => import('../components/stepMajor/StepMajorTrack.vue'));
const StepSecurity = defineAsyncComponent(() => import('../components/stepSecure/StepSecurity.vue'));
const StepPersonal = defineAsyncComponent(() => import('../components/step1/StepPersonal.vue'));
const StepContact = defineAsyncComponent(() => import('../components/step2/StepContact.vue'));



const currentStep = ref(1);
const totalSteps = 5;

const formData = ref({
    firstName: '',
    lastName: '',
    birthDate: '',
    address: '',
    phone: '',
    facebook: '',
    email: '',
    studyLevel: '',
    major: '',
    track: '',
    password: '',
    confirmPassword: ''
});

const validationErrors = ref({
    firstName: false,
    lastName: false,
    birthDate: false,
    address: false,
    phone: false,
    facebook: false,
    email: false,
    track: false,
    password: false
});

// Sélection du composant correspondant à l'étape actuelle
const currentComponent = computed(() => {
    switch (currentStep.value) {
        case 1: return StepPersonal;
        case 2: return StepContact;
        case 3: return StepStudy;
        case 4: return StepMajor;
        case 5: return StepSecurity;
        default: return StepPersonal;
    }
});

const nextStep = () => {
    if (currentStep.value < totalSteps) currentStep.value++;
};

const prevStep = () => {
    if (currentStep.value > 1) currentStep.value--;
};

const submitForm = () => {
    console.log('Form submitted:', formData.value);
};
</script>