<template>
  <div class="min-h-screen max-w-screen-lg bg-gray-50 dark:bg-[#0F172A] font-inter p-4 overflow-y-auto relative">
    <Transition
      enter-active-class="transition-all duration-500 ease-out"
      enter-from-class="opacity-0 scale-95"
      enter-to-class="opacity-100 scale-100"
      leave-active-class="transition-all duration-500 ease-in"
      leave-from-class="opacity-100 scale-100"
      leave-to-class="opacity-0 scale-95"
    >
      <div v-if="showForm" class="w-full mx-auto p-4 sm:p-6 lg:p-16 bg-white dark:bg-gray-800 rounded-lg shadow-sm relative origin-center">
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
          <div class="flex items-center justify-between md:justify-end md:ml-20 w-full md:w-auto">
            <button class="flex items-center gap-2 border-none text-sm font-medium bg-transparent dark:text-white">
              <img src="./assets/icons/Vector.png" alt="listen" class="w-5 h-5 dark:invert">
              Écouter
            </button>
            <button class="flex items-center gap-2 text-sm font-medium bg-[#F4F4F5] dark:bg-[#334155] text-black dark:text-white px-4 py-2 rounded-md">
              <img src="./assets/icons/phone.svg" alt="phone" class="w-5 h-5 dark:invert">
              N°Vert
            </button>
          </div>
        </div>

        <!-- Temps de remplissage -->
        <div class="mb-6">
          <h2 class="text-lg font-bold mb-1 text-left dark:text-white">Temps de remplissage :</h2>
          <p class="text-sm text-gray-500 dark:text-gray-400 text-left">3 minutes</p>
        </div>

        <!-- Formulaire -->
        <form @submit.prevent="submitForm">
          <!-- Question anonymat -->
          <div class="mb-6">
            <p class="mb-3 text-left font-bold dark:text-white">Souhaitez-vous soumettre votre contribution dans l'anonymat ?</p>
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
              <label class="block mb-1 text-left font-bold dark:text-white">Prénom <span class="text-red-500">*</span></label>
              <input type="text" class="w-full border dark:border-gray-600 dark:bg-[#334155] dark:text-white rounded-md p-2 text-left" placeholder="Saisir votre prénom">
            </div>
            <div class="form-group">
              <label class="block mb-1 text-left font-bold dark:text-white">Nom <span class="text-red-500">*</span></label>
              <input type="text" class="w-full border dark:border-gray-600 dark:bg-[#334155] dark:text-white rounded-md p-2 text-left" placeholder="Saisir votre nom">
            </div>
          </div>

          <div class="form-group mt-4">
            <label class="block mb-1 text-left font-bold dark:text-white">Téléphone <span class="text-red-500">*</span></label>
            <div class="relative">
              <div class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 dark:text-gray-300 flex items-center gap-2">
                <span>+237</span>
                <span class="text-gray-300 dark:text-gray-500">|</span>
              </div>
              <input 
                type="tel" 
                class="w-full border dark:border-gray-600 dark:bg-[#334155] dark:text-white rounded-md p-2 pl-20 text-left" 
                placeholder="Saisir votre numéro téléphone"
              >
            </div>
          </div>

          <div class="form-group mt-4">
            <label class="block mb-1 text-left font-bold dark:text-white">Email <span class="text-red-500">*</span></label>
            <input type="email" class="w-full border dark:border-gray-600 dark:bg-[#334155] dark:text-white rounded-md p-2 text-left" placeholder="Saisir votre adresse email">
          </div>

          <div class="grid grid-cols-2 gap-6 mt-4">
            <div class="form-group">
              <label class="block mb-1 text-left font-bold dark:text-white">Age <span class="text-red-500">*</span></label>
              <select class="w-full border dark:border-gray-600 dark:bg-[#334155] dark:text-white rounded-md p-2 text-left">
                <option value="">Choisissez votre tranche d'âge</option>
              </select>
            </div>
            <div class="form-group">
              <label class="block mb-1 text-left font-bold dark:text-white">Sexe <span class="text-red-500">*</span></label>
              <select class="w-full border dark:border-gray-600 dark:bg-[#334155] dark:text-white rounded-md p-2 text-left">
                <option value="">Choisissez votre sexe</option>
              </select>
            </div>
          </div>

          <div class="mt-4">
            <p class="mb-2 text-left font-bold dark:text-white">Résidez-vous au Cameroun ? <span class="text-red-500">*</span></p>
            <div class="flex flex-col items-start gap-4">
              <label class="flex items-center gap-2 min-w-[100px]">
                <input type="radio" name="residence" value="oui" class="peer hidden">
                <div class="w-4 h-4 rounded-full border border-gray-300 dark:border-[#334155] peer-checked:bg-black peer-checked:border-black dark:peer-checked:bg-white dark:peer-checked:border-white relative">
                  <img 
                    src="./assets/icons/cocher.svg" 
                    alt="coché" 
                    class="absolute inset-0 w-4 h-4 opacity-0 peer-checked:opacity-100 dark:peer-checked:brightness-0"
                  >
                </div>
                <span class="text-left dark:text-white">Oui</span>
              </label>
              <label class="flex items-center gap-2 min-w-[100px]">
                <input type="radio" name="residence" value="non" class="peer hidden">
                <div class="w-4 h-4 rounded-full border border-gray-300 dark:border-[#334155] peer-checked:bg-black peer-checked:border-black dark:peer-checked:bg-white dark:peer-checked:border-white relative">
                  <img 
                    src="./assets/icons/cocher.svg" 
                    alt="coché" 
                    class="absolute inset-0 w-4 h-4 opacity-0 peer-checked:opacity-100 dark:peer-checked:brightness-0"
                  >
                </div>
                <span class="text-left dark:text-white">Non</span>
              </label>
            </div>
          </div>

          <div class="form-group mt-4">
            <label class="block mb-1 text-left font-bold dark:text-white">Nationalité <span class="text-red-500">*</span></label>
            <input type="text" class="w-full border dark:border-gray-600 dark:bg-[#334155] dark:text-white rounded-md p-2 text-left" placeholder="Saisir votre nationalité">
          </div>

          <div class="grid grid-cols-2 gap-6 mt-4">
            <div class="form-group">
              <label class="block mb-1 text-left font-bold dark:text-white">Département <span class="text-red-500">*</span></label>
              <select class="w-full border dark:border-gray-600 dark:bg-[#334155] dark:text-white rounded-md p-2 text-left">
                <option value="">Choisissez votre département</option>
              </select>
            </div>
            <div class="form-group">
              <label class="block mb-1 text-left font-bold dark:text-white">Commune <span class="text-red-500">*</span></label>
              <select class="w-full border dark:border-gray-600 dark:bg-[#334155] dark:text-white rounded-md p-2 text-left">
                <option value="">Choisissez votre commune</option>
              </select>
            </div>
          </div>

          <div class="form-group mt-4">
            <label class="block mb-1 text-left font-bold dark:text-white">Profession <span class="text-red-500">*</span></label>
            <input type="text" class="w-full border dark:border-gray-600 dark:bg-[#334155] dark:text-white rounded-md p-2 text-left" placeholder="Choisissez votre profession">
          </div>

          <!-- Bouton Suivant avec icône -->
          <button type="submit" class="mt-10 mb-10 bg-black dark:bg-white text-white dark:text-black px-6 py-2 rounded-md flex items-center gap-2">
            <span>Suivant</span>
            <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg" class="w-5 h-5">
              <path fill-rule="evenodd" clip-rule="evenodd" d="M12.172 6.99992L6.808 1.63592L8.222 0.221924L16 7.99992L8.222 15.7779L6.808 14.3639L12.172 8.99992H0V6.99992H12.172Z" class="fill-white dark:fill-black"/>
            </svg>
          </button>

          <!-- Ligne de séparation -->
          <hr class="border-t border-gray-200 dark:border-gray-700 mb-8">

          <!-- Texte légal en bas -->
          <p class="text-sm text-gray-500 dark:text-gray-400 text-left">
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
          class="bg-black dark:bg-white text-white dark:text-black px-6 py-3 rounded-md hover:bg-gray-800 dark:hover:bg-gray-100 transition-colors"
        >
          Ouvrir
        </button>
      </div>
    </Transition>

    <!-- Footer avec les liens sociaux -->
    <div class=" flex justify-center items-center mt-3">
      <div class="flex flex-col sm:flex-row items-center gap-2 sm:gap-4 text-gray-500 dark:text-gray-400 text-center">
        <span class="text-xs sm:text-sm">Coded by OM</span>
        <div class="flex items-center gap-3">
          <a 
            href="https://github.com/agirem" 
            target="_blank" 
            class="hover:text-[#161B1B] dark:hover:text-white transition-colors duration-200"
          >
            <i class="fa-brands fa-github text-sm sm:text-lg"></i>
          </a>
          <a 
            href="https://twitter.com/agirem1" 
            target="_blank" 
            class="hover:text-[#161B1B] dark:hover:text-white transition-colors duration-200"
          >
            <i class="fa-brands fa-x-twitter text-sm sm:text-lg"></i>
          </a>
          <a 
            href="https://linkedin.com/in/agirem1" 
            target="_blank" 
            class="hover:text-[#161B1B] dark:hover:text-white transition-colors duration-200"
          >
            <i class="fa-brands fa-linkedin text-sm sm:text-lg"></i>
          </a>
        </div>
      </div>
    </div>

    <!-- Bouton de basculement du thème -->
    <button 
      @click="toggleDarkMode"
      class="fixed top-4 right-4 p-2 rounded-full bg-gray-200 dark:bg-gray-700 hover:bg-gray-300 dark:hover:bg-gray-600 transition-colors duration-300"
      :aria-label="isDarkMode ? 'Activer le mode clair' : 'Activer le mode sombre'"
    >
      <!-- Icône soleil pour le mode clair -->
      <svg v-if="isDarkMode" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-yellow-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
      </svg>
      <!-- Icône lune pour le mode sombre -->
      <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gray-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
      </svg>
    </button>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
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

// État pour le mode sombre
const isDarkMode = ref(false);

// Fonction pour basculer le mode sombre
const toggleDarkMode = () => {
  isDarkMode.value = !isDarkMode.value;
  if (isDarkMode.value) {
    document.documentElement.classList.add('dark');
    localStorage.setItem('theme', 'dark');
  } else {
    document.documentElement.classList.remove('dark');
    localStorage.setItem('theme', 'light');
  }
};

// Vérifier le thème au chargement
onMounted(() => {
  const theme = localStorage.getItem('theme');
  if (theme === 'dark' || (!theme && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
    isDarkMode.value = true;
    document.documentElement.classList.add('dark');
  }
});
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&display=swap');

.font-inter {
  font-family: 'Inter', sans-serif;
}

/* Style pour les radios cochés */
input[type="radio"].peer:checked + div {
  @apply border-gray-900 dark:border-white;
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

/* Ajout des styles pour le mode sombre */
.dark {
  color-scheme: dark;
}
</style>
