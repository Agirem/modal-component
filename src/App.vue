<template>
  <div class="min-h-screen max-w-screen-lg bg-gray-50 font-inter p-4 overflow-y-auto relative">
    <Transition
      enter-active-class="transition-all duration-500 ease-out"
      enter-from-class="opacity-0 scale-95"
      enter-to-class="opacity-100 scale-100"
      leave-active-class="transition-all duration-500 ease-in"
      leave-from-class="opacity-100 scale-100"
      leave-to-class="opacity-0 scale-95"
    >
      <div v-if="showForm" class="w-full mx-auto p-4 sm:p-6 lg:p-16 bg-white rounded-lg shadow-sm relative origin-center">
        <CloseButton @click="showForm = false" />

        <!-- En-tête -->
        <div class="flex flex-col md:flex-row md:items-center justify-between mt-6 mb-6 gap-4">
          <!-- Partie gauche avec le stepper -->
          <div class="flex flex-col md:flex-row items-start md:items-center gap-4 md:gap-6 w-full md:w-auto">
            <StepperItem 
              :icon-src="userIcon"
              icon-alt="user"
              label="Présentez-vous"
              :is-active="true"
              :show-arrow="true"
            />
            <StepperItem 
              :icon-src="markPenIcon"
              icon-alt="mark-pen"
              label="Autres contributions"
              :show-arrow="true"
            />
            <StepperItem 
              :icon-src="briefcaseIcon"
              icon-alt="briefcase"
              label="Contributions"
            />
          </div>

          <!-- Partie droite avec les boutons -->
          <div class="flex items-center justify-between md:justify-end  md:ml-20 w-full md:w-auto">
            <button class="flex items-center gap-2 border-none text-sm font-medium bg-transparent">
              <img src="./assets/icons/Vector.png" alt="listen" class="w-5 h-5">
              Écouter
            </button>
            <button class="flex items-center gap-2 text-sm font-medium bg-[#F4F4F5] text-black px-4 py-2 rounded-md">
              <img src="./assets/icons/phone.svg" alt="phone" class="w-5 h-5">
              N°Vert
            </button>
          </div>
        </div>

        <!-- Temps de remplissage -->
        <div class="mb-6">
          <h2 class="text-lg font-bold mb-1 text-left">Temps de remplissage :</h2>
          <p class="text-sm text-gray-500 text-left">3 minutes</p>
        </div>

        <!-- Formulaire -->
        <form @submit.prevent="submitForm">
          <!-- Question anonymat -->
          <div class="mb-6">
            <p class="mb-3 text-left font-bold">Souhaitez-vous soumettre votre contribution dans l'anonymat ?</p>
            <div class="flex flex-col md:flex-row gap-4">
              <ChoiceCard
                name="anonymat"
                value="oui"
                title="Oui"
                description="Utilisation des données récupérées."
              />
              <ChoiceCard
                name="anonymat"
                value="non"
                title="Non"
                description="Utilisation des données récupérées."
              />
            </div>
          </div>

          <!-- Informations personnelles -->
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <div class="form-group">
              <label class="block mb-1 text-left font-bold">Prénom <span class="text-red-500">*</span></label>
              <input type="text" class="w-full border rounded-md p-2 text-left" placeholder="Saisir votre prénom">
            </div>
            <div class="form-group">
              <label class="block mb-1 text-left font-bold">Nom <span class="text-red-500">*</span></label>
              <input type="text" class="w-full border rounded-md p-2 text-left" placeholder="Saisir votre nom">
            </div>
          </div>

          <div class="form-group mt-4">
            <label class="block mb-1 text-left font-bold">Téléphone <span class="text-red-500">*</span></label>
            <div class="relative">
              <div class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 flex items-center gap-2">
                <span>+237</span>
                <span class="text-gray-300">|</span>
              </div>
              <input 
                type="tel" 
                class="w-full border rounded-md p-2 pl-20 text-left text-gray-500" 
                placeholder="Saisir votre numéro téléphone"
              >
            </div>
          </div>

          <div class="form-group mt-4">
            <label class="block mb-1 text-left font-bold">Email <span class="text-red-500">*</span></label>
            <input type="email" class="w-full border rounded-md p-2 text-left" placeholder="Saisir votre adresse email">
          </div>

          <div class="grid grid-cols-2 gap-6 mt-4">
            <div class="form-group">
              <label class="block mb-1 text-left font-bold">Age <span class="text-red-500">*</span></label>
              <select class="w-full border rounded-md p-2 text-left">
                <option value="">Choisissez votre tranche d'âge</option>
              </select>
            </div>
            <div class="form-group">
              <label class="block mb-1 text-left font-bold">Sexe <span class="text-red-500">*</span></label>
              <select class="w-full border rounded-md p-2 text-left">
                <option value="">Choisissez votre sexe</option>
              </select>
            </div>
          </div>

          <div class="mt-4">
            <p class="mb-2 text-left font-bold">Résidez-vous au Cameroun ? <span class="text-red-500">*</span></p>
            <div class="flex flex-col items-start gap-4">
              <label class="flex items-center gap-2 min-w-[100px]">
                <input type="radio" name="residence" value="oui" class="peer hidden">
                <div class="w-4 h-4 rounded-full border border-gray-300 peer-checked:bg-black relative">
                  <img 
                    src="./assets/icons/cocher.svg" 
                    alt="coché" 
                    class="absolute inset-0 w-4 h-4 opacity-0 peer-checked:opacity-100"
                  >
                </div>
                <span class="text-left">Oui</span>
              </label>
              <label class="flex items-center gap-2 min-w-[100px]">
                <input type="radio" name="residence" value="non" class="peer hidden">
                <div class="w-4 h-4 rounded-full border border-gray-300 peer-checked:bg-black relative">
                  <img 
                    src="./assets/icons/cocher.svg" 
                    alt="coché" 
                    class="absolute inset-0 w-4 h-4 opacity-0 peer-checked:opacity-100"
                  >
                </div>
                <span class="text-left">Non</span>
              </label>
            </div>
          </div>

          <div class="form-group mt-4">
            <label class="block mb-1 text-left font-bold">Nationalité <span class="text-red-500">*</span></label>
            <input type="text" class="w-full border rounded-md p-2 text-left" placeholder="Saisir votre nationalité">
          </div>

          <div class="grid grid-cols-2 gap-6 mt-4">
            <div class="form-group">
              <label class="block mb-1 text-left font-bold">Département <span class="text-red-500">*</span></label>
              <select class="w-full border rounded-md p-2 text-left">
                <option value="">Choisissez votre département</option>
              </select>
            </div>
            <div class="form-group">
              <label class="block mb-1 text-left font-bold">Commune <span class="text-red-500">*</span></label>
              <select class="w-full border rounded-md p-2 text-left">
                <option value="">Choisissez votre commune</option>
              </select>
            </div>
          </div>

          <div class="form-group mt-4">
            <label class="block mb-1 text-left font-bold">Profession <span class="text-red-500">*</span></label>
            <input type="text" class="w-full border rounded-md p-2 text-left" placeholder="Choisissez votre profession">
          </div>

          <!-- Bouton Suivant avec icône -->
          <button type="submit" class="mt-10 mb-10 bg-black text-white px-6 py-2 rounded-md flex items-center gap-2">
            <span>Suivant</span>
            <img src="./assets/icons/Icône.svg" alt="suivant" class="w-5 h-5">
          </button>

          <!-- Ligne de séparation -->
          <hr class="border-t border-gray-200 mb-8">

          <!-- Texte légal en bas -->
          <p class="text-sm text-gray-500 text-left">
            Le formulaire s'inscrit dans le cadre d'un traitement de données personnelles géré par la Direction de la Dématérialisation et de l'Automatisation des Services Judiciaires) afin de répondre à l'amélioration du système judiciaires et d'en améliorer la gestion. Vous disposez de droits sur vos données personnelles collectées et utilisées dans ce cadre (opposition, accès, rectification, suppression, limitation, portabilité, testament numérique). Pour en savoir plus, dépliez le texte ci-dessous.
          </p>
        </form>
      </div>
      
    </Transition>

    <Transition
      enter-active-class="transition-all duration-500 delay-300 ease-out"
      enter-from-class="opacity-0 scale-95"
      enter-to-class="opacity-100 scale-100"
      leave-active-class="transition-all duration-300 ease-in"
      leave-from-class="opacity-100 scale-100"
      leave-to-class="opacity-0 scale-95"
    >
      <div v-if="!showForm" class="min-h-screen flex items-center justify-center">
        <button 
          @click="showForm = true"
          class="bg-black text-white px-6 py-3 rounded-md hover:bg-gray-800 transition-colors"
        >
          Ouvrir
        </button>
      </div>
    </Transition>

    <!-- Footer avec les liens sociaux -->
    <div class=" flex justify-center items-center mt-3">
      <div class="flex flex-col sm:flex-row items-center gap-2 sm:gap-4 text-gray-500 text-center">
        <span class="text-xs sm:text-sm">Coded by OM</span>
        <div class="flex items-center gap-3">
          <a 
            href="https://github.com/agirem" 
            target="_blank" 
            class="hover:text-[#161B1B] transition-colors duration-200"
          >
            <i class="fa-brands fa-github text-sm sm:text-lg"></i>
          </a>
          <a 
            href="https://twitter.com/agirem1" 
            target="_blank" 
            class="hover:text-[#161B1B] transition-colors duration-200"
          >
            <i class="fa-brands fa-x-twitter text-sm sm:text-lg"></i>
          </a>
          <a 
            href="https://linkedin.com/in/agirem1" 
            target="_blank" 
            class="hover:text-[#161B1B] transition-colors duration-200"
          >
            <i class="fa-brands fa-linkedin text-sm sm:text-lg"></i>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import CloseButton from './components/CloseButton.vue'
import StepperItem from './components/StepperItem.vue'
import ChoiceCard from './components/ChoiceCard.vue'

import userIcon from './assets/icons/user.svg'
import markPenIcon from './assets/icons/mark-pen.svg'
import briefcaseIcon from './assets/icons/briefcase.svg'

const showForm = ref(true)
const submitForm = () => {
  // Logique de soumission du formulaire
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&display=swap');

.font-inter {
  font-family: 'Inter', sans-serif;
}

/* Style pour les radios cochés */
input[type="radio"].peer:checked + div {
  border-color: #111827;
}

input[type="radio"].peer:checked + div img {
  opacity: 1;
}

/* Ajout des styles pour l'animation */
.origin-center {
  transform-origin: center;
}

/* Pour éviter le chevauchement pendant l'animation */
.v-enter-active,
.v-leave-active {
  position: absolute;
  width: 100%;
}
</style>
